# Execution
| Information | |
|---|---|
| **Team** |  14 |
| **Execution Date** | 23/05/2026 |
| **Browser** | Chrome Version 148 |
| **Operating System** | Windows 10 |

## REQ-01: Login
| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Status | Evidence | Issue |
|---|---|---|---|---|---|---|
| TC-01-01 | Login | Librarian logs in successfully | System redirected user to Home page and displayed LIBRARIAN role correctly | Pass | N/A | - |
| TC-01-02 | Login | Member logs in successfully | System redirected user to Home page and displayed MEMBER role correctly | Pass |  N/A | - |
| TC-01-03 | Login | Display “Member not found” in English mode | System displayed “Không tìm thấy thành viên” | Fail | [View Evidence](Evidences/REQ-01-02/TC-01-03.jpg)|OBS-01|
| TC-01-04 | Login | Display “Incorrect password” in English mode | System displayed “Mật khẩu không đúng” | Fail | [View Evidence](Evidences/REQ-01-02/TC-01-04.jpg) | OBS-01 |
| TC-01-05 | Login | Display validation message when both email and password are empty | System displayed “Please enter your email and password” | Pass |  N/A | - |
| TC-01-06 | Login | Behavior for empty email only is not clearly specified in the SRS | System displayed “Please enter your email and password” | Inconclusive | SRS does not define expected behavior for empty email only [View Evidence](Evidences/REQ-01-02/TC-01-06.jpg) | OBS-02 |
| TC-01-07 | Login | Behavior for empty password only is not clearly specified in the SRS | System displayed “Please enter your email and password” | Inconclusive | SRS does not define expected behavior for empty password only [View Evidence](Evidences/REQ-01-02/TC-01-07.jpg) | OBS-02 |
| TC-01-08 | Login |Requirement gap: SRS does not specify behavior for invalid email format (missing .) | System displayed “Member not found” | Inconclusive | SRS does not clearly define invalid email format validation [View Evidence](Evidences/REQ-01-02/TC-01-08.jpg) | OBS-03 |
| TC-01-09 | Login | Requirement gap: SRS does not specify behavior for invalid email format (missing @) | System displayed "Member not found" | Inconclusive | SRS does not define invalid email format validation [View Evidence](Evidences/REQ-01-02/TC-01-09.jpg) | OBS-03 |
---
## REQ-02: View Book List
| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Status | Evidence | Issue |
|---|---|---|---|---|---|---|
| TC-02-01 | View Book List | Librarian can view complete book list | System displayed all books with complete information correctly | Pass |  [View Evidence](Evidences/REQ-01-02/TC-02-01.jpg)| - |
| TC-02-02 | View Book List | Member can view complete book list | System displayed all books with complete information correctly | Pass | [View Evidence](Evidences/REQ-01-02/TC-02-02.jpg) | - |
| TC-02-03 | View Book List | Display correct information for BOOK001 | System displayed title, author, genre, published year, and status correctly | Pass | [View Evidence](Evidences/REQ-01-02/TC-02-03.jpg) | - |
| TC-02-04 | View Book List | Display correct status for BOOK001 and BOOK003 | BOOK001 displayed as “Available” and BOOK003 displayed as “Borrowed” | Pass | [View Evidence](Evidences/REQ-01-02/TC-02-04.jpg) | -|
| TC-02-05 | View Book List | Update BOOK001 status after borrowing | BOOK001 status changed immediately from “Available” to “Borrowed” | Pass | N/A|- |
| TC-02-06 | View Book List | BOOK007 is displayed with status “Lost” | System displayed BOOK007 with status “Lost” correctly | Pass | N/A| - |
| TC-02-07 | View Book List | Update BOOK003 status after returning | BOOK003 status changed immediately from “Borrowed” to “Available” | Pass | N/A| - |
---

---

# Test Execution Summary

| Metric | Value |
|---|---|
| Total Test Cases | 16 |
| Pass | 10 |
| Fail | 2 |
| Inconclusive | 4 (TC-01-06, TC-01-07, TC-01-08, TC-01-09)|
| Blocked | 0 |
| Not Run | 0 |
| Pass Rate | 62.5% |

---

# Results by Functional Group

| Functional Group | Total TC | Pass | Fail | Inconclusive | Blocked | Pass Rate |
|---|---|---|---|---|---|---|
| Login | 9 | 3 | 2 | 4 | 0 | 33.3% |
| View Book List | 7 | 7 | 0 | 0 | 0 | 100% |