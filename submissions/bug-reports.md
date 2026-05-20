# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Tên nhóm -->` |
| **Ngày báo cáo** | `<!-- DD/MM/YYYY -->` |

---

## BUG-01

| Attribute | Details |
|---|---|
| Bug ID | BUG-01 |
| Related TC | TC-05-02, TC-05-03  |
| Related REQ | REQ-05, REQ-06 |
| Severity | Medium |
| Reported By | Vu Duc Quang |
| Date Found | 20/05/2026 |
| Status | Open |

**Title:** No overdue warning displayed when returning overdue books

### Environment

- **Browser:** Chrome Version 148  
- **Operating System:** Windows 11  
- **Interface Language:** Vietnamese  

### Preconditions

- A member is logged into the system.
- The member has an active borrow record.
- The selected borrow record satisfies:
  - `returnDate >= dueDate`
  - The book has not been returned yet.

### Steps to Reproduce

1. Log in using a member account.
2. Open the **Borrow / Return** page.
3. Select a borrow record where `returnDate = dueDate`.
4. Click **Return Book**.
5. Observe the system response after the return action.

### Expected Result

The system should return the book successfully and display a **clear overdue warning**, because according to business rule **BR-05**:

> A book is considered overdue on the due date itself (including the exact due date).

Additionally:

- The book status should change to **"Available"**
- The borrow record status should change to **"Returned"**

### Actual Result

The system returned the book successfully:

- The book status changed to **"Available"**
- The borrow record status changed to **"Returned"**

However, **no overdue warning message was displayed** when `returnDate = dueDate`.

### Impact

This behavior violates business rules **BR-05 (Overdue)** and **BR-06 (Overdue Return Warning)**.

Users do not receive an overdue warning even though the system defines books returned on the due date as overdue. This creates inconsistent behavior with the specified business requirements.

### Evidence

#### Before Return

<a href="evidence/TC-05/TC-05-02-before-record.png">
  <img src="evidence/TC-05/TC-05-02-before-record.png" width="320">
</a>

#### After Return

<a href="evidence/TC-05/TC-05-02-after-return.png">
  <img src="evidence/TC-05/TC-05-02-after-return.png" width="320">
</a>

<a href="evidence/TC-05/TC-05-02-after-book.png">
  <img src="evidence/TC-05/TC-05-02-after-book.png" width="320">
</a>

### Suggested Fix

The system should display an overdue warning message when:

```text
returnDate >= dueDate

to ensure compliance with business rules **BR-05** and **BR-06**.

---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | `<!-- TC-xx -->` |
| **REQ liên quan** | `<!-- REQ-xx -->` |
| **Mức độ** | `<!-- High / Medium / Low -->` |
| **Người phát hiện** | `<!-- Họ tên thành viên -->` |
| **Ngày phát hiện** | `<!-- DD/MM/YYYY -->` |
| **Trạng thái** | `<!-- Open / Closed -->` |

**Tiêu đề:**
`<!-- Mô tả hành vi lỗi -->`

**Bước tái hiện:**
1. `<!-- -->`
2. `<!-- -->`
3. `<!-- -->`

**Kết quả mong đợi:**
`<!-- -->`

**Kết quả thực tế:**
`<!-- -->`

**Tác động:**
`<!-- -->`

**Minh chứng:**
`<!-- -->`

**Đề xuất xử lý:**
`<!-- -->`

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->
