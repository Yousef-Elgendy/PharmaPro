# MVP Scope

The MVP must deliver the complete core workflow: **Supplier -> Stock-in (batch) -> Inventory -> Sale -> Dashboard**, secured by roles.

## In Scope (MVP)
| Module | Included |
|--------|----------|
| Auth | Login/logout, JWT, role-based access (3 roles) |
| Users | Admin creates/edits/deactivates users, assigns role |
| Catalog | Products and Categories CRUD, unique SKU, image URL, search and category filter |
| Suppliers | Supplier CRUD |
| Inventory | Stock-in with batches (number + expiry), stock adjustments with reason, movement log, stock by batch |
| POS | Search by name/barcode, cart, quantity validation, FEFO deduction, atomic stock update, receipt summary |
| Dashboard | Product counts, total sales, low-stock alerts |
| Quality | xUnit tests for core business rules, Swagger docs, seed data |

## Should Have (include if time allows)
Near-expiry alerts on dashboard, sales history, pagination, password reset, role-adaptive dashboard.

## Could Have / Deferred
Void sale, best-selling products chart, supplier stock-in history view, export to PDF/Excel, barcode scanner hardware integration, Arabic/English language switch.

## Out of Scope
Online ordering, customers module, payment gateway, multi-branch, prescriptions, insurance, purchase orders to suppliers.

## Priority Order (build sequence)
1. Auth and roles
2. Catalog (categories, products)
3. Suppliers
4. Inventory (batches, movements)
5. POS and sales
6. Dashboard
7. Tests, polish, documentation

## Definition of Done (MVP)
- All **Must** requirements in `functional-requirements.md` are implemented.
- All business rules marked [T] have passing xUnit tests.
- A full demo scenario works end to end: create product -> receive batch -> sell -> stock drops -> low-stock alert appears.
- Code merged to `main` through reviewed Pull Requests.
