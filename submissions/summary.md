# Test Summary - Overall Testing Report

---

## 1. Group Information

| Item | Information |
|-----|-------------|
| **Group** | Group 14 |
| **Class** | ICT |
| **Report Date** | 28/05/2026 |
| **System Under Test** | https://stqa.rbc.vn - SRS v1.0 |
| **Testing Scope** | REQ-01 to REQ-08 |
| **Browser / Operating System** | Chrome Version 148 / Windows 10 |

---

## 2. Result Overview

| Metric | Value |
|--------|-------|
| Total executed test cases | 63 |
| Pass | 41 |
| Fail | 15 |
| Inconclusive | 7 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass Rate** | **65.08%** |
| **Confirmed Bugs** | **7** |
| **Observations / Requirement Issues** | **8** |

### Result by Functional Group

| Functional Group | TC | Pass | Fail | Inconclusive | Bug / Observation | Assessment |
|------------------|----|------|------|--------------|-------------------|------------|
| REQ-01 - Login | 9 | 3 | 2 | 4 | 0 bug, 3 observations | Partially Passed - Basic login flows work, but error messages and several input cases are not clearly specified in the SRS. |
| REQ-02 - View Book List | 7 | 7 | 0 | 0 | 0 | Passed - Book list display, book information, and status updates work correctly in the tested cases. |
| REQ-03 - Search & Filter Books | 14 | 7 | 4 | 3 | 1 bugs, 4 observations | Needs Improvement - Basic search works, but category filtering and combined search do not fully meet the requirements. |
| REQ-04 - Borrow Book | 6 | 4 | 2 | 0 | 2 bugs, 1 observation | Needs Improvement - Basic borrowing can work, but the borrow-limit rule and member-status messages still contain defects. |
| REQ-05 - Return Book | 5 | 2 | 3 | 0 | 2 bugs | Needs Improvement - Valid return cases can succeed, but overdue warnings and borrow-record ownership control are incorrect. |
| REQ-06 - Overdue Handling | 5 | 5 | 0 | 0 | 0 | Passed - The overdue checking function works correctly for before-due, on-due, and after-due date conditions. |
| REQ-07 - Member Management | 10 | 7 | 3 | 0 | 1 bug | Needs Improvement - Member-tab permission and several validation cases work, but email validation during member creation is seriously flawed. |
| REQ-08 - Borrow/Return Records | 7 | 6 | 1 | 0 | 1 bug | Needs Improvement - Librarian access works as expected, but members can still view tickets belonging to other members. |
| **Total** | **63** | **41** | **15** | **7** | **7 bugs, 8 observations** | **System is not ready for release.** |

### Bug Distribution by Severity

| Severity | Quantity | Bug IDs |
|----------|----------|---------|
| High | 5 | BUG-02, BUG-03, BUG-05, BUG-06, BUG-07 |
| Medium | 2 | BUG-01,  BUG-04 |
| Low | 0 | None |

### Observations / Requirement Issues

| Type | Quantity | IDs |
|------|----------|-----|
| Localization / UI consistency | 3 | OBS-01, OBS-07, OBS-08 |
| Requirement Ambiguity | 1 | OBS-02 |
| Requirement Gap | 4 | OBS-03, OBS-04, OBS-05, OBS-06 |

---

## 3. Test Design Techniques Used

| Technique | Applied Requirements | Application |
|-----------|----------------------|-------------|
| Equivalence Partitioning (EP) | REQ-01 to REQ-08 | Inputs were divided into valid and invalid partitions, including login accounts, roles, book status, search keywords, categories, member status, borrow-record status, email, phone number, and access permissions. |
| Boundary Value Analysis (BVA) | REQ-04, REQ-05, REQ-06, REQ-07 | Boundary values were tested, such as borrowed-book count equal to 3, current date equal to due date, shortest valid email, and email/phone formats near valid and invalid boundaries. |
| Decision Table | REQ-01, REQ-03, REQ-04, REQ-05, REQ-06, REQ-07, REQ-08 | Used to combine multiple input conditions, especially for login, combined search, borrowing conditions, return-book behavior, and permission to view borrow records. |
| Access Control Testing | REQ-05, REQ-07, REQ-08 | Used to verify permission boundaries between librarian and member roles, including whether members can access the Members tab, view other members' tickets, or return books owned by other members. |
| Negative Testing | REQ-01, REQ-03, REQ-04, REQ-05, REQ-07, REQ-08 | Used to test invalid inputs, non-existing accounts, no-result keywords, unavailable books, invalid members, records not owned by the current user, and invalid member information. |

