# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.
## BUG-07

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-07 |
| **TC liên quan** | TC-01 |
| **REQ liên quan** | REQ-07 |
| **Mức độ** | High |
| **Người phát hiện** | Hoàng Hải Minh |
| **Ngày phát hiện** | 12/5/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
System rejects valid email but accepts invalid email when creating a new member

**Môi trường:**
- Trình duyệt: Chrome
- Hệ điều hành: Windows 10
- Ngôn ngữ giao diện: English

**Điều kiện tiên quyết:**
Log in using librarian account (librarian@library.com / admin123)

**Bước tái hiện:**
1. Get in tab member
2. Navigate to the **Add New Member** page.
3. Enter valid member information, including a valid email format (e.g., `newmember@gmail.com`).
4. Click **Submit**.
5. Observe the system response.
6. Repeat the process using an invalid email format (e.g., `whoisthis@idontknow`).

**Kết quả mong đợi:**
New member successfully created, appears in list (REQ-07: valid input → created successfully)

**Kết quả thực tế:**
Valid input --> Error message " Email invalid ", 
Invalid input --> Created succesfully

**Tác động:**
Loss of new members, poor user experience, damage to reputation, allows invalid data to be stored in the system database.

**Severity explanation:**
- High because this bug prevents valid users from being created while still allowing invalid entries, which breaks core member registration flow and undermines data integrity.

**Minh chứng:**
- ![TC-01 REQ-07](Evidences/REQ-07/TC-01%20REQ-07%20BUG.png)
- ![TC-02 REQ-07](Evidences/REQ-07/TC-02%20REQ-07%20BUG.png)
- ![TC-06 REQ-07](Evidences/REQ-07/TC-06%20REQ-07%20BUG.png)

**Đề xuất xử lý:**
Review and fix the email validation logic in the member creation form, ensure valid email formats are accepted and invalid formats are rejected correctly
---

## BUG-08

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-08 |
| **TC liên quan** | TC-09 |
| **REQ liên quan** | REQ-08 |
| **Mức độ** | High |
| **Người phát hiện** | Hoàng Hải Minh |
| **Ngày phát hiện** | 12/5/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
Member can view other members' tickets (privacy breach)

**Môi trường:**
- Trình duyệt: Chrome
- Hệ điều hành: Windows 10
- Ngôn ngữ giao diện: English

**Điều kiện tiên quyết:**
Log in MEM002 (ba.nguyen) — another member is MEM003 (dam.tran) with BR002

**Bước tái hiện:**
1. Log in to MEM002
2. Go to the Borrow/Return tab
3. Enter/look up the ID of MEM003

**Kết quả mong đợi:**
Tickets for MEM003 are not displayed — or the search function by other IDs is unavailable (REQ-08: Tickets of other members cannot be viewed)

**Kết quả thực tế:**
Tickets for MEM003 are displayed

**Tác động:**
Data privacy breach

**Severity explanation:**
- High because the issue exposes other members' ticket data, creating a serious privacy breach and potential compliance violation.

**Minh chứng:**
- ![TC-09 REQ-08](Evidences/REQ-08/TC-09%20REQ-08%20BUG.png)

**Đề xuất xử lý:**
Server-side / data-layer filtering, improve UI-layer enforcement
