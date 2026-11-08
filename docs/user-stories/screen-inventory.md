# Screen Inventory

| ID | Screen | Roles | Module |
|---|---|---|---|
| SCR-01 | Login | All | Authentication |
| SCR-02 | Dashboard (content varies by role) | All | Dashboard |
| SCR-03 | Users List | Admin | User Management |
| SCR-04 | Add/Edit User | Admin | User Management |
| SCR-05 | Profile / Change Password | All | Authentication |
| SCR-06 | Products List (cards/table with images) | All | Catalog |
| SCR-07 | Add/Edit Product | Admin | Catalog |
| SCR-08 | Categories | All (Admin manages; others view) | Catalog |
| SCR-09 | Suppliers List | Admin, Stock Manager | Suppliers |
| SCR-10 | Add/Edit Supplier | Admin | Suppliers |
| SCR-11 | Stock-in (receive batches) | Stock Manager | Inventory |
| SCR-12 | Inventory / Stock by Batch | Admin, Stock Manager | Inventory |
| SCR-13 | Stock Adjustment | Stock Manager | Inventory |
| SCR-14 | Stock Movement Log | Admin, Stock Manager | Inventory |
| SCR-15 | POS (search and cart) | Admin, Sales Clerk | Sales |
| SCR-16 | Sale Receipt / Invoice | Admin, Sales Clerk | Sales |
| SCR-17 | Sales History | Admin (all sales), Sales Clerk (own sales) | Sales |
| SCR-18 | Access Denied | All | System |
| SCR-19 | Not Found (404) | All | System |

# Global UX Requirements

- **UX-01:** Navigation must show only the menu items permitted for the user's role.
- **UX-02:** The layout must be responsive and usable at 360px (mobile), 768px (tablet), and 1280px or wider (desktop).
- **UX-03:** Forms must display inline validation messages next to invalid fields and clear error messages for server-side validation failures.
- **UX-04:** Destructive actions, such as deleting or deactivating records, must require a confirmation dialog.
- **UX-05:** API operations must provide loading feedback. Empty lists must display helpful empty-state messages.
- **UX-06:** Successful operations and errors must provide feedback through toast notifications.
- **UX-07:** Medicine images must use lazy loading and display a placeholder when an image is missing or fails to load.
- **UX-08:** The application must use a consistent color system for primary actions, success, warnings (low stock and near expiry), and danger (expired or out-of-stock).
- **UX-09:** Tables must support search and sorting. Pagination should be implemented according to the MVP priority and requirements.

