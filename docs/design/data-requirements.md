# Data Requirements

## 1. Data Needed per Module 
| Module | Entities used | Key data |
|--------|---------------|----------|
| Auth & Users | Role, User | Username/email, password hash, role, active flag, created date |
| Catalog | Category, Product | Name, category, SKU (unique), barcode, price, image URL, reorder level, active flag |
| Suppliers | Supplier | Company name, contact person, phone, email, address, active flag |
| Inventory | StockIn, Batch, StockMovement | Supplier, receiving user, date, batch number, expiry date, quantity received/remaining, cost price, movement type/reason |
| POS / Sales | Sale, SaleItem, SaleItemBatch | Invoice number, clerk, date/time, items, quantities, unit price snapshot, batches consumed, total, status |
| Dashboard | Product, Batch, Sale (read-only) | Counts, sum of sales by period, products under reorder level, batches near expiry |

## 2. Storage Requirements for Sales, Batches, and Stock Movements 
### Batches
- Each stock-in line creates one `Batch` row with `QuantityReceived` (immutable) and `QuantityRemaining` (decremented by sales/adjustments).
- Expiry date is mandatory; expired batches are retained for history but excluded from available stock.
- Batch number is unique per product.

### Sales
- A `Sale` row is created only on confirmation (cart is client-side until then).
- `SaleItem.UnitPrice` stores the price at sale time; `LineTotal` and `Sale.TotalAmount` are stored for fast reporting and must match the item sums.
- `SaleItemBatch` records exactly which batches and quantities were consumed (supports FEFO, voids, and audits).
- Sales are never hard-deleted; voiding sets `Status = Voided` and creates reversing movements.

### Stock Movements
- Append-only: rows are never updated or deleted.
- One row per batch affected, with signed `QuantityChange` (+ for stock-in/void, - for sale/write-off).
- Each row stores type, user, UTC timestamp, reference to the source record (`ReferenceType` + `ReferenceId`), and a reason (mandatory for adjustments).
- Invariant: for each batch, `QuantityReceived + SUM(QuantityChange of movements) = QuantityRemaining`.

### Transactions
- Stock-in (StockIn + Batches + Movements) and Sale confirmation (Sale + SaleItems + SaleItemBatches + Batch updates + Movements) must each run in one database transaction.

## 3. Requirements vs. Data Model Check 
| Requirement | Supported by | Status |
|-------------|--------------|:------:|
| FR-PRD-02 unique SKU | Unique index on `Product.Sku` | OK |
| FR-INV-02 batch number + expiry | `Batch.BatchNumber`, `Batch.ExpiryDate` | OK |
| FR-INV-06 / BR-11 movement log for every change | `StockMovement` | OK |
| FR-INV-10 stock = sum of non-expired batches | Computed from `Batch` | OK |
| FR-POS-07 / BR-14 FEFO | Order by `Batch.ExpiryDate`, log in `SaleItemBatch` | OK |
| FR-POS-08 / BR-18 price snapshot | `SaleItem.UnitPrice` | OK |
| BR-10 no negative stock | CHECK on `Batch.QuantityRemaining` | OK |
| BR-04 / BR-05 / FR-SUP-02 protected deletes | FK restrict + `IsActive` flags | OK |
| FR-DSH-03 low stock | `Product.ReorderLevel` vs computed stock | OK |
| FR-DSH-04 near expiry | `Batch.ExpiryDate` | OK |
| FR-POS-11 void sale | `Sale.Status` + reversing movements | OK |
| FR-USR-04 deactivate user | `User.IsActive` | OK |
| NFR-17 audit who/when | `UserId` + timestamps on StockIn, StockMovement, Sale | OK |

### Open Questions for the team
1. Should cost price be hidden from Sales Clerk at the API level (yes per user-roles.md)? Confirm during design.
2. Is one barcode per product enough, or can one product have multiple barcodes (e.g., different pack sizes)?
3. Are pack sizes (strip/box) modeled as separate products? Recommended for MVP: yes.
4. Should products have a global default near-expiry threshold or per-product? Recommended: global setting.
