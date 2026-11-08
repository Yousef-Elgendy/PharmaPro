# Non-Functional Requirements

| ID | Category | Requirement |
|----|----------|-------------|
| NFR-01 | Security | Passwords are hashed (e.g., BCrypt/ASP.NET Identity hasher). |
| NFR-02 | Security | Authentication via JWT; all endpoints except login require a valid token. |
| NFR-03 | Security | Role-based authorization enforced on the server for every endpoint. |
| NFR-04 | Security | Input validation on server side; protection against SQL injection (parameterized queries via EF Core) and XSS (output encoding). |
| NFR-05 | Security | Secrets (connection strings, JWT key) are not committed to Git. |
| NFR-06 | Performance | Product search and POS lookup respond in under 1 second for up to 10,000 products. |
| NFR-07 | Performance | Confirming a sale completes in under 2 seconds. |
| NFR-08 | Reliability | Sale confirmation and stock-in run inside database transactions (all-or-nothing). |
| NFR-09 | Data integrity | Foreign keys, unique constraints (SKU, batch per product, username), and check constraints (quantity >= 0, price > 0) are enforced at the database level. |
| NFR-10 | Usability | Responsive UI that works on desktop, tablet, and mobile widths. |
| NFR-11 | Usability | The POS flow (search -> add -> confirm) takes no more than 3 clicks per item. |
| NFR-12 | Usability | Clear error messages for business-rule violations (e.g., "Only 5 units available"). |
| NFR-13 | Usability | Consistent navigation and visual design across all pages; medicine images shown in lists and POS. |
| NFR-14 | Maintainability | Layered architecture (Controllers, Services, Repositories) with DTOs. |
| NFR-15 | Maintainability | Unit tests for all business rules marked [T]; target at least 70% coverage of the service layer. |
| NFR-16 | Portability | Runs locally with SQL Server (LocalDB/Docker) using documented setup steps. |
| NFR-17 | Auditability | Stock movements and sales record who performed the action and when (UTC timestamps). |
| NFR-18 | Compatibility | Supports the latest versions of Chrome, Edge, and Firefox. |
| NFR-19 | Documentation | API documented with Swagger/OpenAPI; README with setup and run instructions. |
| NFR-20 | Accessibility | Sufficient colour contrast, labels on form fields, keyboard-usable forms. |
