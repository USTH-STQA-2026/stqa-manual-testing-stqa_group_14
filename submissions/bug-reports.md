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
| Related REQ | REQ-05 |
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
3. Select a borrow record where `returnDate >= dueDate`.
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

However, **no overdue warning message was displayed** when `returnDate >= dueDate`.

### Impact

This behavior violates business rules **BR-05 (Overdue)** and **BR-06 (Overdue Return Warning)**.

Users do not receive an overdue warning even though the system defines books returned on the due date as overdue. This creates inconsistent behavior with the specified business requirements.

### Evidence

#### Before Return

<a href="evidence/TC-05/TC-05-02-before-record.png">
  <img src="evidence/TC-05/TC-05-02-before-record.png">
</a>

#### After Return

<a href="evidence/TC-05/TC-05-02-after-return.png">
  <img src="evidence/TC-05/TC-05-02-after-return.png" >
</a>
----------
<a href="evidence/TC-05/TC-05-02-after-book.png">
  <img src="evidence/TC-05/TC-05-02-after-book.png">
</a>

### Suggested Fix

The system should display an overdue warning message when:

```text
returnDate >= dueDate
```
to ensure compliance with business rules **BR-05** and **BR-06**.
---


## BUG-02

| Attribute | Details |
|---|---|
| Bug ID | BUG-02 |
| Related TC | TC-05-05 |
| Related REQ | REQ-05, REQ-08 |
| Severity | High |
| Reported By | Vu Duc Quang |
| Date Found | 27/05/2026 |
| Status | Open |

**Title:** Member can return books borrowed by another member

### Environment

- **Browser:** Chrome Version 148  
- **Operating System:** Windows 11  
- **Interface Language:** Vietnamese  

### Preconditions

- A member account is logged into the system.
- Another member has an active borrow record.
- The borrow record does not belong to the currently logged-in member.

### Steps to Reproduce

1. Log in using a member account (e.g. `dam.tran@email.com` / MEM003).
2. Open the **Borrow / Return** page.
3. Locate or select an active borrow record belonging to another member (e.g. MEM002).
4. Click **Return Book** on that borrow record.
5. Observe the system response and record status.

### Expected Result

The system must **not allow** a member to return another member’s borrowed book.

Additionally:

- Borrow records belonging to other members should **not be visible or accessible** for return actions.
- The **Return Book** button should not be displayed or should be disabled for unauthorized records.
- The borrow record status must remain unchanged.
- The book status must remain unchanged.

### Actual Result

The logged-in member was able to access and return a book borrowed by another member.

As a result:

- The borrow record status was updated even though the record did not belong to the current member.
- The book status changed despite unauthorized access.

### Impact

This behavior violates **access control and data ownership rules**.

Members are able to manipulate borrow records that belong to other users, which may lead to:

- Unauthorized modifications of borrowing history
- Incorrect book availability status
- Data integrity issues
- Privacy and security concerns

### Evidence

#### Before Unauthorized Return

Logged in as **MEM003 (Trần Dựa Dẫm)**, but the system displayed borrow records belonging to **MEM002 (Nguyễn Học Bá)** and still allowed the **"Trả sách"** action.

<a href="evidence/TC-05/TC-05-05-before-record.png">
  <img src="evidence/TC-05/TC-05-05-before-record.png">
</a>

#### After Unauthorized Return

While logged in as **MEM003 (Trần Dựa Dẫm)**, the system successfully returned a borrow record belonging to **MEM002 (Nguyễn Học Bá)**. The record status changed to **"Đã trả"**, confirming unauthorized access and modification.

<a href="evidence/TC-05/TC-05-05-after-return.png">
  <img src="evidence/TC-05/TC-05-05-after-return.png">
</a>