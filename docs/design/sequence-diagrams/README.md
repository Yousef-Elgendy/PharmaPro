# Sequence Diagrams

Sequence diagrams for the main workflows of the Pharmacy Sales & Inventory Management System. Each diagram follows one request from the user interface down to the database and back.

## Index

| ID | Module | Diagram | Actor | Source | SVG | PNG |
|----|--------|---------|-------|--------|-----|-----|
| SD-01 | Authentication | Login | Any user | [src](src/01-auth-login.mmd) | [svg](svg/01-auth-login.svg) | [png](png/01-auth-login.png) |
| SD-02 | Catalog | Add Product (unique SKU) | Administrator | [src](src/02-catalog-add-product.mmd) | [svg](svg/02-catalog-add-product.svg) | [png](png/02-catalog-add-product.png) |
| SD-03 | Inventory | Receive Stock (Stock-in with batches) | Stock Manager | [src](src/03-inventory-receive-stock.mmd) | [svg](svg/03-inventory-receive-stock.svg) | [png](png/03-inventory-receive-stock.png) |
| SD-04 | Inventory | Adjust Stock | Stock Manager | [src](src/04-inventory-adjust-stock.mmd) | [svg](svg/04-inventory-adjust-stock.svg) | [png](png/04-inventory-adjust-stock.png) |
| SD-05 | Sales | Confirm Sale (POS with FEFO) | Sales Clerk | [src](src/05-sales-confirm-sale.mmd) | [svg](svg/05-sales-confirm-sale.svg) | [png](png/05-sales-confirm-sale.png) |
| SD-06 | Sales | Void Sale | Administrator | [src](src/06-sales-void-sale.mmd) | [svg](svg/06-sales-void-sale.svg) | [png](png/06-sales-void-sale.png) |
| SD-07 | Dashboard | View Dashboard | Any user | [src](src/07-dashboard-view-dashboard.mmd) | [svg](svg/07-dashboard-view-dashboard.svg) | [png](png/07-dashboard-view-dashboard.png) |

## What each diagram shows

| ID | Key behaviour | Requirements | Business rules | User stories |
|----|---------------|--------------|----------------|--------------|
| SD-01 | Checks `IsActive` and password hash, returns a JWT with user id and role, or 401 | FR-AUTH-01 to 04 | BR-24 | US-01 |
| SD-02 | Validates fields, checks category exists and SKU/barcode unused, inserts the product; the unique index guards against concurrent duplicates | FR-PRD-01, FR-PRD-02 | BR-01, BR-02, BR-03 | US-21 |
| SD-03 | Validates expiry date, quantity and unique batch number, then saves StockIn, Batches and StockMovements in one transaction | FR-INV-01 to 04, FR-INV-06 | BR-06 to BR-09, BR-11 | US-30 |
| SD-04 | Requires a reason, rejects negative stock, updates the batch and logs an Adjustment movement in one transaction | FR-INV-05, FR-INV-06 | BR-10 to BR-12 | US-32 |
| SD-05 | Loads non-expired batches in FEFO order, rolls back if stock is insufficient, otherwise saves the sale with a price snapshot, updates batches and logs movements atomically | FR-POS-04 to 08 | BR-13 to BR-20 | US-43 |
| SD-06 | Administrator only; rejects an already voided sale, restores quantities to the original batches and logs reversing Void movements | FR-POS-11 | BR-21 | US-46 |
| SD-07 | Collects counts, sales totals, low-stock items and expiry alerts, then filters the widgets by role; voided sales are excluded from totals | FR-DSH-01 to 04, FR-DSH-06 | BR-26, BR-27 | US-06 to US-10 |

## Participants and notation

- **Actor**: the user role performing the action.
- **Frontend**: HTML/CSS/JavaScript pages calling the API with `fetch`.
- **API**: ASP.NET Core controller (authentication, role authorization, request mapping).
- **Service**: business-rule layer (validation, FEFO, transactions).
- **SQL Server**: relational database accessed through Entity Framework Core.
- Solid arrows are requests, dashed arrows are responses, `alt` blocks show failure versus success paths, notes state the important rule or guarantee.
- Diagram numbers (`autonumber`) are step numbers inside one diagram, not diagram IDs.

## Folder structure

```
sequence-diagrams/
├── README.md
├── src/    Mermaid sources (.mmd), the editable originals
├── svg/    vector exports
└── png/    raster exports (2x scale)
```

File names follow `NN-module-action`, and the number matches the diagram ID (`01-auth-login` is SD-01).

## Viewing and editing

- **GitHub**: Mermaid renders natively. Paste the contents of a `.mmd` file (without the `---` title header if you prefer) inside a ```` ```mermaid ```` block in any Markdown file.
- **draw.io**: Arrange > Insert > Advanced > Mermaid, paste the source.
- **Mermaid Live Editor**: paste the source to edit and export.
- **Regenerate the exports** (requires `@mermaid-js/mermaid-cli`):

```bash
mmdc -i src/01-auth-login.mmd -o svg/01-auth-login.svg -b white
mmdc -i src/01-auth-login.mmd -o png/01-auth-login.png -b white -s 2
```

## Consistency with other design documents

- Tables and columns match `design/initial-data-model.md` and the ERD (for example `Batch.QuantityRemaining`, `StockMovement` types, `Sale.VoidedAt`).
- Transactions in SD-03 to SD-06 match section 5 of the data model.
- Roles and permissions match `requirements/user-roles.md`.
- The earlier chat versions of these diagrams were numbered 1 to 5 in a different order; the IDs above are the final numbering.
