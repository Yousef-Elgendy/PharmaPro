# Business Rules (BRs)

Each rule must be enforced in the backend service layer and covered by at least one xUnit test where marked **[T]**.

## Catalog
| ID | Rule | Test |
|----|------|:----:|
| BR-01 | Product SKU must be unique across all products. | T |
| BR-02 | Product price must be greater than zero. | T |
| BR-03 | Product name and category are required. | T |
| BR-04 | A category that has products cannot be deleted. | T |
| BR-05 | A product with stock or sales history cannot be deleted; it can only be deactivated. | T |

## Inventory
| ID | Rule | Test |
|----|------|:----:|
| BR-06 | Every stock-in line requires a batch number and an expiry date. | T |
| BR-07 | Expiry date of a received batch must be in the future. | T |
| BR-08 | Received quantity must be a positive integer. | T |
| BR-09 | Batch numbers must be unique per product (same product cannot have two batches with the same number). | T |
| BR-10 | Stock quantity can never become negative. | T |
| BR-11 | Every stock change (stock-in, sale, adjustment, void) must create a Stock Movement record. | T |
| BR-12 | A stock adjustment requires a reason. | T |
| BR-13 | Expired batches are excluded from available stock and cannot be sold. | T |
| BR-14 | Stock is consumed from the earliest-expiring batch first (FEFO). | T |

## Sales
| ID | Rule | Test |
|----|------|:----:|
| BR-15 | A sale must contain at least one valid item. | T |
| BR-16 | Sale quantity must be a positive integer and cannot exceed available non-expired stock. | T |
| BR-17 | Unit price and line total must be positive. | T |
| BR-18 | The sale item stores the unit price at the time of sale; later price changes do not affect past sales. | T |
| BR-19 | Sale total equals the sum of (quantity x unit price) of all items. | T |
| BR-20 | Confirming a sale deducts stock immediately and atomically; if any step fails, nothing is saved. | T |
| BR-21 | Confirmed sales cannot be edited; they can only be voided by an Administrator. | |

## Users & Security
| ID | Rule | Test |
|----|------|:----:|
| BR-22 | Username/email must be unique. | T |
| BR-23 | Each user has exactly one role. | |
| BR-24 | Deactivated users cannot log in. | T |
| BR-25 | Users with sales or stock history cannot be deleted, only deactivated. | |

## Dashboard
| ID | Rule | Test |
|----|------|:----:|
| BR-26 | A product is low-stock when available quantity <= its reorder level. | T |
| BR-27 | A batch is near-expiry when its expiry date is within 30 days (configurable). | T |
