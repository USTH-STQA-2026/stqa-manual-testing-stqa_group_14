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

## REQ-05 — Return Book

| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Conclusion | Evidence | Bug |
|---|---|---|---|---|---|---|
| TC-05-01 | Return Book | Book is returned successfully. No overdue warning message is displayed. Book status changes to **"Available"**. Borrow record status changes to **"Returned"**. | Borrow record changed to **"Returned"**. Book status changed to **"Available"**. No overdue warning message was displayed. | PASS | N/A | None |
| TC-05-02 | Return Book | Book is returned successfully. System displays a clear overdue warning. Book status changes to **"Available"**. Borrow record status changes to **"Returned"**. | Book was returned successfully and the record/book status was updated, but no overdue warning message was displayed when `returnDate = dueDate`. | FAIL | See BUG-01 | BUG-01 |
| TC-05-03 | Return Book | Book is returned successfully. System displays a clear overdue warning. Book status changes to **"Available"**. Borrow record status changes to **"Returned"**. | Book was returned successfully and the record/book status was updated, but no overdue warning message was displayed for an overdue return (`returnDate > dueDate`). | FAIL | See BUG-01 | BUG-01 |
| TC-05-04 | Return Book | System does not allow returning a book that has already been returned. The **Return Book** button is not displayed or cannot be used. Book status remains **"Available"**. Borrow record status remains **"Returned"**. | The borrow record remained in **"Returned"** status. The **Return Book** button was no longer displayed after the book had been returned, preventing duplicate return actions. Book status remained **"Available"**. | PASS | N/A | None |





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
