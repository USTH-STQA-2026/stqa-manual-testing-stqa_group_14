# Execution
| Information | |
|---|---|
| **Team** |  14 |
| **Execution Date** | 23/05/2026 |
| **Browser** | Chrome Version 148 |
| **Operating System** | Windows 10 |

---
## Bước 3: Test Execution

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
| TC-02-01 | View Book List | Librarian can view complete book list | System displayed all 20 books with complete information correctly | Pass |  [View Evidence](Evidences/REQ-01-02/TC-02-01.jpg)| - |
| TC-02-02 | View Book List | Member can view complete book list | System displayed all 20 books with complete information correctly | Pass | [View Evidence](Evidences/REQ-01-02/TC-02-02.jpg) | - |
| TC-02-03 | View Book List | Display correct information for BOOK001 | System displayed title, author, genre, published year correctly | Pass | [View Evidence](Evidences/REQ-01-02/TC-02-03.jpg) | - |
| TC-02-04 | View Book List | Display correct status for BOOK001 and BOOK003 | BOOK001 displayed as “Available” and BOOK003 displayed as “Borrowed” | Pass | [View Evidence](Evidences/REQ-01-02/TC-02-04.jpg) | -|
| TC-02-05 | View Book List | Update BOOK001 status after borrowing | BOOK001 status changed immediately from “Available” to “Borrowed” | Pass | N/A|- |
| TC-02-06 | View Book List | BOOK007 is displayed with status “Lost” | System displayed BOOK007 with status “Lost” correctly | Pass | N/A| - |
| TC-02-07 | View Book List | Update BOOK003 status after returning | BOOK003 status changed immediately from “Borrowed” to “Available” | Pass | N/A| - |
---
## REQ-03: Search & Filter Books
| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Status | Evidence | Issue |
|---|---|---|---|---|---|---|
| TC-03-01 | Search by title/author | Display 1 book: BOOK001 (baseline for TC-05) | Display BOOK001 | Pass |N/A| -|
| TC-03-02 | As above | Display 2 books: BOOK001, BOOK009 | Display BOOK001, 009 | Pass |N/A| - |
| TC-03-03 | Filter by category | Display 8 books in Technology: BOOK001, 002, 003, 005, 008, 009, 010, 011 (baseline for TC-06) | Display BOOK001, 002, 003, 005, 008, 009, 010, 011 | Pass |N/A| -|
| TC-03-04 | Both bars | Display "No books found" | Display "No books found" |  Pass | N/A| - |
| TC-03-05 | Case sensitivity — title/author bar | Display 1 book: BOOK001 for both `"nguyễn minh đức"` and `"NGUYỄN MINH ĐỨC"` (same as TC-03-01) | Display BOOK001 for both inputs | Pass | N/A| - |
| TC-03-06 | Case sensitivity — category bar | Display 8 books for both `"công nghệ"` and `"CÔNG NGHỆ"` (same as TC-03-03) | Display "No books found", blank list for both inputs | Fail |  [Lowercase](Evidences/REQ-03/TC-06_lowercase%20(Medium).png), [Uppercase](Evidences/REQ-03/TC-06_uppercase%20(Medium).png)| BUG-01 |
| TC-03-07 | Diacritic sensitivity — name bar | Display 2 books: BOOK001, BOOK009 (same as TC-03-02) | Display "No books found", blank list | Inconclusive | [Author without diacritics](Evidences/REQ-03/TC-07_author-without-diacritics%20(Low).png) | OBS-04 |
| TC-03-08 | Diacritic sensitivity — category bar | Display 8 books: BOOK001, 002, 003, 005, 008, 009, 010, 011 (same as TC-03-03) | Display "No books found", blank list | Inconclusive | [Genre without diacritics](Evidences/REQ-03/TC-07_genre-without-diacritics%20(Low).png) | OBS-04 |
| TC-03-09 | Partial keyword — title/author bar | Display 4 books whose author contains "Nguyễn": BOOK001, 006, 009, 016 | Display BOOK001, 006, 009, 016 | Pass |N/A | - |
| TC-03-10 | Partial keyword — category bar | Display 8 books whose genre contains "Công": BOOK001, 002, 003, 005, 008, 009, 010, 011 | Display "No books found", blank list | Inconclusive | [Evidence](Evidences/REQ-03/TC-03-09%20Observed.png) | OBS-05 |
| TC-03-11 | Empty fields | Display all 20 books | Display all 20 books | Pass |N/A| -|
| TC-03-12 | Combined search - match | Display 2 books: BOOK001, BOOK009 | (1) If keyword entered first then category — display 8 Technology books: BOOK001, 002, 003, 005, 008, 009, 010, 011 (category overrides keyword); (2) If category entered first then keyword — display 2 books: BOOK001, BOOK009 (keyword overrides category) | Fail | [Author first 1](Evidences/REQ-03/TC-11_author-first_1%20(High).png), [Author first 2](Evidences/REQ-03/TC-11_author-first_2%20(High).png), [Author first 3](Evidences/REQ-03/TC-11_author-first_3%20(High).png), [Genre first](Evidences/REQ-03/TC-11_genre-first%20(High).png) | BUG-02 |
| TC-03-13 | Combined search - mismatch | Display "No books found" | (1) If keyword entered first then category — display 3 Economics books: BOOK007, BOOK014, BOOK015 (category overrides keyword); (2) If category entered first then keyword — display 2 books: BOOK001, BOOK009 (keyword overrides category); | Fail | [Author first](Evidences/REQ-03/TC-12_author-first%20(High).png), [Genre first](Evidences/REQ-03/TC-12_genre-first%20(High).png) | BUG-02 |
| TC-03-14 | Category bar — English keyword (bilingual support) | Display 8 books in Technology category (same as TC-03-03) | Display "No books found" | Fail | N/A | OBS-06 |
---
## REQ-04: Borrow book
| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Status | Evidence | Issue |
|---|---|---|---|---|---|---|
| TC-04-01 | Borrow Book | Member can borrow the book, successful message displayed in corresponding language| Member can borrow the book, successful message displayed in corresponding language | Pass | <a href="Evidences/REQ-04/evidence/TC-04-01/BOOK001_before.png">Before borrowing BOOK001</a><br><a href="Evidences/REQ-04/evidence/TC-04-01/BOOK001_after_vi.png">After borrowing BOOK001 (Vietnamese)</a><br><a href="Evidences/REQ-04/evidence/TC-04-01/BOOK001_after_en.png">After borrowing BOOK001 (English)</a><br><a href="Evidences/REQ-04/evidence/TC-04-01/BR_before.png">Borrow records before borrowing</a><br><a href="Evidences/REQ-04/evidence/TC-04-01/BR_after.png">Borrow records after borrowing</a> | - |
| TC-04-02 | Borrow Book | Member cannot borrow the book | Member cannot borrow the book | Pass | <a href="Evidences/REQ-04/evidence/TC-04-02/BOOK003_before.png">Before borrowing BOOK003</a><br><a href="Evidences/REQ-04/evidence/TC-04-02/BOOK003_after.png">After borrowing BOOK003</a><br><a href="Evidences/REQ-04/evidence/TC-04-02/BR_before.png">Borrow records before borrowing</a><br><a href="Evidences/REQ-04/evidence/TC-04-02/BR_after.png">Borrow records after borrowing</a> | - |
| TC-04-03 | Borrow Book | Member cannot borrow the book | Member cannot borrow the book | Pass | <a href="Evidences/REQ-04/evidence/TC-04-03/BOOK007_before.png">Before borrowing BOOK007</a><br><a href="Evidences/REQ-04/evidence/TC-04-03/BOOK007_after.png">After borrowing BOOK007</a><br><a href="Evidences/REQ-04/evidence/TC-04-03/BR_before.png">Borrow records before borrowing</a><br><a href="Evidences/REQ-04/evidence/TC-04-03/BR_after.png">Borrow records after borrowing</a> | - |
| TC-04-04 | Borrow Book | - Member cannot borrow the book<br>- Error message on member being suspended is displayed in corresponding language | - Member cannot borrow the book<br>- Error message says the member has expired<br>- Error message is Vietnamese while display language is English | Fail | <a href="Evidences/REQ-04/evidence/TC-04-04%20BUG(Low%20and%20Medium)/BOOK001_before.png">Before borrowing BOOK001</a><br><a href="Evidences/REQ-04/evidence/TC-04-04%20BUG(Low%20and%20Medium)/BOOK001_after_vi.png">After borrowing BOOK001 (Vietnamese)</a><br><a href="Evidences/REQ-04/evidence/TC-04-04%20BUG(Low%20and%20Medium)/BOOK001_after_en.png">After borrowing BOOK001 (English)</a><br><a href="Evidences/REQ-04/evidence/TC-04-04%20BUG(Low%20and%20Medium)/BR_before.png">Borrow records before borrowing</a><br><a href="Evidences/REQ-04/evidence/TC-04-04%20BUG(Low%20and%20Medium)/BR_after.png">Borrow records after borrowing</a> | BUG-03, OBS-06 |
| TC-04-05 | Borrow Book | - Member cannot borrow the book<br>- Error message on member having expired is displayed in corresponding language | - Member cannot borrow the book<br>- Error message says the member has expired<br>- Error message is Vietnamese while display language is English | Pass | <a href="Evidences/REQ-04/evidence/TC-04-05%20BUG(Low)/BOOK001_before.png">Before borrowing BOOK001</a><br><a href="Evidences/REQ-04/evidence/TC-04-05%20BUG(Low)/BOOK001_after_vi.png">After borrowing BOOK001 (Vietnamese)</a><br><a href="Evidences/REQ-04/evidence/TC-04-05%20BUG(Low)/BOOK001_after_en.png">After borrowing BOOK001 (English)</a><br><a href="Evidences/REQ-04/evidence/TC-04-05%20BUG(Low)/BR_before.png">Borrow records before borrowing</a><br><a href="Evidences/REQ-04/evidence/TC-04-05%20BUG(Low)/BR_after.png">Borrow records after borrowing</a> | OBS-06 |
| TC-04-06 | Borrow Book | - Member cannot borrow book BOOK005<br>- Error on limit having exceeded is displayed in corresponding language<br>- Borrow record is not created for BOOK005 | Member can borrow book BOOK005, no error message is displayed, borrow record for BOOK005 is created | Fail | <a href="Evidences/REQ-04/evidence/TC-04-06%20BUG/BOOK005_before.png">Before borrowing BOOK005</a><br><a href="Evidences/REQ-04/evidence/TC-04-06%20BUG/BOOK005_after.png">After borrowing BOOK005</a><br><a href="Evidences/REQ-04/evidence/TC-04-06%20BUG/BR_before.png">Borrow records before borrowing</a><br><a href="Evidences/REQ-04/evidence/TC-04-06%20BUG/BR_after.png">Borrow records after borrowing</a> | BUG-04 |

