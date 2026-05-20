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
