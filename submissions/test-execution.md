# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | Group 14 |
| **Ngày thực thi** | 20/05/2026 |
| **Trình duyệt** | Chrome `<!-- version 142.0.7444.176 -->` |
| **Hệ điều hành** | `<!-- Windows 10 -->` |

---

## Kết quả chi tiết

| Mã TC (TC ID) | Nhóm chức năng (Feature group) | Kết quả mong đợi (tóm tắt) (Expected result (summary)) | Kết quả thực tế (Actual result) | Kết luận (Conclusion) | Minh chứng (Evidence) | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-01 | Search by title/author | Display 1 book: BOOK001 (baseline for TC-05) | Display BOOK001 | Pass | | - |
| TC-02 | As above | Display 2 books: BOOK001, BOOK009 | Display BOOK001, 009 | Pass | | - |
| TC-03 | As above | Display "No books found" | Display "No books found" |  Pass | | - |
| TC-04 | Filter by category | Display 8 books in Technology: BOOK001, 002, 003, 005, 008, 009, 010, 011 (baseline for TC-06) | Display BOOK001, 002, 003, 005, 008, 009, 010, 011 | Pass | | - |
| TC-05 | Case sensitivity — title/author bar | Display 1 book: BOOK001 for both `"flutter"` and `"FLUTTER"` (same as TC-01) | Display BOOK001 for both inputs | Pass | | - |
| TC-06 | Case sensitivity — category bar | Display 8 books for both `"công nghệ"` and `"CÔNG NGHỆ"` (same as TC-04) | Display "No books found", blank list for both inputs | Fail | TC-06_BUG-01_ lowercase.png, TC-06_BUG-01_uppercase.png | BUG-01 |
| TC-07 | Diacritic sensitivity — both bars | Display 2 books: BOOK001, BOOK009 (Step 3 - same as TC-02). Display 8 books: BOOK001, 002, 003, 005, 008, 009, 010, 011 (Step 7 - same as TC-04) | Display "No books found", blank list | Observed/TBD | TC-07_author-without-diacritics.png, TC-07_genre-without-diacritics.png | - |
| TC-08 | Partial keyword — title/author bar | Display 4 books whose author contains "Nguyễn": BOOK001, 006, 009, 016 | Display BOOK001, 006, 009, 016 | Pass | | - |
| TC-09 | Partial keyword — category bar | Display 8 books whose genre contains "Công": BOOK001, 002, 003, 005, 008, 009, 010, 011 | Display "No books found", blank list | Fail | TC-09_BUG-02.png | BUG-02 |
| TC-10 | Empty fields | Display all 20 books | Display all 20 books | Pass | | - |
| TC-11 | Combined search - match| Display 2 books: BOOK001, BOOK009 | (1) If keyword entered first then category — display 8 Technology books: BOOK001, 002, 003, 005, 008, 009, 010, 011 (category overrides keyword); (2) If category entered first then keyword — display 2 books: BOOK001, BOOK009 (keyword overrides category) | Fail | TC-11_BUG-03_author-first_1.png, TC-11_BUG-03_author-first_2.png, TC-11_BUG-03_author-first_3.png, TC-11_BUG-03_genre-first.png | BUG-03 |
| TC-12 | Combined search - mismatch | Display "No books found" | (1) If keyword entered first then category — display 3 Economics books: BOOK007, BOOK014, BOOK015 (category overrides keyword); (2) If category entered first then keyword — display 2 books: BOOK001, BOOK009 (keyword overrides category); | Fail | TC-12_BUG-03_author-first.png, TC-12_BUG-03_genre-first.png | BUG-03 |
---

## Tổng hợp kết quả

| Chỉ số (Metric) | Giá trị (Value) |
|--------|---------|
| Tổng số test case (Total TC) | 12 |
| Pass | 7 |
| Fail | 4 |
| Blocked | 0 |
| Not Run | 0 |
| Observed | 1 |
| **Tỷ lệ Pass (Pass rate)** | 63.6% |

### Kết quả theo nhóm chức năng

| Nhóm (Group) | Tổng TC (Total TC) | Pass | Fail | Tỷ lệ Pass (Pass rate) |
|------|---------|------|------|------------|
| Search by title/author | 3 | 3 | 0 | 100% |
| Filter by category | 1 | 1 | 0 | 100% |
| Case sensitivity | 2 | 1 | 1 | 50% |
| Diacritic sensitivity | 1 | 0 | 0 | N/A |
| Partial keyword | 2 | 1 | 1 | 50% |
| Empty fields | 1 | 1 | 0 | 100% |
| Combined search | 2 | 0 | 2 | 0% |
