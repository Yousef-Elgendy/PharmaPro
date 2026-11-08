# Functional Requirements

**Priority Levels:**
- **M (Must):** Essential requirements for the Minimum Viable Product (MVP).
- **S (Should):** Important requirements that can be deferred if necessary.
- **C (Could):** Optional features that may be implemented in future releases.

## 1. Authentication & Authorization

| ID | Requirement | Pri |
|---|---|:---:|
| FR-AUTH-01 | The system shall allow users to log in using their username/email and password. | M |
| FR-AUTH-02 | The system shall issue an authentication token/session upon successful login and expire it according to the configured expiration and inactivity policy. | M |
| FR-AUTH-03 | The system shall restrict access to every endpoint and page based on the user's assigned role (see user-roles.md). | M |
| FR-AUTH-04 | The system shall securely hash and store user passwords and never store them in plain text. | M |
| FR-AUTH-05 | Users shall be able to log out and change their own passwords. | S |

## 2. User Management

| ID | Requirement | Pri |
|---|---|:---:|
| FR-USR-01 | Admin shall be able to create users with a name, username/email, password, and role. | M |
| FR-USR-02 | Admin shall be able to view a list of users and search/filter them by role or status. | M |
| FR-USR-03 | Admin shall be able to update user details and change a user's role. | M |
| FR-USR-04 | Admin shall be able to deactivate/reactivate users instead of deleting users who have historical records. | M |
| FR-USR-05 | Admin shall be able to reset a user's password. | S |
| FR-USR-06 | The system shall prevent an Admin from deactivating their own account. | S |

## 3. Products & Categories

| ID | Requirement | Pri |
|---|---|:---:|
| FR-CAT-01 | Admin shall be able to create, view, update, and delete categories (e.g., Painkillers, Antibiotics). | M |
| FR-CAT-02 | A category containing products shall not be deletable unless its products are reassigned first. | M |
| FR-PRD-01 | Admin shall be able to create a product with the following details: name, category, SKU, barcode, selling price, image URL, and reorder level. | M |
| FR-PRD-02 | The system shall reject a product whose SKU already exists. | M |
| FR-PRD-03 | Admin shall be able to update product details. | M |
| FR-PRD-04 | Admin shall be able to delete a product only if it has no stock or sales history; otherwise, the product must be deactivated. | M |
| FR-PRD-05 | All authorized roles shall be able to view the product list with image, name, category, price, and available quantity. | M |
| FR-PRD-06 | Users shall be able to search for products by name, SKU, or barcode and filter them by category. | M |
| FR-PRD-07 | The product list shall support pagination. | S |
| FR-PRD-08 | The UI shall display a placeholder image when a product image URL is missing or broken. | S |

## 4. Suppliers

| ID | Requirement | Pri |
|---|---|:---:|
| FR-SUP-01 | Admin shall be able to create, view, update, and delete suppliers (company name, contact person, phone, email, and address). | M |
| FR-SUP-02 | A supplier linked to stock-in records shall not be deletable; it may be deactivated instead. | M |
| FR-SUP-03 | Users shall be able to search suppliers by name. | S |
| FR-SUP-04 | The system shall display the stock-in history of each supplier. | C |

## 5. Inventory

| ID | Requirement | Pri |
|---|---|:---:|
| FR-INV-01 | Stock Manager shall be able to record a stock-in transaction by selecting a supplier and one or more products. | M |
| FR-INV-02 | Each received line shall include a batch number, expiry date, quantity, and optionally a cost price. | M |
| FR-INV-03 | The system shall increase the product's stock quantity by the received batch quantity. | M |
| FR-INV-04 | The system shall reject batches with an expiry date in the past or a non-positive quantity. | M |
| FR-INV-05 | Stock Manager shall be able to record stock adjustments (damage, expiry write-off, or count correction) with a mandatory reason. | M |
| FR-INV-06 | Every stock change shall create a Stock Movement record containing the movement type, product, batch, quantity, user, date, and reference. | M |
| FR-INV-07 | Authorized users shall be able to view the stock movement log and filter it by product, type, user, and date. | M |
| FR-INV-08 | The system shall display each product's stock broken down by batch, including expiry dates. | M |
| FR-INV-09 | The system shall flag batches that are expired or near expiry (30 days by default). | S |
| FR-INV-10 | The system shall calculate available stock based on the quantities of non-expired batches. | M |

## 6. Sales / POS

| ID | Requirement | Pri |
|---|---|:---:|
| FR-POS-01 | Sales Clerk shall be able to search for a medicine by name or barcode and view its image, price, and available quantity. | M |
| FR-POS-02 | The clerk shall be able to add products to a cart, change quantities, and remove items. | M |
| FR-POS-03 | The system shall automatically calculate line totals and the invoice total. | M |
| FR-POS-04 | The system shall prevent sales quantities from exceeding available non-expired stock, with validation enforced by the backend. | M |
| FR-POS-05 | The system shall reject a sale with no items or with non-positive prices or quantities. | M |
| FR-POS-06 | Upon confirmation, the system shall save the sale and its items and deduct stock immediately within a single database transaction. | M |
| FR-POS-07 | The system shall deduct stock from the earliest-expiring non-expired batch first (FEFO). | M |
| FR-POS-08 | The system shall record the product's unit price at the time of sale in the sale item (price snapshot). | M |
| FR-POS-09 | The system shall display an invoice/receipt summary after a successful sale. | M |
| FR-POS-10 | Users shall be able to view sales history (Admin: all sales; Clerk: own sales) with date and clerk filters. | S |
| FR-POS-11 | Admin shall be able to void a sale, restoring the stock and recording the corresponding stock movement. | C |

## 7. Dashboard

| ID | Requirement | Pri |
|---|---|:---:|
| FR-DSH-01 | The dashboard shall display the total number of products, categories, and suppliers. | M |
| FR-DSH-02 | The dashboard shall display total sales amounts (today, this month, and all time). | M |
| FR-DSH-03 | The dashboard shall list low-stock items (available quantity at or below the product's reorder level). | M |
| FR-DSH-04 | The dashboard shall list near-expiry and expired batches. | S |
| FR-DSH-05 | The dashboard shall display the best-selling products. | C |
| FR-DSH-06 | Dashboard content shall adapt to the user's role and permissions. | S |