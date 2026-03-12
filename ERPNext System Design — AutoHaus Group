ERPNext System Design — AutoHaus Group
Version: v15 (self-hosted, on-premise) | Date: March 2026
Part 1: Data Model Design (Standard Doctypes - may be required)
Doctype
Purpose
Company
Single record for the legal entity covering both dealerships
Warehouse
One or multiple per dealership for physical stock separation
Cost Center
One per dealership for P&L reporting
Vehicle (or Asset)
Primary vehicle master (Asset if maintenance required)
Customer
Buyer management
Supplier
Manufacturer
Purchase Order
Raised per vehicle order toward the manufacturer
Purchase Receipt
Raised when vehicle arrives at dealership
Sales Order/Sales Invoice
Raised when customer commits to a vehicle




Note on Vehicle vs Item:
Vehicle doctype will be customized with custom fields same as the required master.
Each Vehicle record represents one physical vehicle.
Items and Serial Nos will be used for parts and accessories.
Custom Doctypes
Vehicle Master — Sales staff select model, color, and options/packages.
Purchase Order — Tracks one order list with SAP: order status (Pending / Transmitted / Confirmed), SAP order reference
Trade-in Vehicle — To be discussed

Entity Relationships
Company
├── Warehouse (City A) ── Cost Center (City A)
└── Warehouse (City B) ── Cost Center (City B)

Vehicle Configuration → Manufacturer Order ↔ SAP
    └──────────→ Vehicle
             ├── Purchase Order → Supplier
             ├── Purchase Receipt
             ├── Sales Order → Customer → Contact/Address
             └── Sales Invoice


Two-Dealership Setup
Both dealerships share one Company. Separation is via Warehouses (stock) and Cost Centers (financials). User Permissions on the Warehouse field restrict sales staff to their own dealership. The accountant and management see both. Unified inventory view is available through standard stock reports filtered by warehouse or company-wide.
Part 2: Integration Architecture
Architecture
ERPNext (Custom App)
 ├── Outbound queue → REST API → SAP (vehicle creations, order creations so on ....)
 ├── Inbound webhook ← REST API ← SAP (order confirmations)

No separate middleware server is required. All integration logic lives within the ERPNext custom app as Frappe background jobs and whitelisted API endpoints.


Method Choice
REST API: Calls to i SAP, instant notification to Sales Staff/Purchase Staff when orders are confirmed in SAP.

Data Flows
Order (ERPNext → SAP): Sales staff submit a Vehicle Configuration → Manufacturer Order created (Pending) → Frappe scheduler picks it up every 5 minutes → REST call to SAP → on success, status changes to Pending Confirmation and SAP reference stored.
Confirmation (SAP → ERPNext): When order confirmed in SAP → status changes to Confirmed → sales person notified.

Error Handling
Error Code
Response
Error 402
SAP REST for timeout






Part 3: Assumptions & Open Questions
Assumptions
Single legal entity — one ERPNext Company is sufficient, no inter-company transactions needed.
Vehicle catalogue (models, colours, option codes) is stable enough to maintain manually; updated on new model years.
Manufacturer's REST API is documented and a sandbox environment is available for testing.
Single local currency throughout process
Dedicated member is available, who can take decisions on behalt of Autohaus
The training model is train the trainer. Training will be provided to single erp champion
Questions for the Customer
Per day transactions
No if users users required for training
Budget planned for complete implementation and training
Timeline/deadline for complete implementation and training
Support after Go-live support required?

Out of Scope
Workshop/Service module — not in scope.
CRM/Lead pipeline — not in scope
SAP RFC channel — REST API.
HR & Payroll — not in scope
Multi-currency — single currency assumed
End of Document
