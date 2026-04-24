# Inventory App – Architecture Overview

## Overview
Inventory App is a closed‑source Windows `.exe` application built for offline operation, secure license enforcement, and automated inventory control. It provides a fast, local inventory and warehouse management system designed to work independently of any specific trade, with support for multi‑warehouse stock, transfers, and transaction history.

The application supports both SQL Server Express and Full SQL Server, selected during installation.

---

# Architecture

## Database selection (installer‑driven)
During installation, the user selects one of two supported database modes:

### 1. SQL Server Express (local database – recommended for 1–5 users)
- Installer automatically installs and configures SQL Server Express  
- Ideal for single‑machine setups or small office networks  
- No licensing cost  

### 2. Full SQL Server (Standard/Enterprise)
- User connects to an existing SQL Server instance  
- Supports multi‑user environments and IT‑managed deployments  
- Designed for medium to large companies  

The installer writes a registry flag (`UseSQLExpress`) that determines which connection setup page the application loads on first launch.

---

## License enforcement flow
User Launch → License Prompt → Gumroad API Validation → Local Unlock

- User enters their Gumroad license key on first launch  
- Key is validated through Gumroad’s `/v2/licenses/verify` endpoint  
- Valid keys unlock the application and store the license state locally  
- Periodic revalidation may occur (e.g., every 7 days)  
- License tier determines access to Basic, Pro, or Enterprise inventory features  

---

## Local session context
- All data is stored in SQL Server Express or Full SQL Server  
- No cloud sync, Redis, or external session store  
- Secure login using salted + hashed admin credentials  
- Fully offline operation after initial license activation  

---

## Data transfer between computers
The app includes a built‑in SQL migration tool for moving data to a new machine:

- Creates a `.bak` backup file from the old computer  
- Restores the `.bak` file on the new computer  
- Works for both SQL Express and Full SQL Server  
- Suitable for machine upgrades or office migrations  

---

## SQL connection pages
The application routes users to the correct connection setup page based on installer selection:

- `sql_connection_page.py` – SQL Express  
- `sql_server_connection_page.py` – Full SQL Server  

Both pages support:
- Connection testing  
- Credential validation  
- Database creation (if needed)  
- Secure admin login setup  

---

## Core inventory & warehouse workflow
Admin Login → Material Setup → Warehouse Setup → Inventory Transactions → Reporting

- Admin defines materials in a universal `Material_Info` schema (code, name, unit, cost, etc.)  
- Warehouses are configured in a dedicated `Warehouse` table  
- Stock levels are tracked per warehouse via `Warehouse_Inventory`  
- All movements (receipts, issues, adjustments, transfers) are logged in `Inventory_Transactions` and `Warehouse_Transfers`  
- Inventory can be filtered and reported by material, warehouse, date range, and transaction type  

---

## File storage & export
All exports are stored locally under a user‑selectable root folder, for example:

- `\Inventory_Exports\Reports\` – inventory, valuation, and transaction reports  
- `\Inventory_Exports\Backups\` – generated `.bak` files and optional CSV/Excel dumps  

Paths are configurable from the admin settings screen and are never synced to any external service.
