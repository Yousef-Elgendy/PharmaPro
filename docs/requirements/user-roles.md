# User Roles & Permissions

## 1. User Roles

| Role | Description |
|---|---|
| **Administrator** | Manages users, products, categories, suppliers, sales, inventory, and reports. |
| **Sales Clerk (Pharmacist)** | Handles sales and browses available products. |
| **Stock Manager** | Records stock-in operations, manages batches, and performs stock adjustments. |

## 2. Role Responsibilities

- **Administrator:** Has full system access, manages user accounts and system data, and views all reports.
- **Sales Clerk:** Searches for products, checks prices and availability, and processes customer sales. Cannot manage users or view supplier costs.
- **Stock Manager:** Records received stock, manages batch and expiry information, and maintains accurate stock quantities. Cannot process sales.

## 3. Permission Matrix

**Legend:** C = Create, R = Read, U = Update, D = Delete, X = No Access.

| Feature | Administrator | Sales Clerk | Stock Manager |
|---|---|---|---|
| Login / Logout | Yes | Yes | Yes |
| Change Own Password | Yes | Yes | Yes |
| User Management | CRUD | X | X |
| Products | CRUD | R | R |
| Categories | CRUD | R | R |
| Suppliers | CRUD | X | R |
| Stock-in | C/R | X | C/R |
| Stock Adjustments | C/R | X | C/R |
| Stock Movement Log | R | X | R |
| Batches & Expiry | R | R (available stock only) | R |
| Create Sales (POS) | C/R | C/R | X |
| Sales History | R (all sales) | R (own sales) | X |
| Cancel / Void Sales | Yes | X | X |
| Dashboard | Full | Limited | Limited |
| Reports | R | X | X |

## 4. Access Control Rules

1. Role-based access control (RBAC) must be enforced on every API endpoint, not only through the user interface.
2. Access is denied by default unless explicitly granted to a role.
3. Each user must have exactly one role in the MVP.
4. Sales Clerks must not have access to supplier purchase costs or product cost prices.
5. Deactivated users cannot log in or access protected system resources.