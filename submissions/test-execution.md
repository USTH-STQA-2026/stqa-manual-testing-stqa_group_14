# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Group 14 -->` |
| **Ngày thực thi** | `<!-- 20/05/2026 -->` |
| **Trình duyệt** | Chrome `<!-- version -->` |
| **Hệ điều hành** | `<!-- Windows / macOS / Linux -->` |

---

## Kết quả chi tiết

| Mã TC/TC ID | Nhóm chức năng (Feature group) | Kết quả mong đợi (tóm tắt) (Expected result (summary)) | Kết quả thực tế (Actual result) | Kết luận (Conclusion) | Minh chứng (Evidence) | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Search by title/author | Display 1 book: BOOK001 (baseline for TC) | Display BOOK001 | Pass | | |
| TC-02 | As above | Display 2 books: BOOK001, BOOK009 | Display BOOK001, 009 | Pass | | |
| TC-03 | As above | Display "Không tìm thấy sách" | Display "No books found |  Pass | | |
| TC-04 | Filter by category | Display 8 books in Technology: BOOK001, 002, 003, 005, 008, 009, 010, 011 (baseline) | Display BOOK001, 002, 003, 005, 008, 009, 010, 011 | Pass | | |
| TC-05 | Case sensitivity — keyword bar | Display 1 book: BOOK001 (same as TC-01) | Display BOOK001 | Pass | | |
| TC-06 | As above | Display 1 book: BOOK001 (same as TC-01) | Display BOOK001 | Pass | | |
| TC-07 | Case sensitivity — category bar | Display 8 books (same as TC-04) | Display "No books found", blank list | Fail | | BUG-01|
| TC-08 | As above | Display 8 books (same as TC-04) | Display "No books found", blank list | Fail | | BUG-02|
| TC-09 | Diacritic sensitivity — keyword bar | Display 2 books: BOOK001, BOOK009 (Same as TC-02) | Display "No books found", blank list | Observed/TBD | | - |
| TC-10 | Diacritic sensitivity — category bar | Display 8 books: BOOK001, 002, 003, 005, 008, 009, 010, 011 (Same as TC-04) | Display "No books found", blank list | Observed/TBD | | - |
| TC-11 | Partial keyword — keyword bar | Display 4 books: BOOK001, 006, 009, 016 | Display all 20 books | Fail | | BUG-03 |
| TC-12 | Partial keyword — category bar | Display 8 books: BOOK001, 002, 003, 005, 008, 009, 010, 011 | Display "No books found", blank list | Fail | | BUG-04 |
| TC-13 | Empty fields | Display all 20 books | Display all 20 books | Pass | | |
| TC-14 | Combined search | Display 2 books: BOOK008, BOOK011 | Display BOOK001, 002, 003, 005, 008, 009, 010, 011 | Fail | | BUG-05 |
| TC-15 | As above | Display "Không tìm thấy sách" | Display BOOK007, 014, 015 | Fail | | BUG-06 |
---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | `<!-- 15 -->` |
| Pass | `<!-- 7 -->` |
| Fail | `<!-- 6 -->` |
| Blocked | `<!-- 0 -->` |
| Not Run | `<!-- 0 -->` |
| Observed | `<!-- 2 -->` |
| **Tỷ lệ Pass** | `<!-- 54% -->` |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| Search by title/author | 3 | 3 | 0 | 100% |
| Filter by category | 1 | 1 | 0 | 100% |
| Case sensitivity | 4 | 2 | 2 | 50% |
| Diacritic sensitivity | 2 | 0 | 0 | N/A |
| Partial keyword | 2 | 0 | 2 | 0% |
| Empty fields | 1 | 1 | 0 | 100% |
| Combined search | 2 | 0 | 2 | 0% |
