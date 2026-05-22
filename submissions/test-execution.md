# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Tên nhóm -->` |
| **Ngày thực thi** | `<!-- DD/MM/YYYY -->` |
| **Trình duyệt** | Chrome `<!-- version -->` |
| **Hệ điều hành** | `<!-- Windows / macOS / Linux -->` |

---

## Kết quả chi tiết

| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Conclusion | Evidence | Bug |
|---|---|---|---|---|---|---|
| TC-05-01 | Return Book | Book is returned successfully. No overdue warning message is displayed. Book status changes to **"Available"**. Borrow record status changes to **"Returned"**. | Borrow record changed to **Returned**. Book status changed to **Available**. No overdue warning message displayed. | PASS | See evidence below | None |
## Evidence

### TC-05-01

#### Before Return

<table>
<tr>
<td align="center">
<b>Borrow Record</b><br>
<a href="evidence/TC-05/TC-05-01 before-record.png">
  <img src="evidence/TC-05/TC-05-01 before-record.png" width="320">
</a>
</td>

<td align="center">
<b>Book Status</b><br>
<a href="evidence/TC-05/TC-05-01 before-book.png">
  <img src="evidence/TC-05/TC-05-01 before-book.png" width="320">
</a>
</td>
</tr>
</table>

#### After Return

<table>
<tr>
<td align="center">
<b>Borrow Record Updated</b><br>
<a href="evidence/TC-05/TC-05-01 after-return.png">
  <img src="evidence/TC-05/TC-05-01 after-return.png" width="320">
</a>
</td>

<td align="center">
<b>Book Status Updated</b><br>
<a href="evidence/TC-05/TC-05-01 after-book.png">
  <img src="evidence/TC-05/TC-05-01 after-book.png" width="320">
</a>
</td>
</tr>
</table>

---

## TC-05-02 

| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Conclusion | Evidence | Bug |
|---|---|---|---|---|---|---|
| TC-05-02 | Return Book | Book is returned successfully. System displays a clear overdue warning. Book status changes to **"Available"**. Borrow record status changes to **"Returned"**. | Book was returned successfully and the record/book status was updated, but no overdue warning message was displayed when `returnDate = dueDate`. | FAIL | See evidence below | BUG-01 |

### Evidence — TC-05-02

#### Before Return

<table>
<tr>
<td align="center">
<b>Borrow Record</b><br>
<a href="evidence/TC-05/TC-05-02-before-record.png">
  <img src="evidence/TC-05/TC-05-02-before-record.png" width="320">
</a>
</td>
</tr>
</table>

#### After Return

<table>
<tr>
<td align="center">
<b>Borrow Record Returned — No Overdue Warning</b><br>
<a href="evidence/TC-05/TC-05-02-after-return.png">
  <img src="evidence/TC-05/TC-05-02-after-return.png" width="320">
</a>
</td>

<td align="center">
<b>Book Status Available</b><br>
<a href="evidence/TC-05/TC-05-02-after-book.png">
  <img src="evidence/TC-05/TC-05-02-after-book.png" width="320">
</a>
</td>
</tr>
</table>

## TC-05-03

| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Conclusion | Evidence | Bug |
|---|---|---|---|---|---|---|
| TC-05-03 | Return Book | Book is returned successfully. System displays a clear overdue warning. Book status changes to **"Available"**. Borrow record status changes to **"Returned"**. | Book was returned successfully and the record/book status was updated, but no overdue warning message was displayed for an overdue return (`returnDate > dueDate`). | FAIL | See evidence TC-05-02 | BUG-01 |

## TC-05-04

| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Conclusion | Evidence | Bug |
|---|---|---|---|---|---|---|
| TC-05-04 | Return Book | System does not allow returning a book that has already been returned. The **Return Book** button is not displayed or cannot be used. Book status remains **"Available"**. | The borrow record remained in **"Returned"** status. The **Return Book** button was no longer displayed after the book had been returned, preventing duplicate return actions. | PASS | See evidence below | None |

### Evidence — TC-05-04

#### Returned Record — No Return Action

<table>
<tr>
<td align="center">
<b>Returned Record (No Return Button)</b><br>
<a href="evidence/TC-05/TC-05-04 before-return.png">
  <img src="evidence/TC-05/TC-05-04 before-return.png" width="320">
</a>
</td>

<td align="center">
<b>Book Status Available</b><br>
<a href="evidence/TC-05/TC-05-04 after-return.png">
  <img src="evidence/TC-05/TC-05-04 after-return.png" width="320">
</a>
</td>
</tr>
</table>


#### Borrow Records Visibility

<table>
<tr>
<td align="center">
<b>MEM002 Borrow Records Only</b><br>
<a href="evidence/TC-05/TC-05-04-own-records.png">
  <img src="evidence/TC-05/TC-05-04-own-records.png" width="320">
</a>
</td>

<td align="center">
<b>No Access to Other Members' Records</b><br>
<a href="evidence/TC-05/TC-05-04-no-other-records.png">
  <img src="evidence/TC-05/TC-05-04-no-other-records.png" width="320">
</a>
</td>
</tr>
</table>

## Tổng hợp kết quả 

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `<!-- số -->` |
| Pass | `<!-- số -->` |
| Fail | `<!-- số -->` |
| Blocked | `<!-- số -->` |
| Not Run | `<!-- số -->` |
| **Tỷ lệ Pass** | `<!-- xx% -->` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| | | | | |
