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

## REQ-06 — Overdue Handling

| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Conclusion | Evidence | Bug |
|---|---|---|---|---|---|---|
| TC-06-01 | Overdue Handling | Librarian can access and use the **Check Overdue** function. Overdue borrow records are displayed or updated after checking. | The librarian account successfully accessed and used the **Check Overdue** function. Borrow records were updated and overdue records were displayed after checking. | PASS | N/A | None |
| TC-06-02 | Overdue Handling | Borrow record with `current date < dueDate` is **not marked as "Overdue"**. Status remains **"Borrowing"**. | The borrow record was **not marked as "Overdue"**. The status remained **"Borrowing"** after overdue checking. | PASS | N/A | None |
| TC-06-03 | Overdue Handling | Borrow record with `current date = dueDate` is marked as **"Overdue"**. `dueDate <= current date` is considered overdue. | The borrow record was successfully marked as **"Overdue"** when the due date matched the current date. | PASS | N/A | None |
| TC-06-04 | Overdue Handling | Borrow record with `current date > dueDate` is marked as **"Overdue"**. | The overdue borrow record was successfully marked as **"Overdue"** after overdue checking. | PASS | N/A | None |
| TC-06-05 | Overdue Handling | Member cannot access or use the **Check Overdue** function. The button is not displayed or cannot be used. Member cannot mark records as **"Overdue"**. | The member account could not access the **Check Overdue** function. The **Check Overdue** button was not displayed in the interface. | PASS | N/A | None |



## Summary of Results

| Metric | Value |
|--------|---------|
| Total Test Cases | 9 |
| Pass | 7 |
| Fail | 2 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass Rate** | 77.78% |

### Results by Functional Group

| Functional Group | Total TC | Pass | Fail | Pass Rate |
|------|---------|------|------|------------|
| Return Book (REQ-05) | 4 | 2 | 2 | 50% |
| Overdue Handling (REQ-06) | 5 | 5 | 0 | 100% |
| **Total** | **9** | **7** | **2** | **77.78%** |