---
## REQ-05: Return Book
| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Status | Evidence | Issue |
|---|---|---|---|---|---|---|
| TC-05-01 | Return Book | Book is returned successfully. No overdue warning message is displayed. Book status changes to **"Available"**. Borrow record status changes to **"Returned"**. | Borrow record changed to **"Returned"**. Book status changed to **"Available"**. No overdue warning message was displayed. | Pass | N/A | - |
| TC-05-02 | Return Book | Book is returned successfully. System displays a clear overdue warning. Book status changes to **"Available"**. Borrow record status changes to **"Returned"**. | Book was returned successfully and the record/book status was updated, but no overdue warning message was displayed when `returnDate = dueDate`. | Fail |[Book Status After Return](Evidences/REQ-05/TC-02-after-book%20BUG%20(Medium).png),[Borrow Record After Return](Evidences/REQ-05/TC-02-after-return%20BUG%20(Medium).png),[Borrow Record Before Return](Evidences/REQ-05/TC-02-before-record%20BUG%20(Medium).png)| BUG-05 |
| TC-05-03 | Return Book | Book is returned successfully. System displays a clear overdue warning. Book status changes to **"Available"**. Borrow record status changes to **"Returned"**. | Book was returned successfully and the record/book status was updated, but no overdue warning message was displayed for an overdue return (`returnDate > dueDate`). | Fail |[Book Status After Return](Evidences/REQ-05/TC-02-after-book%20BUG%20(Medium).png),[Borrow Record After Return](Evidences/REQ-05/TC-02-after-return%20BUG%20(Medium).png),[Borrow Record Before Return](Evidences/REQ-05/TC-02-before-record%20BUG%20(Medium).png)| BUG-05 |
| TC-05-04 | Return Book | System does not allow returning a book that has already been returned. The **Return Book** button is not displayed or cannot be used. Book status remains **"Available"**. Borrow record status remains **"Returned"**. | The borrow record remained in **"Returned"** status. The **Return Book** button was no longer displayed after the book had been returned, preventing duplicate return actions. Book status remained **"Available"**. | Pass | N/A| - |
| TC-05-05 | Return Book / Access Control | The system must not allow the logged-in member to view or return another member’s borrowed book. The borrow record status and book status remain unchanged. | The logged-in member was able to view and return a book borrowed by another member. The borrow record/book status was updated even though the record did not belong to the current user. | Fail |[Before Record](Evidences/REQ-05/TC-05-before-record%20BUG%20(High).png),[After Return](Evidences/REQ-05/TC-05-after-return%20BUG%20(High).png)| BUG-06 |
---
## REQ-06: Overdue Handling
| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Status | Evidence | Issue |
|---|---|---|---|---|---|---|
| TC-06-01 | Overdue Handling | Librarian can access and use the **Check Overdue** function. Overdue borrow records are displayed or updated after checking. | The librarian account successfully accessed and used the **Check Overdue** function. Borrow records were updated and overdue records were displayed after checking. | Pass | N/A | - |
| TC-06-02 | Overdue Handling | Borrow record with `current date < dueDate` is **not marked as "Overdue"**. Status remains **"Borrowing"**. | The borrow record was **not marked as "Overdue"**. The status remained **"Borrowing"** after overdue checking. | Pass| N/A| - |
| TC-06-03 | Overdue Handling | Borrow record with `current date = dueDate` is marked as **"Overdue"**. `dueDate <= current date` is considered overdue. | The borrow record was successfully marked as **"Overdue"** when the due date matched the current date. | Pass |N/A | - |
| TC-06-04 | Overdue Handling | Borrow record with `current date > dueDate` is marked as **"Overdue"**. | The overdue borrow record was successfully marked as **"Overdue"** after overdue checking. | Pass |N/A| - |
| TC-06-05 | Overdue Handling | Member cannot access or use the **Check Overdue** function. The button is not displayed or cannot be used. Member cannot mark records as **"Overdue"**. | The member account could not access the **Check Overdue** function. The **Check Overdue** button was not displayed in the interface. | Pass| N/A| - |
---

