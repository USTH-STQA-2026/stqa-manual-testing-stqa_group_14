# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | Group 14 |
| **Ngày thực thi** | `<!-- DD/MM/YYYY -->` |
| **Trình duyệt** | Chrome `<!-- version -->` |
| **Hệ điều hành** | `<!-- Windows / macOS / Linux -->` |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-04-01 | Borrow Book | Member can borrow the book, successful message displayed in corresponding language| Member can borrow the book, successful message displayed in corresponding language | Pass | <a href="evidence/TC-04-01/BOOK001_before.png">Before borrowing BOOK001</a><br><a href="evidence/TC-04-01/BOOK001_after_vi.png">After borrowing BOOK001 (Vietnamese)</a><br><a href="evidence/TC-04-01/BOOK001_after_en.png">After borrowing BOOK001 (English)</a><br><a href="evidence/TC-04-01/BR_before.png">Borrow records before borrowing</a><br><a href="evidence/TC-04-01/BR_after.png">Borrow records after borrowing</a> | None |
| TC-04-02 | Borrow Book | Member cannot borrow the book | Member cannot borrow the book | Pass | <a href="evidence/TC-04-02/BOOK003_before.png">Before borrowing BOOK003</a><br><a href="evidence/TC-04-02/BOOK003_after.png">After borrowing BOOK003</a><br><a href="evidence/TC-04-02/BR_before.png">Borrow records before borrowing</a><br><a href="evidence/TC-04-02/BR_after.png">Borrow records after borrowing</a> | None |
| TC-04-03 | Borrow Book | Member cannot borrow the book | Member cannot borrow the book | Pass | <a href="evidence/TC-04-03/BOOK007_before.png">Before borrowing BOOK007</a><br><a href="evidence/TC-04-03/BOOK007_after.png">After borrowing BOOK007</a><br><a href="evidence/TC-04-03/BR_before.png">Borrow records before borrowing</a><br><a href="evidence/TC-04-03/BR_after.png">Borrow records after borrowing</a> | None |
| TC-04-04 | Borrow Book | - Member cannot borrow the book<br>- Error message on member being suspended is displayed in corresponding language | - Member cannot borrow the book<br>- Error message says the member has expired<br>- Error message is Vietnamese while display language is English | Fail | <a href="evidence/TC-04-04/BOOK001_before.png">Before borrowing BOOK001</a><br><a href="evidence/TC-04-04/BOOK001_after_vi.png">After borrowing BOOK001 (Vietnamese)</a><br><a href="evidence/TC-04-04/BOOK001_after_en.png">After borrowing BOOK001 (English)</a><br><a href="evidence/TC-04-04/BR_before.png">Borrow records before borrowing</a><br><a href="evidence/TC-04-03/BR_after.png">Borrow records after borrowing</a> | BUG-04-03, BUG-04-07 |
| TC-04-05 | Borrow Book | - Member cannot borrow the book<br>- Error message on member having expired is displayed in corresponding language | - Member cannot borrow the book<br>- Error message says the member has expired<br>- Error message is Vietnamese while display language is English | Fail | <a href="evidence/TC-04-05/BOOK001_before.png">Before borrowing BOOK001</a><br><a href="evidence/TC-04-05/BOOK001_after_vi.png">After borrowing BOOK001 (Vietnamese)</a><br><a href="evidence/TC-04-05/BOOK001_after_en.png">After borrowing BOOK001 (English)</a><br><a href="evidence/TC-04-05/BR_before.png">Borrow records before borrowing</a><br><a href="evidence/TC-04-05/BR_after.png">Borrow records after borrowing</a> | BUG-04-07 |
| TC-04-06 | Borrow Book | - Member cannot borrow book BOOK005<br>- Error on limit having exceeded is displayed in corresponding language<br>- Borrow record is not created for BOOK005 | Member can borrow book BOOK005, no error message is displayed, borrow record for BOOK005 is created | Fail | <a href="evidence/TC-04-06/BOOK005_before.png">Before borrowing BOOK005</a><br><a href="evidence/TC-04-06/BOOK005_after.png">After borrowing BOOK005</a><br><a href="evidence/TC-04-06/BR_before.png">Borrow records before borrowing</a><br><a href="evidence/TC-04-06/BR_after.png">Borrow records after borrowing</a> | BUG-04-05 |
---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 6 |
| Pass | 3 |
| Fail | 3 |
| Blocked | 0 |
| Not Run | 0 |
| **Tỷ lệ Pass** | 50% |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| Borrow Book | 6 | 3 | 3 | 50% |