---

## 4. Software Quality Analysis

### 4.1. Strengths

- Login with both librarian and member accounts works correctly for valid credentials.
- The book list displays the required information and updates book status after borrow/return actions.
- Searching by book title or author works correctly with valid input, including lowercase and uppercase input in the keyword search bar.
- The category filter returns correct results when the exact existing category name is entered.
- Borrowing works for active members when the book is available and the member is below the borrow limit.
- The system blocks several invalid borrowing cases, such as borrowing books that are already borrowed or lost.
- Valid return actions correctly update both book status and borrow-record status.
- The system prevents returning a book that has already been returned.
- The librarian's Check Overdue function works correctly for before-due, on-due, and after-due date conditions.
- Basic permission control for the Members tab works: members cannot see or access member-management features.
- The test design covers REQ-01 to REQ-08 and combines EP, BVA, Decision Table, and Access Control Testing.

### 4.2. Weaknesses

#### REQ-01 - Login

**Observations / Requirement issues**
- **OBS-01 - Error messages are not consistently localized.** When the interface is in English mode, some login error messages are still displayed in Vietnamese.
- **OBS-02 - The SRS does not clearly specify cases where only email or only password is empty.** Therefore, TC-01-06 and TC-01-07 cannot be confidently evaluated as pass or fail.
- **OBS-03 - The SRS does not define email-format validation during login.** Inputs such as `abc.com` or `user@gmail` do not have clear expected results.

#### REQ-02 - View Book List

**No confirmed bug recorded.**

- All REQ-02 test cases passed. Book list display, book information, book status, and real-time status updates are stable within the tested scope.

#### REQ-03 - Search & Filter Books

**Medium**
- **BUG-01 - Category filter is case-sensitive.** The category filter does not comply with the case-insensitive requirement in REQ-03, while the keyword search bar handles case variations correctly.

**Observations / Requirement issues**
- **OBS-04 - Search does not support Vietnamese diacritic-insensitive input.** Inputs without diacritics, such as `Nguyen Minh Duc` or `Cong nghe`, return no results.
- **OBS-05 - Category filter does not support partial match.** The category field requires the full exact category name, which is inconsistent with the keyword search bar.
- **OBS-06 - Combined search does not apply AND logic.** When both keyword and category are entered, the system does not apply both filters at the same time. The result depends on the search field entered last, causing users to receive incorrect results.
- **OBS-07 - Category bar does not support English category input.** When the interface is in English, entering `Technology` does not return the corresponding book list.

#### REQ-04 - Borrow Book

**High**
- **BUG-03 - A member can still borrow a book when their current borrow count is already 3.** The system creates a new borrow record and displays no borrow-limit error, violating the maximum-borrow business rule.

**High**
- **BUG-02 - Incorrect error reason is displayed for suspended members.** A suspended member is correctly prevented from borrowing, but the system displays the reason as expired instead of suspended.

**Observations / Requirement issues**
- **OBS-08 - Some error messages remain in Vietnamese when the display language is English.** This affects language consistency in borrowing workflows.

#### REQ-05 - Return Book

**High**
- **BUG-05 - A member can return another member's borrowed book.** The system allows members to view and act on borrow records that do not belong to them, creating security, data ownership, and book-status integrity risks.

**Medium**
- **BUG-04 - No overdue warning is displayed when returning overdue books or books on the due date.** The return action succeeds, but the system does not show the required overdue warning according to BR-05 and BR-06.

#### REQ-06 - Overdue Handling

**No confirmed bug recorded.**

