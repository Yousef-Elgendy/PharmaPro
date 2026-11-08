# User Stories: Core Screens

**Format:** As a [role], I want [goal], so that [benefit].

**Priority:** M = Must, S = Should, C = Could.

Each user story is linked to its related Functional Requirements.

## 1. Login and Authentication

### US-01: Login (M) — FR-AUTH-01, FR-AUTH-02

As a user, I want to log in with my credentials so that I can access features permitted for my role.

**Acceptance Criteria**
- Given valid credentials, when I submit the login form, I am redirected to the dashboard.
- Given incorrect credentials, I see "Invalid username or password" without revealing which credential is incorrect.
- Given empty fields, inline validation prevents form submission.
- Given a deactivated account, login is refused with a clear message.
- The password field is masked by default and provides a show/hide option.

### US-02: Logout (M) — FR-AUTH-02

As a user, I want to log out so that nobody else can use my session.

**Acceptance Criteria**
- Logging out clears the authentication token from the client.
- The user is redirected to the Login screen.
- After logout, protected pages cannot be accessed, including through browser navigation.

### US-03: Session Expiry (S) — FR-AUTH-02

As a user, I want to be notified when my session expires so that I can log in again.

**Acceptance Criteria**
- When the authentication token expires, the user is redirected to Login.
- A "Session expired" message is displayed.

### US-04: Change Password (S) — FR-AUTH-05

As a user, I want to change my password so that I can keep my account secure.

**Acceptance Criteria**
- The user must provide their current password.
- The new password must meet the application's password policy.
- The new password and confirmation must match.
- A success message is displayed after the password is changed.

### US-05: Access Denied (M) — FR-AUTH-03

As a user, I want to see an "Access Denied" page if I try to access a feature outside my role.

**Acceptance Criteria**
- Navigation hides items that are not permitted for the user's role.
- Direct access to a restricted page displays SCR-18.
- The API returns HTTP 403 Forbidden for unauthorized access.

## 2. Dashboard

### US-06: Overview Statistics (M) — FR-DSH-01

As an Administrator, I want to see the total number of products, categories, and suppliers so that I can understand the size of the catalog.

**Acceptance Criteria**
- Three statistic cards are displayed when the dashboard loads.
- Each card displays 0 instead of remaining blank when there is no data.

### US-07: Sales Totals (M) — FR-DSH-02

As an Administrator, I want to see total sales for today, this month, and all time so that I can monitor sales performance.

**Acceptance Criteria**
- Sales amounts are formatted with the configured currency and thousands separators.
- Values are updated when the dashboard is refreshed after a new sale.

### US-08: Low-Stock Alerts (M) — FR-DSH-03

As an Administrator or Stock Manager, I want to see a list of low-stock products so that I can reorder stock in time.

**Acceptance Criteria**
- Each item displays its image, name, current available quantity, and reorder level.
- Items are sorted by lowest available quantity first.
- Each row provides access to the relevant product.
- If there are no low-stock items, the message "No low-stock items" is displayed.

### US-09: Near-Expiry Alerts (S) — FR-DSH-04

As a Stock Manager, I want to see expired batches and batches expiring within 30 days so that I can take action before products become unsuitable for sale.

**Acceptance Criteria**
- Expired batches are highlighted in red.
- Near-expiry batches are highlighted in amber.
- Each row displays the batch number, product name, expiry date, and quantity.

### US-10: Role-Based Dashboard (S) — FR-DSH-06

As a Sales Clerk, I want a simple dashboard with a shortcut to the POS so that I can start processing sales quickly.

**Acceptance Criteria**
- The Sales Clerk cannot see supplier or user statistics.
- A "New Sale" button is displayed.
- A low-stock list is displayed.

### US-11: Best Sellers (C) — FR-DSH-05

As an Administrator, I want to see the best-selling products so that I can make better purchasing decisions.

**Acceptance Criteria**
- The dashboard displays the top 5 products by quantity sold during the current month.

## 3. User Management

### US-12: View Users (M) — FR-USR-02

As an Administrator, I want to view a list of users with their roles and account statuses so that I can manage staff accounts.

**Acceptance Criteria**
- The table displays name, username/email, role, and status.
- Users can be searched and filtered by role.

### US-13: Create User (M) — FR-USR-01

As an Administrator, I want to create a user and assign a role so that new staff can use the system.

**Acceptance Criteria**
- Required fields are validated.
- Duplicate usernames and email addresses are rejected with clear error messages.
- The role must be selected from the three available roles.
- A success notification is displayed, and the new user appears in the users list.

### US-14: Edit User and Role (M) — FR-USR-03

As an Administrator, I want to edit a user's details and role so that user records remain up to date.

**Acceptance Criteria**
- Updated details are saved and displayed in the users list.
- Role changes take effect the next time the user logs in.

### US-15: Deactivate / Reactivate User (M) — FR-USR-04, FR-USR-06

As an Administrator, I want to deactivate or reactivate a user so that I can control account access while preserving user history.

**Acceptance Criteria**
- A confirmation dialog is displayed before deactivation.
- Deactivated users cannot log in or access protected resources.
- The Administrator cannot deactivate their own account.
- Reactivated users can log in again.

### US-16: Reset Password (S) — FR-USR-05

As an Administrator, I want to reset a user's password so that staff who cannot access their accounts can regain access.

**Acceptance Criteria**
- The Administrator can assign a temporary password.
- The user must change the temporary password at the next login.
- The temporary password is securely handled and never stored as plain text.