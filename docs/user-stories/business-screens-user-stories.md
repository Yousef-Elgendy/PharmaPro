# User Stories: Business Screens

**Format:** As a [role], I want [goal], so that [benefit].

**Priority:** M = Must, S = Should, C = Could.

Each user story is linked to its related Functional Requirements.

## 1. Products & Categories

### US-20: Browse Products (M) — FR-PRD-05, FR-PRD-06

As any user, I want to browse medicines with their images, names, categories, prices, and available quantities so that I can quickly find the products I need.

**Acceptance Criteria**
- Products can be displayed in card or table view.
- Users can search by name, SKU, or barcode.
- Users can filter products by category.
- Missing or broken images display a placeholder.
- Out-of-stock products are clearly marked.
- Pagination is supported according to the MVP priority.

### US-21: Add Product (M) — FR-PRD-01, FR-PRD-02

As an Administrator, I want to add a medicine with its name, category, SKU, barcode, selling price, image URL, and reorder level so that it can be stocked and sold.

**Acceptance Criteria**
- Required fields are validated.
- Selling price must be greater than zero.
- Duplicate SKUs are rejected with the message "SKU already exists".
- An image preview is displayed when a valid image URL is provided.

### US-22: Edit Product (M) — FR-PRD-03

As an Administrator, I want to edit medicine details so that product information and prices remain accurate.

**Acceptance Criteria**
- Updated product details are saved successfully.
- Price changes affect future sales only; previous sales retain their original unit prices.
- A success notification is displayed.

### US-23: Delete / Deactivate Product (M) — FR-PRD-04

As an Administrator, I want to remove or deactivate a medicine so that the product catalog stays accurate.

**Acceptance Criteria**
- A product without stock or sales history can be deleted after confirmation.
- A product with stock or sales history cannot be deleted and must be deactivated instead.
- An explanatory message is displayed when deletion is not allowed.

### US-24: Manage Categories (M) — FR-CAT-01, FR-CAT-02

As an Administrator, I want to add, rename, and delete categories so that medicines remain well organized.

**Acceptance Criteria**
- The Administrator can create and update categories.
- Deleting a category that contains products is blocked with a clear message.

## 2. Suppliers

### US-25: View Suppliers (M) — FR-SUP-01, FR-SUP-03

As an Administrator or Stock Manager, I want to view the list of suppliers so that I can select the correct supplier when receiving stock.

**Acceptance Criteria**
- The list displays company name, contact person, phone, and email.
- Users can search suppliers by name.

### US-26: Add / Edit Supplier (M) — FR-SUP-01

As an Administrator, I want to add and edit supplier details so that supplier records remain complete and accurate.

**Acceptance Criteria**
- Company name is required.
- Email and phone formats are validated.
- A success notification is displayed after saving.

### US-27: Delete / Deactivate Supplier (M) — FR-SUP-02

As an Administrator, I want to delete unused suppliers and deactivate suppliers with stock-in history so that supplier records remain accurate.

**Acceptance Criteria**
- A confirmation dialog is displayed before deletion.
- A supplier with stock-in records cannot be deleted and must be deactivated instead.
- An explanatory message is displayed when deletion is not allowed.

### US-28: Supplier Stock-in History (C) — FR-SUP-04

As an Administrator, I want to view all stock received from a supplier so that I can review the supplier's delivery history.

**Acceptance Criteria**
- The history displays stock-in records with dates, products, and quantities.

## 3. Stock Management

### US-30: Receive Stock (M) — FR-INV-01 to FR-INV-04

As a Stock Manager, I want to record an incoming delivery with a supplier and multiple products, each with a batch number, expiry date, and quantity, so that inventory remains accurate and traceable.

**Acceptance Criteria**
- The Stock Manager can add multiple product batches to one stock-in operation.
- Expiry dates must be in the future.
- Quantity must be a positive integer.
- Duplicate batch numbers for the same product are rejected.
- Stock-in is saved as one database transaction.
- Product stock increases after successful saving.
- A stock movement is recorded for each stock change.
- A confirmation summary is displayed after successful saving.

### US-31: View Stock by Batch (M) — FR-INV-08, FR-INV-10

As a Stock Manager, I want to view each product's batches with their quantities and expiry dates so that I can track inventory accurately.