- Librarians can use Check Overdue.
- Members cannot access Check Overdue.
- The system correctly handles `currentDate < dueDate`, `currentDate = dueDate`, and `currentDate > dueDate`.

#### REQ-07 - Member Management

**High**
- **BUG-06 - Email validation is incorrect when creating members.** The system rejects valid emails but accepts some invalid emails, directly affecting member creation and data quality.

#### REQ-08 - Borrow/Return Records

**High**
- **BUG-07 - Members can view tickets belonging to other members.** This is a privacy and access-control issue because members can access borrow-ticket information that does not belong to them.

**Cross-related issue**
- **BUG-05** also affects REQ-08 because a member can not only view another member's record but also perform the return action on that record.

---

## 5. Bug Fix Priority Recommendation

The priority is based on severity, impact on business rules, security/privacy risk, data-integrity impact, and how essential the affected function is.

| Priority | Bug | Severity | Reason |
|----------|-----|----------|--------|
| 1 | BUG-07 | High | Members can view borrow tickets belonging to other members, causing data exposure and violating access control. |
| 2 | BUG-05 | High | Members can return books borrowed by other users, causing unauthorized changes to borrow records and book status. |
| 3 | BUG-03 | High | The maximum limit of 3 borrowed books is an important business rule, but the system still allows members to borrow beyond the limit. |
| 4 | BUG-06 | High | Incorrect email validation blocks valid members and allows invalid data into the system. |
| 5 | BUG-02 | High | Mixing up between suspension and expiration violates the business rule. |
| 6 | BUG-04 | Medium | Missing overdue warnings violate business rules and may mislead users during overdue returns. |
| 7 | BUG-01 | Medium | Category filtering is not case-insensitive, violating the SRS and creating inconsistent search behavior. |

After fixing High and Medium severity bugs, the team should retest at least the related test cases: TC-03-06, TC-04-04, TC-04-06, TC-05-02, TC-05-03, TC-05-05, TC-07-01, TC-07-03, TC-07-06, and TC-08-03.

---

## 6. Conclusion

The system is **not ready for release** in its current state.

The test results show that several basic workflows are functional, especially viewing the book list, updating book status, basic search, valid book return, and overdue checking. However, the system still contains multiple issues that directly affect business rules and access control.

The most serious problems are related to members being able to view or modify other members' data, the borrow-limit rule not being enforced, incorrect email validation, and combined search not applying the required AND logic. These defects can cause data inconsistency, privacy concerns, and unreliable results for users.

The team recommends fixing all High and Medium severity bugs before release, then retesting the affected requirements. Observations and requirement gaps should also be clarified in the SRS so future testing can be evaluated against clear expected results.

---

## 7. Lessons Learned

- Input Domain Modeling helped the team identify input partitions, representative values, and boundary cases before writing test cases.
- Functions with multiple conditions, such as borrow book, return book, and combined search, should be designed with decision tables to reduce missed cases.
- Access control testing is critical for systems with multiple roles. Several serious issues were found only when testing with another user's data.
- Requirement ambiguity and requirement gaps should be separated from confirmed functional bugs to keep reporting fair and to support SRS improvement.
- Localization testing is not only about translating the interface; it also includes error messages, category/filter behavior, and language consistency across workflows.
- After fixing defects, the team should retest both the directly affected cases and related cases because many issues share validation, filtering, or authorization logic.

---

## 8. AI Usage Declaration

| AI Tool | Used For | How the Team Reviewed / Edited It |
|---------|----------|-----------------------------------|
| ChatGPT | Reviewing wording and summarizing content from test cases, test execution, and bug reports | The content was cross-checked against actual execution results and the bug list before being included in the summary. |
| Claude | Supporting ideas for IDM presentation, bug-report wording, and report structure | Suggestions were used only when they matched the team's actual testing results. |
| Gemini | Explaining testing concepts and supporting QA wording | The team applied the concepts manually and revised the wording according to the assignment context. |
| GitHub Copilot | Supporting spelling correction and document formatting | All suggested content was manually reviewed and edited before submission. |
