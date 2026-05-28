# Inventory App — Unified SQL Express & SQL Server Edition  
## GitHub Release Documentation — Version 2.0.0

This release delivers the fully unified Inventory App architecture, combining all features, license tiers, and database modes into a single Windows `.exe`. The application now includes enhanced RBAC controls, improved admin onboarding, multi‑resolution icon support, and a modernized SQL workflow.

All license tiers (Basic, Pro, Enterprise) are included in one unified application, with access determined by the user’s Gumroad license key.

---

## Included in This Release
- Basic Plan  
- Pro Plan  
- Enterprise Plan   
- Unified SQL Express + SQL Server architecture  
- Multi‑warehouse support  
- Purchase orders (full lifecycle)  
- Inventory transactions (receipts, issues, adjustments, transfers)  
- Centralized RBAC enforcement  
- Multi‑resolution `.ico` for crisp Windows display  
- One installer, one app, one onboarding flow  

---

## Plan Descriptions

### Basic Plan
Provides essential inventory management features for individuals or small teams.  
Includes core material tracking, single‑warehouse support, and standard reporting.  
Ideal for users who need a simple, reliable inventory foundation.

---

### Pro Plan
Expands on the Basic plan with enhanced tools and deeper reporting.  
Designed for growing teams that manage multiple materials and require more control.  
Includes multi‑warehouse support, transaction history, and valuation reporting.

---

### Enterprise Plan
Unlocks the full capabilities of the system, including everything in Pro plus advanced administrative controls.  
Required for organizations with multiple administrators or complex warehouse operations.  
Includes:

- Custom reporting templates  
- Priority support  
- Advanced warehouse transfer tools  
- Additional administrative controls  

---

## Role‑Based Access Control (RBAC)

### Global Admin
- Full system access  
- Can configure warehouses, materials, suppliers, and system settings  
- Can manage other admins (if license tier allows)  

### Local Admin
- Restricted to operational modules  
- Cannot modify global system settings  
- Redirected to login after registration (no auto‑session creation)  

### Enforcement
- Centralized in `Admin_Interface.py`  
- UI dynamically adapts based on role  
- Feature access validated before loading any module  
- Prevents unauthorized navigation or direct file access  

---

## License Activation
A valid Stripe subscription is required to use this application.

• On first launch, the app checks your subscription status securely through Stripe.
• If your subscription is active, the app unlocks full access.
• If your subscription is canceled, expired, or unpaid, access is restricted.
• Internet is required only during subscription verification and plan changes.
• All billing and upgrades are handled through Stripe’s secure checkout.

---

## Database Architecture
The Inventory App supports two database modes, selected during installation:

### SQL Express (Local Database — Recommended for 1–5 users)
- Automatically installed and configured by the installer  
- Ideal for individuals, small teams, and single‑machine setups  
- Fully offline and self‑contained  

### SQL Server (Remote or On‑Prem Server)
- Connect to an existing SQL Server instance  
- Supports multi‑user environments and IT‑managed deployments  
- Ideal for medium‑to‑large teams or companies with dedicated servers  

Both modes use the same unified application and feature set.

---

## Core Inventory Workflow
Admin Login → Material Setup → Warehouse Setup → Inventory Transactions → Reporting

- Universal `Material_Info` schema  
- Multi‑warehouse stock tracking  
- Transaction logging with reason codes and timestamps  
- Purchase order lifecycle: Pending → Ordered → Received → Closed  
- Real‑time stock updates  
- Excel/PDF reporting  

---

## Multi‑Resolution Icon Support
The application now includes a professional multi‑size `.ico`:

- 256×256  
- 128×128  
- 64×64  
- 48×48  
- 32×32  
- 24×24  
- 16×16  

Ensures crisp rendering across all Windows views (Taskbar, Explorer, Start Menu).

---

## Stability
This version is the current stable build distributed through the updater and serves as the foundation for all future updates.  
All modules, SQL workflows, and RBAC systems have been consolidated into a unified, maintainable architecture.

