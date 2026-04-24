# Inventory App — Unified SQL Express & SQL Server Edition
## Initial GitHub Release — Version 1.0.0

This release introduces the fully unified version of the Inventory App, combining all features and license tiers into a single Windows `.exe` application. The app supports both SQL Express and SQL Server, selected during installation, eliminating the need for separate builds or database versions.

All license tiers (Basic, Pro, Enterprise) are included in one unified application, with access determined by the user’s Gumroad license key.

---

## Included in This Release
- Basic Plan  
- Pro Plan  
- Enterprise Plan  
- Admin Add‑on  
- Unified SQL Express + SQL Server architecture  
- Multi‑warehouse support  
- Inventory transactions (receipts, issues, adjustments, transfers)  
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
Unlocks the full capabilities of the system, including everything in Pro plus advanced controls and administrative features.  
Required for organizations with multiple administrators or complex warehouse operations.  
Includes:

- Custom reporting templates  
- Priority support  
- Advanced warehouse transfer tools  
- Additional administrative controls  

---

### Admin Add‑on
A supplemental license for each additional administrator beyond the main admin included with the Enterprise plan.  
Ensures secure, individual admin access without shared credentials.  
Cannot function alone — requires an active Basic, Pro, or Enterprise plan.

---

## License Activation
This app requires a valid Gumroad license key to unlock full functionality.

- You will be prompted to enter your license key on first launch.  
- The app verifies your key securely via Gumroad’s API.  
- If the license is invalid or revoked, access will be restricted.  
- Internet access is required for initial license validation.

After activation, the app operates fully offline.

---

## Database
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

## Stability
This version is the current stable build distributed through the updater and serves as the foundation for all future updates.
