# Execution
| Information | |
|---|---|
| **Team** | Team 14 |
| **Execution Date** | 23/05/2026 |
| **Browser** | Chrome Version 148 |
| **Operating System** | Windows 10 |

---
# Detailed Test Execution Results

| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Status | Evidence | Issue |
|---|---|---|---|---|---|---|
| TC-01 | Login | Librarian logs in successfully | System redirected user to Home page and displayed LIBRARIAN role correctly | Pass | AppBar displayed LIBRARIAN | N/A |
| TC-02 | Login | Member logs in successfully | System redirected user to Home page and displayed MEMBER role correctly | Pass | AppBar displayed MEMBER | N/A |
| TC-03 | Login | Display “Member not found” in English mode | System displayed “Không tìm thấy thành viên” | Fail | Error message displayed in Vietnamese while application language was set to English | BUG-01 |
| TC-04 | Login | Display “Incorrect password” in English mode | System displayed “Mật khẩu không đúng” | Fail | Error message displayed in Vietnamese while application language was set to English | BUG-02 |
| TC-05 | Login | Display validation message when both email and password are empty | System displayed “Please enter your email and password” | Pass | Validation message displayed correctly | N/A |
| TC-06 | Login | Behavior for empty email only is not clearly specified in the SRS | System displayed “Please enter your email and password” | Inconclusive | SRS does not define expected behavior for empty email only | Requirement Ambiguity |
| TC-07 | Login | Behavior for empty password only is not clearly specified in the SRS | System displayed “Please enter your email and password” | Inconclusive | SRS does not define expected behavior for empty password only | Requirement Ambiguity |
| TC-08 | Login |Requirement gap: SRS does not specify behavior for invalid email format (missing .) | System displayed “Member not found” | Inconclusive | SRS does not clearly define invalid email format validation | Requirement Gap |
| TC-09 | Login | Requirement gap: SRS does not specify behavior for invalid email format (missing @) | System displayed "Member not found" | Inconclusive | SRS does not define invalid email format validation | Requirement Gap |
| TC-10 | View Book List | Librarian can view complete book list | System displayed all books with complete information correctly | Pass | Book list displayed successfully | N/A |
| TC-11 | View Book List | Member can view complete book list | System displayed all books with complete information correctly | Pass | Book list displayed successfully | N/A |
| TC-12 | View Book List | Display correct information for BOOK001 | System displayed title, author, genre, published year, and status correctly | Pass | BOOK001 information displayed correctly | N/A |
| TC-13 | View Book List | Display correct status for BOOK001 and BOOK003 | BOOK001 displayed as “Available” and BOOK003 displayed as “Borrowed” | Pass | Book statuses displayed correctly | N/A |
| TC-14 | View Book List | Update BOOK001 status after borrowing | BOOK001 status changed immediately from “Available” to “Borrowed” | Pass | Real-time update worked correctly | N/A |
| TC-15 | View Book List | Update BOOK003 status after returning | BOOK003 status changed immediately from “Borrowed” to “Available” | Pass | Real-time update worked correctly | N/A |


---

# Test Execution Summary

| Metric | Value |
|---|---|
| Total Test Cases | 15 |
| Pass | 9 |
| Fail | 2 |
| Inconclusive | 4 (TC-06, TC-07, TC-08, TC-09)|
| Blocked | 0 |
| Not Run | 0 |
| Pass Rate | 60.0% |

---

# Results by Functional Group

| Functional Group | Total TC | Pass | Fail | Inconclusive | Blocked | Pass Rate |
|---|---|---|---|---|---|---|
| Login | 9 | 3 | 2 | 4 | 0 | 33.3% |
| View Book List | 6 | 6 | 0 | 0 | 0 | 100% |