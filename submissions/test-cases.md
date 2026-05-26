# Table 1: IDM for REQ-01 — Login

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| Existing Email | Valid librarian account | librarian@library.com | Login successful |
|  | Valid member account | ba.nguyen@email.com | Login successful |
|  | Non-existing email | khongtontai@gmail.com | Display message: “Member not found” |
| Password | Correct password | admin123 | User can log in successfully |
|  | Incorrect password | wrongpassword123 | Display message: “Incorrect password” |
| Input Fields | Both fields filled | Valid email + valid password | Continue login process |
|  | Both fields empty | Email: "" <br> Password: "" | Display message: “Please enter email and password” |
| Validation Behavior | Empty email only | Email: "" <br> Password: password123 |Display message: "Please enter email" |
|  | Empty password only | Email: ba.nguyen@email.com <br> Password: "" |Display message: "Please enter password" |
| Email Format (BVA) | Valid email format | ba.nguyen@email.com | Continue login validation |
| |Invalid email format(missing . in the format)|user@gmail| Display message: "Member not found"
| |Invalid email format(missing @ in the format)|abc.com| Display message: "Member not found "
---

# Table 2: IDM for REQ-02 — View Book List

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| User Role | Librarian | librarian@library.com | System displays complete book list |
|  | Member | ba.nguyen@email.com | System displays complete book list |
| Book Information Display | Complete book information | BOOK001 | System displays title, author, genre, published year, and status correctly |
| Book Status | Available | BOOK001 | Status displayed as “Available” |
|  | Borrowed | BOOK003 | Status displayed as “Borrowed” |
|  | Lost | BOOK007 | Status displayed as “Lost” |
| Real-time Update | After borrowing a book | BOOK001 | Status changes immediately to “Borrowed” |
|  | After returning a book | BOOK003 | Status changes immediately to “Available” |


# DECISION TABLE REQ-01:
| Condition | Case 1 | Case 2 | Case 3 | Case 4 | Case 5 |
|---|---|---|---|---|---|
| Email exists in DB? | YES | YES | NO | NO | — |
| Password correct? | YES | NO | YES | NO | — |
| Both fields empty? | NO | NO | NO | NO | YES |
| **Expected Result** | Login successful | "Incorrect password" | "Member not found" | "Member not found" | "Please enter email and password" |


# Table 3: TEST CASES FOR REQ-01 — Login
---
| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|---|---|---|---|---|---|---|---|
| TC-01 | Verify successful login with librarian account | User is on Login page and not logged in | 1. Open https://stqa.rbc.vn <br> 2. Enter email <br> 3. Enter password <br> 4. Click “Login” | Email: librarian@library.com <br> Password: admin123 | User is redirected to Home page. AppBar displays role “LIBRARIAN” | REQ-01 | EP |
| TC-02 | Verify successful login with member account | User is on Login page and not logged in | 1. Open https://stqa.rbc.vn <br> 2. Enter email <br> 3. Enter password <br> 4. Click “Login” | Email: ba.nguyen@email.com <br> Password: password123 | User is redirected to Home page. AppBar displays role “MEMBER” | REQ-01 | EP |
| TC-03 | Verify login with non-existing email | User is on Login page | 1. Open https://stqa.rbc.vn <br> 2. Enter non-existing email <br> 3. Enter password <br> 4. Click “Login” | Email: khongtontai@gmail.com <br> Password: password123 | System displays message: “Member not found” | REQ-01 | EP |
| TC-04 | Verify login with incorrect password | User is on Login page | 1. Open https://stqa.rbc.vn <br> 2. Enter valid email <br> 3. Enter incorrect password <br> 4. Click “Login” | Email: ba.nguyen@email.com <br> Password: wrongpassword123 | System displays message: “Incorrect password” | REQ-01 | EP |
| TC-05 | Verify login when both email and password are empty | User is on Login page | 1. Open https://stqa.rbc.vn <br> 2. Leave Email empty <br> 3. Leave Password empty <br> 4. Click “Login” | Email: "" <br> Password: "" | System displays message: “Please enter email and password” | REQ-01 | EP |
| TC-06 | Verify system behavior when email field is empty | User is on Login page | 1. Open https://stqa.rbc.vn <br> 2. Leave Email empty <br> 3. Enter password <br> 4. Click “Login” | Email: "" <br> Password: password123 | Requirement gap: SRS does not specify expected behavior when only email field is empty | REQ-01 | EP |
| TC-07 | Verify system behavior when password field is empty | User is on Login page | 1. Open https://stqa.rbc.vn <br> 2. Enter email <br> 3. Leave Password empty <br> 4. Click “Login” | Email: user@gmail.com <br> Password: "" | Requirement gap: SRS does not specify expected behavior when only password field is empty | REQ-01 | EP |
| TC-08 | Verify system behavior for invalid email format(missing @) | User is on Login page | 1. Open https://stqa.rbc.vn <br> 2. Enter invalid email format <br> 3. Enter password <br> 4. Click “Login” | Email: abc.com <br> Password: password123 | "Requirement gap: SRS does not specify expected behavior for invalid email format (missing @)" | REQ-01 | BVA |
| TC-09 | Verify system behavior for invalid email format(missing .) | User is on Login page | 1. Open https://stqa.rbc.vn <br> 2. Enter invalid email format <br> 3. Enter password <br> 4. Click “Login” | Email: user@gmail <br> Password: password123 | "Requirement gap: SRS does not specify expected behavior for invalid email format (missing .)" | REQ-01 | BVA |