## REQ-07: Members
| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Status | Evidence | Issue |
|---|---|---|---|---|---|---|
| TC-07-01 | Members | Create valid member | System rejected, displays "Email invalid" | Fail | [View Evidence](Evidences/REQ-07/TC-01%20REQ-07%20BUG%20(High).png) | BUG-07 |
| TC-07-02 | Members | Reject email missing "." | System rejected, displays "Email invalid" | Pass |[View Evidence](Evidences/REQ-07/TC-02%20REQ-07%20BUG%20(High).png)| -|
| TC-07-03 | Members | Reject email missing "@" | Created Successfully | Fail | [View Evidence](Evidences/REQ-07/TC-03%20REQ-07.png)| BUG-07 |
| TC-07-04 | Members | Reject duplicate email | System rejected (email exists) | Pass |[View Evidence](Evidences/REQ-07/TC-04%20REQ-07.png)| -|
| TC-07-05 | Members | Member does not see "Add member" tab | Tab not displayed / not accessible | Pass |[View Evidence](Evidences/REQ-07/TC-05%20REQ-07.png) | -|
| TC-07-06 | Members | Create member with a@b.co successfully | System rejected (email invalid) | Fail |[View Evidence](Evidences/REQ-07/TC-06%20REQ-07%20BUG%20(High).png) | BUG-07|
| TC-07-14 | Members | Reject email with multiple @ or .. | System rejected (email invalid) | Pass |[View Evidence](Evidences/REQ-07/TC-14%20REQ-07.png)| -|
| TC-07-15 | Members | Reject blank username | System rejected (Username blank) | Pass | [View Evidence](Evidences/REQ-07/TC-15%20REQ-07.png)| -|
| TC-07-16 | Members | Reject wrong phone number | System rejected (Invalid phone number) | Pass |[View Evidence](Evidences/REQ-07/TC-16%20REQ-07.png) |- |
| TC-07-17 | Members | Librarian can view all members across categories (Active, Suspended, Expired) | Librarian saw all members appear in the "Member" list, categorized correctly | Pass | N/A | - |
---
## REQ-08: Search borrow tickets
| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Status | Evidence | Issue |
|---|---|---|---|---|---|---|
| TC-08-07 | Borrow/Return | Display BR001–BR005 (Librarian) | Display all tickets | Pass |[View Evidence](Evidences/REQ-08/TC-07%20REQ-08.png)| -|
| TC-08-08| Borrow/Return | Member sees only BR001 & BR004 | Only see BR001 & BR004 | Pass |[View Evidence](Evidences/REQ-08/TC-08%20REQ-08.png) | -|
| TC-08-09 | Borrow/Return | Member cannot view other ticket | MEM003 tickets displayed | Fail |[View Evidence](Evidences/REQ-08/TC-09%20REQ-08%20BUG%20(High).png) | BUG-08 |
| TC-08-10 | Borrow/Return | View BR001 details completely | Display all information | Pass |[View Evidence](Evidences/REQ-08/TC-10-11-12-13%20REQ-08.png) |- |
| TC-08-11 | Borrow/Return | BR002 displays "Returned" | Displays "Returned" | Pass |[View Evidence](Evidences/REQ-08/TC-10-11-12-13%20REQ-08.png) |- |
| TC-08-12 | Borrow/Return | Check Overdue marks BR001 | BR001 changes to "Overdue" if expired | Pass |[View Evidence](Evidences/REQ-08/TC-10-11-12-13%20REQ-08.png)| -|
| TC-08-13 | Borrow/Return | BR002 still "Returned" after check | BR002 still displays "Returned" | Pass |[View Evidence](Evidences/REQ-08/TC-10-11-12-13%20REQ-08.png)|- |
---
# SUMMARY TABLE

| Functional Group | TC Count | REQ Covered | IDM Technique Used |
|---|---|---|---|
| Login | 9 | REQ-01 | Equivalence Partitioning (EP) |
| View Book List | 7 | REQ-02 | Equivalence Partitioning (EP) |
| Search by Title/Author | 14 | REQ-03 | Equivalence Partitioning (EP), Boundary Value Analysis (BVA) |
| Borrow Book | 6 | REQ-04 | Equivalence Partitioning (EP), Decision Table (DT) |
| Return Book | 5 | REQ-05 | Equivalence Partitioning (EP), Decision Table (DT) |
| Overdue Handling | 5 | REQ-06 | Equivalence Partitioning (EP), Boundary Value Analysis (BVA) |
| Members Management | 10 | REQ-07 | Equivalence Partitioning (EP), Boundary Value Analysis (BVA) |
| Borrow/Return Records | 7 | REQ-08 | Equivalence Partitioning (EP), Access Control Testing |

- Total: 63 test cases, 8 REQs covered
- Techniques applied: EP, BVA, DT, Access Control Testing
---
