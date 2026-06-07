# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | Group 14 |
| **Ngày báo cáo** | `<!-- DD/MM/YYYY -->` |

---

## BUG-04-03

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-04-03 |
| **TC liên quan** | TC-04-04 |
| **REQ liên quan** | REQ-04 |
| **Mức độ** | High |
| **Người phát hiện** | Trần Thị Thu Trang |
| **Ngày phát hiện** | 23/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:** Error message says the member has expired while they are suspended

**Môi trường:**
- Trình duyệt: Chrome Version 148
- Hệ điều hành: Linux
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
1. Member can log in
2. Member has been suspended
3. Book is available
4. Member's borrow count is less than 3

**Bước tái hiện:**
1. Refresh the page
2. Log in to the account of MEM004
3.  Borrow the book BOOK001

**Kết quả mong đợi:**
- Member cannot borrow the book
- Display error message: member has been suspended
- Program state remains unchanged

**Kết quả thực tế:**
- Member cannot borrow the book
- Error message says the member has expired
- Program state remains unchanged

**Tác động:**
- Wrong cause of error is announced to the user, leading to confusion

**Severity explanation:** Mixing up between suspension and expiration violates the business rule, hence the severity is High

**Priority:** P1

**Minh chứng:**
<br><a href="evidence/TC-04-04/BOOK001_before.png">Before borrowing BOOK001</a><br><a href="evidence/TC-04-04/BOOK001_after_vi.png">After borrowing BOOK001</a><br><a href="evidence/TC-04-04/BR_before.png">Borrow records before borrowing</a><br><a href="evidence/TC-04-04/BR_after.png">Borrow records after borrowing</a>

**Đề xuất xử lý:**
Correct the error message to "member has been suspended"

---

## BUG-04-05

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-04-05 |
| **TC liên quan** | TC-04-06 |
| **REQ liên quan** | REQ-04 |
| **Mức độ** | High |
| **Người phát hiện** | Trần Thị Thu Trang |
| **Ngày phát hiện** | 23/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:** Users can still borrow a book when their borrow count is 3

**Môi trường:**
- Trình duyệt: Chrome Version 148
- Hệ điều hành: Linux
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:**
1. Member can log in
2. Member is active
3. Book is available
4. Member's borrow count is 3

**Bước tái hiện:**
1. Refresh the page
2. Log in to the account of MEM002
3. Borrow the book BOOK001
4. Borrow the book BOOK002
5. Borrow the book BOOK005 

**Kết quả mong đợi:**
 - Member cannot borrow the book BOOK005
 - BOOK005 remains available
 - Display error message when borrowing BOOK005 in corresponding display language: borrow limit reached
 - Borrow records for that member and books BOOK001 and BOOK002 are created, due date is 14 days later after today, no record created for BOOK005


**Kết quả thực tế:**
Member can borrow book BOOK005, no error message is displayed, borrow record for BOOK005 is created

**Tác động:**
This violates the business requirement of only allowing to borrow up to 3 books at a time

**Severity explanation:** Letting a member borrow more than 3 books violates the business rule, hence the severity is High

**Priority:** P1

**Minh chứng:**
<br><a href="evidence/TC-04-06/BOOK005_before.png">Before borrowing BOOK005</a><br><a href="evidence/TC-04-06/BOOK005_after.png">After borrowing BOOK005</a><br><a href="evidence/TC-04-06/BR_before.png">Borrow records before borrowing</a><br><a href="evidence/TC-04-06/BR_after.png">Borrow records after borrowing</a>

**Đề xuất xử lý:**
Recheck the condition checking whether the user has reached the borrow limit.

---

## BUG-04-07

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-04-07 |
| **TC liên quan** | TC-04-04, TC-04-05 |
| **REQ liên quan** | REQ-04 |
| **Type** | Failure |
| **Mức độ** | Low |
| **Người phát hiện** | Trần Thị Thu Trang |
| **Ngày phát hiện** | 23/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**  Error messages are in Vietnamese while display language is English

**NOTE:**
- Merge this with other language-related failures in other REQs
- TC-04-07 has been DELETED. Do NOT include this in the final version

**Môi trường:**
- Trình duyệt: Chrome Version 148
- Hệ điều hành: Linux
- Ngôn ngữ giao diện: Tiếng Việt

**Điều kiện tiên quyết:** Refer to each individual test case mentioned below

**Bước tái hiện:**
1. Recreate the BUG-03, set display language to English after step 2
2. Perform TC-04-04:
	1. Refresh the page
	2. Log in to the account of MEM005
	3. Set display language to English
	4. Borrow the book BOOK001
3. Perform these steps (extra case):
	1. Refresh the page
	2. Log in to the account of MEM002
	3. Set display language to English
	4. Borrow the book BOOK001
	5. Borrow the book BOOK002
	6. Borrow the book BOOK005
	7. Borrow the book BOOK008



**Kết quả mong đợi:**
Error messages are in English


**Kết quả thực tế:**
Error messages are in Vietnamese

**Tác động:**
Users who do not know Vietnamese can be confused

**Minh chứng:**
<br><a href="evidence/TC-04-04/BOOK001_after_en.png">TC-04-04: After borrowing BOOK001 (English)</a><br><a href="evidence/TC-04-05/BOOK001_after_en.png">TC-04-05: After borrowing BOOK001 (English)</a><br><a href="evidence/TC-04-07/BOOK008_after_en.png">Extra case: After borrowing BOOK008 (English)</a>

**Đề xuất xử lý:**
Correct the error messages to the English version when the display language is English

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->