---

# Table 4: TEST CASES FOR REQ-02 — View Book List

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|---|---|---|---|---|---|---|---|
| TC-10 | Verify librarian can view the complete book list | User is logged in as librarian | 1. Login as librarian <br> 2. Navigate to the “Books” tab <br> 3. Check displayed book list | Email: librarian@library.com <br> Password: admin123 | System displays all books with title, author, genre, published year, and status | REQ-02 | EP |
| TC-11 | Verify member can view the complete book list | User is logged in as member | 1. Login as member <br> 2. Navigate to the “Books” tab <br> 3. Check displayed book list | Email: ba.nguyen@email.com <br> Password: password123 | System displays all books with title, author, genre, published year, and status | REQ-02 | EP |
| TC-12 | Verify complete book information is displayed correctly | User is logged in and currently on the “Books” tab | 1. Login <br> 2. Navigate to the “Books” tab <br> 3. Check information of BOOK001 | BOOK001 | System correctly displays title, author, genre, published year, and status for BOOK001 | REQ-02 | EP |
| TC-13 | Verify book status is displayed correctly | User is logged in and currently on the “Books” tab | 1. Login <br> 2. Navigate to the “Books” tab <br> 3. Check status of BOOK001 and BOOK003 | BOOK001, BOOK003 | BOOK001 status is displayed as “Available”. BOOK003 status is displayed as “Borrowed” | REQ-02 | EP |
| TC-14 | Verify real-time status update after borrowing a book | User is logged in as member. BOOK001 is currently “Available” | 1. Login as member <br> 2. Navigate to the “Books” tab <br> 3. Verify BOOK001 is “Available” <br> 4. Borrow BOOK001 <br> 5. Return to the “Books” tab <br> 6. Check BOOK001 status again | BOOK001 | BOOK001 status changes immediately from “Available” to “Borrowed” | REQ-02 | EP |
| TC-15 | Verify real-time status update after borrowing a book | User is logged in as member. BOOK007 is currently “Lost” | 1. Login as member <br> 2. Navigate to the “Books” tab <br> 3. Verify BOOK007 is “Lost” <br>|BOOK007,BOOK020 | BOOK007 status remains “Lost” | REQ-02 | EP |
| TC-16 | Verify real-time status update after returning a book | User is logged in as member. BOOK003 is currently “Borrowed” | 1. Login as member <br> 2. Navigate to the “Books” tab <br> 3. Verify BOOK003 is “Borrowed” <br> 4. Return BOOK003 <br> 5. Return to the “Books” tab <br> 6. Check BOOK003 status again | BOOK003 | BOOK003 status changes immediately from “Borrowed” to “Available” | REQ-02 | EP |

---

# SUMMARY TABLE
| Functional Group | TC Count | REQ Covered | IDM Technique Used |
|---|---|---|---|
| Login | 9 | REQ-01 | Equivalence Partitioning (EP), Boundary Value Analysis (BVA), Decision Table |
| View Book List | 7 | REQ-02 | Equivalence Partitioning (EP) |

- Total: 16 test cases, 2 REQs covered
- Techniques applied: EP (all TCs), BVA (TC-08, TC-09), Decision Table (REQ-01)