# Wireframes

Low-fidelity desktop wireframes (1280 × 720 px) for the Pharmacy Sales & Inventory Management System. They cover the screens defined in `docs/user-stories/screen-inventory.md`.

## Folder Structure

```text
wireframes/
├── README.md
├── pharmacy-wireframes.pdf
├── svg/
│   └── 11 editable SVG files
└── png/
    └── 11 PNG preview files
```

## Screens

| # | File Name | Screen ID | Screen | Description |
|---|-----------|-----------|--------|-------------|
| 01 | `01-login` | SCR-01 | Login | Sign-in card with username/email, password, error message, and Sign in button. |
| 02 | `02-dashboard` | SCR-02 | Dashboard | Product, category, supplier, and sales stat cards, total sales (today / month / all time), low-stock items, and near-expiry/expired batches. |
| 03 | `03-users` | SCR-03, SCR-04 | Users | Searchable users list with role filter and status, plus the Add / Edit User form. |
| 04 | `04-products` | SCR-06 | Products | Medicine cards with image placeholder, category, price, and stock status (in stock, low, out of stock), search, category filter, and pagination. |
| 05 | `05-product-form-categories` | SCR-07, SCR-08 | Product Form and Categories | Add / Edit Product form (unique SKU, barcode, price, image URL, reorder level) with image preview, and category management. |
| 06 | `06-suppliers` | SCR-09, SCR-10 | Suppliers | Suppliers list with search and the Add / Edit Supplier form. |
| 07 | `07-stock-in` | SCR-11 | Stock-in | Receive a delivery: supplier, reference, date, and batch lines (batch number, expiry date, quantity, cost). |
| 08 | `08-inventory-adjustment` | SCR-12, SCR-13 | Inventory and Adjustment | Stock by batch with expiry status (OK, near expiry, expired) and the Adjust Stock form with a mandatory reason. |
| 09 | `09-movement-log` | SCR-14 | Movement Log | Filterable log of every stock change (date, product, batch, type, quantity, user, reference, reason). |
| 10 | `10-pos` | SCR-15 | POS | Medicine search by name/barcode, product cards with available quantity, cart with quantities and totals, and Confirm Sale. |
| 11 | `11-receipt-sales-history` | SCR-16, SCR-17 | Receipt and Sales History | Sales history with date filters and the sale receipt with Print, New Sale, and Void Sale actions. |

**Not included:** SCR-05 (Profile / Change Password) and SCR-18 (Access Denied / 404).

## Export Formats

| Format | Location | Details |
|--------|----------|---------|
| SVG | `svg/NN-name.svg` | Editable vector files at 1280 × 720 px, with `viewBox="0 0 1280 720"`. Elements are represented using SVG shapes and text. |
| PNG | `png/NN-name.png` | 1280 × 720 px previews for quick viewing on GitHub. |
| PDF | `pharmacy-wireframes.pdf` | All 11 screens, one per page, with 1280 × 720 px page dimensions, selectable text, and a bookmark for each screen. |

## Import SVG Files into Figma

1. Open a Figma Design file and navigate to the page where you want to place the screens.
2. Select the SVG files from the `svg/` folder and drag them onto the Figma canvas. Alternatively, use **File > Place image...** (Shift + Cmd/Ctrl + K).
3. Each SVG is imported as an editable vector group containing shapes, text, lines, and other elements.
4. Optionally, select an imported group and use **Frame selection** (Cmd/Ctrl + Alt + G) to turn it into a frame. Rename it to match the file name and use **Tidy up** to arrange the frames.
5. The text uses the Inter font. If Figma reports a missing font, set the text layers to Inter.

**Notes:**

- Figma does not recreate Auto Layout from SVG; elements retain their original absolute positions.
- Dropdown arrows are represented by vector chevrons.
- Date fields use the placeholder `mm/dd/yyyy`.
- Dashed placeholder boxes retain their dashed borders.

## Navigation and User Flows

User flows and navigation flow diagrams are not included in these wireframes. Navigation is represented by the sidebar visible on every screen except Login.

## Design Coverage

The wireframes provide a visual reference for the main system screens and their layouts, including authentication, dashboard, user management, product catalog, suppliers, inventory operations, POS, and sales history.

They are intended to guide UI implementation and maintain consistency between the screen designs and the documented requirements.

