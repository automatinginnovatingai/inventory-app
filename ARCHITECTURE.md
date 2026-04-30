# Inventory App – Architecture Overview  
Version: 2.0.0

## Overview
The Automating Innovating AI **Inventory App** is a closed‑source Windows `.exe` designed for secure, offline‑capable inventory and warehouse management. It includes automated license enforcement, SQL‑based data storage, multi‑warehouse tracking, purchase orders, reporting, and full audit‑ready transaction history.

The application supports **SQL Server Express** and **Full SQL Server**, selected during installation.  
All operations occur locally after initial license activation.

---

# Architecture

## Database Selection (Installer‑Driven)
During installation, the user selects one of two supported database modes:

### 1. SQL Server Express (local database – recommended for 1–5 users)
- Installer automatically installs and configures SQL Server Express  
- Ideal for single‑machine or small office setups  
- Zero licensing cost  

### 2. Full SQL Server (Standard/Enterprise)
- Connects to an existing SQL Server instance  
- Supports multi‑user environments and IT‑managed deployments  
- Designed for medium to large companies  

The installer writes a registry flag (`UseSQLExpress`) that determines which SQL connection page loads on first launch.

---

## License Enforcement Flow
**User Launch → License Prompt → Gumroad API Validation → Local Unlock**

- User enters their Gumroad license key on first launch  
- Key is validated via Gumroad’s `/v2/licenses/verify` endpoint  
- Valid keys unlock the application and store the license state locally  
- Periodic revalidation may occur (e.g., every 7 days)  
- License tier controls access to Basic, Pro, or Enterprise features  

After activation, the app operates fully offline.

---

## Role‑Based Access Control (RBAC)
The Inventory App includes a clean, centralized RBAC system:

### **Admin‑Only Registration**
- Only admins can register accounts  
- No employee/installer self‑registration  
- Prevents unauthorized access and maintains data integrity  

### **Global Admin**
- Full system access  
- Can configure warehouses, materials, suppliers, and system settings  
- Can manage other admins (if enabled by license tier)  

### **Local Admin**
- Restricted to operational modules  
- Cannot create companies or modify global system settings  
- Redirected to login after registration (no auto‑session creation)  

### **RBAC Enforcement**
- Centralized in `Admin_Interface.py`  
- UI dynamically adapts based on role  
- Feature access is validated before loading any module  
- Prevents unauthorized navigation or direct file access  

---

## Local Session Context
- All data stored in SQL Server Express or Full SQL Server  
- No cloud sync, Redis, or external session store  
- Secure login using salted + hashed admin credentials  
- Fully offline operation after initial license activation  

---

## Data Transfer Between Computers
The app includes a built‑in SQL migration tool:

- Generates a `.bak` backup file from the old machine  
- Restores the `.bak` file on the new machine  
- Works for both SQL Express and Full SQL Server  
- Ideal for machine upgrades or office migrations  

---

## SQL Connection Pages
The application routes users to the correct connection setup page based on installer selection:

- `sql_connection_page.py` – SQL Express  
- `sql_server_connection_page.py` – Full SQL Server  

Both pages support:
- Connection testing  
- Credential validation  
- Database creation (if needed)  
- Secure admin login setup  

---

## Core Inventory & Warehouse Workflow
**Admin Login → Material Setup → Warehouse Setup → Inventory Transactions → Reporting**

### Material Management
- Universal `Material_Info` schema  
- Supports SKUs, units, cost, categories, and reorder points  
- Supplier linking and preferred vendor tracking  

### Warehouse Management
- Dedicated `Warehouse` table  
- Multi‑warehouse support  
- Per‑warehouse stock tracking via `Warehouse_Inventory`  

### Inventory Transactions
- All movements logged in `Inventory_Transactions`  
- Transfers logged in `Warehouse_Transfers`  
- Includes reason codes, references, supplier info, timestamps  
- Fully audit‑ready  

### Purchase Orders
- PO lifecycle: Pending → Ordered → Received → Closed  
- Receiving updates stock automatically  
- Supplier‑linked PO workflow  

### Reporting
- Excel and PDF reports  
- Inventory summaries, valuation, and transaction logs  
- Customizable filenames  
- Print‑ready formatting  

---

## UI Architecture
- Dashboard‑driven navigation  
- Submenus grouped by functional modules  
- RBAC‑aware UI rendering  
- Multi‑resolution `.ico` (256 → 16 px) for crisp display across Windows views  

---

## File Storage & Export
All exports are stored locally under a user‑selectable root folder:

- `\Inventory_Exports\Reports\` – inventory, valuation, and transaction reports  
- `\Inventory_Exports\Backups\` – `.bak` files and optional CSV/Excel dumps  

Paths are configurable from the admin settings screen and never synced externally.

---

## Offline‑First Design
- All operations occur locally  
- SQL Server handles all data persistence  
- No external dependencies after license activation  
- Ideal for field‑service, warehouse, and low‑connectivity environments  

---

## Auto‑Update System
- Checks for new versions on launch  
- Downloads and installs updates when available  
- Ensures clients always run the latest stable release  

---

## Summary
The Inventory App is engineered for reliability, offline operation, secure admin workflows, and transparent audit‑ready inventory control. With SQL‑based storage, RBAC enforcement, multi‑warehouse support, and a modernized UI, it delivers a professional‑grade inventory system suitable for small businesses and enterprise environments alike.