**Acceptance Criteria**
- Batches are sorted by expiry date.
- Expired batches are clearly marked in red.
- Expired batches are excluded from available stock totals.

### US-32: Adjust Stock (M) — FR-INV-05

As a Stock Manager, I want to adjust stock for damage, expiry write-off, or count correction so that system quantities match actual inventory.

**Acceptance Criteria**
- An adjustment reason is mandatory.
- Stock quantity cannot become negative.
- Every adjustment is recorded in the stock movement log.

### US-33: View Stock Movement Log (M) — FR-INV-06, FR-INV-07

As a Stock Manager or Administrator, I want to view a log of stock changes so that every inventory movement is traceable.

**Acceptance Criteria**
- The log displays date, product, batch, movement type, quantity change, user, and reference.
- Movement types include Stock-in, Sale, and Adjustment.
- Void movements are recorded when the sale-void feature is implemented.
- Users can filter movements by product, type, user, and date range.

### US-34: Expiry Awareness (S) — FR-INV-09

As a Stock Manager, I want expired and near-expiry batches to be highlighted so that I can take action before products become unsuitable for sale.

**Acceptance Criteria**
- Batches expiring within 30 days are highlighted in amber.
- Expired batches are highlighted in red.
- The batch number, product, expiry date, and quantity are displayed.

## 4. Point of Sale (POS)

### US-40: Search and Add to Cart (M) — FR-POS-01, FR-POS-02

As a Sales Clerk, I want to search for medicines by name or barcode and add them to the cart so that I can serve customers quickly.

**Acceptance Criteria**
- Search results display product image, price, and available quantity.
- Pressing Enter on an exact barcode match adds the product to the cart.
- Out-of-stock products cannot be added.
- Search results should appear in under one second under the defined performance conditions.
- Expired batches are excluded from available quantities.

### US-41: Manage Cart (M) — FR-POS-02, FR-POS-03

As a Sales Clerk, I want to change product quantities and remove items from the cart so that the invoice remains accurate.

**Acceptance Criteria**
- Line totals and the grand total update immediately when quantities change.
- Quantity cannot be zero or negative.
- Removing an item updates the grand total.

### US-42: Stock Validation (M) — FR-POS-04, FR-POS-05

As a Sales Clerk, I want the system to prevent me from selling more than the available stock so that inventory is never oversold.

**Acceptance Criteria**
- The system prevents quantities exceeding available non-expired stock.
- An attempt to exceed available stock displays a message such as "Only X units available".
- An empty cart disables the Confirm button.
- Stock validation is enforced on the server, not only in the UI.

### US-43: Confirm Sale (M) — FR-POS-06 to FR-POS-08

As a Sales Clerk, I want to confirm a sale so that the invoice is saved and stock is deducted immediately.

**Acceptance Criteria**
- Sale confirmation and stock deduction execute within one database transaction.
- Stock is deducted using FEFO (First Expired, First Out).
- The unit price at the time of sale is saved with each sale item.
- If any item fails validation or stock deduction, the entire transaction is rolled back.
- A clear error message explains why the sale failed.

### US-44: Receipt (M) — FR-POS-09

As a Sales Clerk, I want to view a receipt summary after completing a sale so that I can provide the transaction details to the customer.

**Acceptance Criteria**
- The receipt displays invoice number, date, clerk, items, quantities, unit prices, and total.
- A "New Sale" button is available.
- A print option may be provided if included in the MVP implementation.

### US-45: Sales History (S) — FR-POS-10

As a Sales Clerk, I want to view my previous sales, while an Administrator can view all sales, so that transactions can be reviewed.

**Acceptance Criteria**
- Sales can be filtered by date.
- Sales Clerks can view only their own sales.
- Administrators can view all sales.

### US-46: Void Sale (C) — FR-POS-11

As an Administrator, I want to void a sale so that transaction mistakes can be corrected.

**Acceptance Criteria**
- Voiding requires a reason and confirmation.
- Stock is restored to the appropriate batches.
- A stock movement is recorded for the void operation.

## 5. Cross-Screen Acceptance Criteria

- All forms must follow UX-03 for inline validation and UX-04 for confirmation of destructive actions.
- Every list must provide loading, empty, and error states.
- Every screen must be usable at a width of 360px and support keyboard navigation.
- Server-side validation errors must be displayed to users in clear, understandable language.