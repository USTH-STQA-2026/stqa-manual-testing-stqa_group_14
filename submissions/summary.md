# Test Summary — Báo cáo tổng hợp kiểm thử

> **Hướng dẫn**: Đây là hoạt động **Quality Assurance** — bạn đánh giá chất lượng tổng thể của phần mềm, không chỉ liệt kê lỗi.

---

## 1. Thông tin nhóm

| Mục | Thông tin |
|-----|----------|
| **Nhóm** | `<!-- Tên nhóm -->` |
| **Lớp** | `<!-- VD: SE001.P11 -->` |
| **Ngày báo cáo** | `<!-- DD/MM/YYYY -->` |
| **Hệ thống kiểm thử** | https://stqa.rbc.vn — v1.0 |

---

## 2. Overall Test Results

| Metric | Value |
|--------|---------|
| Total Test Cases | 9 |
| Pass | 7 |
| Fail | 2 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass Rate** | 77.78% |
| **Number of Bugs Found** | 1 |

### Distribution by Functional Group

| Functional Group | TC | Pass | Fail | Bug | Assessment |
|---------------|-----|------|------|-----|---------|
| Return Book (REQ-05) | 4 | 2 | 2 | 1 | Partially Passed — Core return functionality worked correctly, but overdue warning behavior did not comply with business rules. |
| Overdue Handling (REQ-06) | 5 | 5 | 0 | 0 | Passed — Overdue checking function worked correctly in all tested scenarios. |

### Bug Distribution by Severity

| Severity | Quantity | Bug IDs |
|--------|---------|---------|
| High | 0 | None |
| Medium | 1 | BUG-01 |
| Low | 0 | None |

---

## 3. Test Design Techniques Used

| Technique | Applied to REQ | Number of TCs | Application Description |
|----------|---------------------|---------------|------------------------|
| Equivalence Partitioning (EP) | REQ-05, REQ-06 | 7 | Input conditions were divided into different partitions such as overdue/non-overdue records, librarian/member permissions, and active/returned borrow records. |
| Boundary Value Analysis (BVA) | REQ-05, REQ-06 | 5 | Boundary conditions around due dates were tested, especially `currentDate = dueDate`, to verify system behavior at critical limits. |

---

## 4. Software Quality Analysis

### 4.1. Strengths

- The **Return Book** feature correctly updated the book status to **"Available"** and borrow record status to **"Returned"** after successful returns.
- The system successfully prevented duplicate return actions for books that had already been returned.
- The **Check Overdue** feature worked correctly for all tested date conditions (`before`, `on`, and `after` due date).
- Access control for overdue checking was implemented correctly: librarians had permission while members did not.

### 4.2. Weaknesses

- The system failed to display an overdue warning when returning overdue books (`returnDate >= dueDate`), causing inconsistency with business rules **BR-05** and **BR-06**.
- Overdue return behavior was inconsistent between **REQ-05** and **REQ-06**, since overdue detection worked correctly in overdue checking but failed during the return process.

---

## 5. Recommended Bug Fix Priority

| Priority | Bug | Severity | Reason for Priority |
|--------|-----|--------|---------------|
| 1 | BUG-01 | Medium | This bug violates business rules related to overdue handling and creates inconsistent system behavior. Although the return process succeeds, users do not receive the required overdue warning. |

---

## 6. Conclusion

The system performed well for most tested scenarios in **REQ-05** and **REQ-06**, achieving a **77.78% pass rate**. Core functionalities such as returning books, updating statuses, overdue checking, and permission control operated correctly.

However, the system is **not fully ready for release** because **BUG-01** violates business rules regarding overdue warnings. The issue should be fixed before deployment to ensure consistency and compliance with system requirements.

---

## 7. Bài học rút ra (Tùy chọn)

`<!-- Nhóm bạn học được gì từ quá trình kiểm thử này? -->`

---

## 8. Khai báo sử dụng AI (Tùy chọn)

| AI Tool | Used For | Verification / Modification |
|------------|-------------------|-----------------------------------|
| ChatGPT | Grammar checking and wording improvement for test documentation | All test cases, executions, and reports were manually reviewed and adjusted based on the actual testing results. |
