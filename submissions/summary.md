## 2. Overall Test Results

| Metric | Value |
|--------|---------|
| Total Test Cases | 10 |
| Pass | 7 |
| Fail | 3 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass Rate** | 70.00% |
| **Number of Bugs Found** | 2 |

### Distribution by Functional Group

| Functional Group | TC | Pass | Fail | Bug | Assessment |
|---------------|-----|------|------|-----|---------|
| Return Book (REQ-05) | 5 | 2 | 3 | 2 | Partially Passed — Core return functionality worked, but overdue warning behavior and access control did not comply with business requirements. |
| Overdue Handling (REQ-06) | 5 | 5 | 0 | 0 | Passed — Overdue checking function worked correctly in all tested scenarios. |

### Bug Distribution by Severity

| Severity | Quantity | Bug IDs |
|--------|---------|---------|
| High | 1 | BUG-02 |
| Medium | 1 | BUG-01 |
| Low | 0 | None |

---

## 3. Test Design Techniques Used

| Technique | Applied to REQ | Number of TCs | Application Description |
|----------|---------------------|---------------|------------------------|
| Equivalence Partitioning (EP) | REQ-05, REQ-06 | 8 | Input conditions were divided into different partitions such as overdue/non-overdue records, librarian/member permissions, record ownership, and active/returned borrow records. |
| Boundary Value Analysis (BVA) | REQ-05, REQ-06 | 5 | Boundary conditions around due dates were tested, especially `currentDate = dueDate`, to verify system behavior at critical limits. |
| Negative Testing | REQ-05 | 2 | Unauthorized and invalid return scenarios were tested, including returning books already returned and attempting to return another member’s borrowed book. |

---

## 4. Software Quality Analysis

### 4.1. Strengths

- The **Return Book** feature correctly updated the book status to **"Available"** and borrow record status to **"Returned"** after successful returns.
- The system successfully prevented duplicate return actions for books that had already been returned.
- The **Check Overdue** feature worked correctly for all tested date conditions (`before`, `on`, and `after` due date).
- Access control for overdue checking was implemented correctly: librarians had permission while members did not.

### 4.2. Weaknesses

- The system failed to display an overdue warning when returning overdue books (`returnDate >= dueDate`), causing inconsistency with overdue-return requirements.
- Overdue return behavior was inconsistent between **REQ-05** and **REQ-06**, since overdue detection worked correctly in overdue checking but failed during the return process.
- The system allowed a logged-in member to return books borrowed by another member, violating access control and borrow-record ownership rules.
- Unauthorized return actions could modify book and borrow-record statuses, creating risks to data integrity and user privacy.

---

## 5. Recommended Bug Fix Priority

| Priority | Bug | Severity | Reason for Priority |
|--------|-----|--------|---------------|
| 1 | BUG-02 | High | This bug violates access control rules by allowing members to manipulate borrow records belonging to other users. It may cause unauthorized modifications, incorrect borrowing history, and data integrity issues. |
| 2 | BUG-01 | Medium | This bug causes inconsistent overdue handling behavior and violates overdue warning requirements, but does not block the core return process. |

---

## 6. Conclusion

The system showed acceptable performance in **REQ-05** and **REQ-06**, achieving a **70.00% pass rate**. Core functionalities such as updating return status, preventing duplicate returns, overdue checking, and overdue-access permissions generally worked as expected.

However, the system still contains important defects that should be resolved before release. In particular, **BUG-02** is a **high-severity access control issue**, allowing members to return books borrowed by other users. Additionally, **BUG-01** creates inconsistent overdue-return behavior by failing to display required overdue warnings.

Therefore, the system should **not yet be considered fully compliant with business requirements** until these issues are fixed.