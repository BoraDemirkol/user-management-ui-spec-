# User Management UI Specification

## 1. Overview

This document defines the user interface (UI), behavior, and interaction details for the **User Management Screen**.

The screen enables administrators to:
- View existing users
- Create new users
- Edit user information
- Enable/disable users
- Filter users

This document is intended for software developers to implement the UI accurately.

---

## 2. Layout Structure

The screen is divided into two main sections:

### 2.1 Top Toolbar
- **New User Button**
- **Hide Disabled User Checkbox**
- **Save User Button (top-right aligned)**

---

### 2.2 Main Content Area

#### Left Panel – User List Table
Displays all users in a tabular format.

Columns:
- ID
- User Name
- Email
- Enabled (true/false)

Features:
- Row selection
- Column sorting (via icons)
- Column filtering (via filter icons)

---

#### Right Panel – User Form
Used for creating or editing users.

Fields:
- Username
- Display Name
- Phone
- Email
- User Roles (dropdown)
- Enabled (checkbox)

---

## 3. Initial State (On Page Load)

- User table is populated via backend API
- All users are displayed
- "Hide Disabled User" checkbox is **unchecked**
- No row is selected
- Form is empty
- UI is in **Create Mode**
- "Save User" button is **disabled**

---

## 4. UI Components

### 4.1 Buttons

#### New User
- Clears form fields
- Switches UI to Create Mode
- Removes selected table row

---

#### Save User
- Saves current form data
- Disabled until form is valid
- Triggers create or update depending on mode

---

### 4.2 Checkbox

#### Hide Disabled User
- Checked → Only shows users where Enabled = true
- Unchecked → Shows all users

---

### 4.3 User Table

- Displays user list
- Clicking a row:
  - Selects the row
  - Loads user data into form
  - Switches to Edit Mode

---

### 4.4 Form Fields

#### Username
- Required
- Unique
- Cannot be edited in Edit Mode (optional constraint)

#### Display Name
- Optional

#### Phone
- Optional
- Numeric input expected

#### Email
- Required
- Must be valid email format

#### User Roles
- Multi-select dropdown
- Options:
  - Guest
  - Admin
  - SuperAdmin
- At least one role required

#### Enabled
- Checkbox
- Indicates active/inactive user

---

## 5. UI State Management

### Create Mode
- Triggered by:
  - Page load
  - Clicking "New User"
- Form is empty
- Save operation creates new user

---

### Edit Mode
- Triggered by selecting a row in table
- Form is populated
- Save operation updates existing user

---

## 6. User Interaction Flows

### 6.1 Create User Flow
1. Click "New User"
2. Fill required fields
3. Click "Save User"
4. New user appears in table

---

### 6.2 Edit User Flow
1. Select user from table
2. Modify fields
3. Click "Save User"
4. Table updates

---

### 6.3 Filter Flow
1. Check "Hide Disabled User"
2. Disabled users are hidden

---

## 7. Validation Rules

| Field        | Rule                          |
|-------------|------------------------------|
| Username     | Required, unique             |
| Email        | Required, valid format       |
| Roles        | At least one must be selected|
| Phone        | Numeric only (optional)      |

---

## 8. Button State Logic

- Save User button is enabled only when:
  - Required fields are filled
  - Validation passes

- Disabled when:
  - Form is empty
  - Invalid input exists

---

## 9. Error Handling

- Inline error messages displayed under fields
- Example:
  - "Email is invalid"
  - "Username already exists"
- Prevent submission if errors exist

---

## 10. API Integration (Assumptions)

| Action            | Endpoint            |
|------------------|---------------------|
| Get Users        | GET /users          |
| Create User      | POST /users         |
| Update User      | PUT /users/{id}     |

- UI refreshes after successful operation

---

## 11. Data Handling

- Table data is fetched on page load
- Form updates are reflected instantly in UI
- Selected user is tracked in state

---

## 12. Security Considerations

- Only Admin / SuperAdmin can access screen
- Input validation required (frontend + backend)
- Prevent injection attacks

---

## 13. Non-Functional Requirements

- Responsive UI design
- Fast rendering of user list
- Smooth user interaction
- Minimal latency on save

---

## 14. Edge Cases

- Duplicate username
- Invalid email format
- No role selected
- Switching between users without saving
- Filtering while editing

---

## 15. UX Considerations

- Highlight selected row
- Show success message after save
- Disable Save button during API call
- Maintain clean layout

---

## 16. Future Improvements

- Search bar
- Pagination
- Bulk user actions
- Audit logging
- Role-based UI restrictions
