# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | Group 14 |
| **Ngày thực thi** | 20/05/2026 |
| **Trình duyệt** | Chrome version 142.0.7444.176 |
| **Hệ điều hành** | Windows 10 |

---

## Kết quả chi tiết

| Mã TC (TC ID) | Nhóm chức năng (Feature group) | Kết quả mong đợi (tóm tắt) (Expected result (summary)) | Kết quả thực tế (Actual result) | Kết luận (Conclusion) | Minh chứng (Evidence) | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----| 
| TC-03-01 | Search by title/author | Display 1 book: BOOK001 | Display BOOK001 | Pass | | - |
| TC-03-02 | As above | Display 2 books: BOOK001, BOOK009 | Display BOOK001, BOOK009 (baseline for TC-03-05) | Pass | | - |
| TC-03-03 | Filter by category | Display 8 books in Technology: BOOK001, 002, 003, 005, 008, 009, 010, 011 (baseline for TC-03-06) | Display BOOK001, 002, 003, 005, 008, 009, 010, 011 | Pass | | - |
| TC-03-04 | Both bars | Display "No books found" | Display "No books found" |  Pass | | - |
| TC-03-05 | Case sensitivity - title/author bar | Display 1 book: BOOK001 for both `"nguyễn minh đức"` and `"NGUYỄN MINH ĐỨC"` (same as TC-03-02) | Display BOOK001 for both inputs | Pass | | - |
| TC-03-06 | Case sensitivity - category bar | Display 8 books for both `"công nghệ"` and `"CÔNG NGHỆ"` (same as TC-03-03) | Display "No books found", blank list for both inputs | Fail | [TC-03-06 lowercase](evidence/TC-03-06_BUG-01_lowercase.png), [TC-03-06 uppercase](evidence/TC-03-06_BUG-01_uppercase.png) | BUG-01 |
| TC-03-07 | Diacritic sensitivity - title/author bar | Display 2 books: BOOK001, BOOK009 (same as TC-03-02). | Display "No books found", blank list | Observed/TBD | [TC-03-07](evidence/TC-03-07_OBS-01_author-without-diacritics.png) | - |
| TC-03-08 | Diacritic sensitivity - category bars | Display 8 books: BOOK001, 002, 003, 005, 008, 009, 010, 011 (same as TC-03-04) | Display "No books found", blank list | Observed/TBD | [TC-03-08](evidence/TC-03-08_OBS-01_genre-without-diacritics.png) | - |
| TC-03-09 | Partial keyword - title/author bar | Display 4 books whose author contains "Nguyễn": BOOK001, 006, 009, 016 | Display BOOK001, 006, 009, 016 | Observed/TBD | | - |
| TC-03-10 | Partial keyword - category bar | Display 8 books whose category contains "Công": BOOK001, 002, 003, 005, 008, 009, 010, 011 | Display "No books found", blank list | Observed/TBD | [TC-03-10](evidence/TC-03-10_OBS-02.png) | - |
| TC-03-11 | Empty fields | Display all 20 books | Display all 20 books | Pass | | - |
| TC-03-12 | Combined search - match| Display 2 books: BOOK001, BOOK009 | (1) If keyword entered first then category - display 8 Technology books: BOOK001, 002, 003, 005, 008, 009, 010, 011 (category overrides keyword); (2) If category entered first then keyword - display 2 books: BOOK001, BOOK009 (keyword overrides category) | Observation | [TC-03-12 author 1st](evidence/TC-03-12_OBS-03_author-first_1.png), [TC-03-12 author 1st](evidence/TC-03-12_OBS-03_author-first_2.png), [TC-03-12 author 1st](evidence/TC-03-12_OBS-03_author-first_3.png), [TC-03-12 genre 1st](evidence/TC-03-12_OBS-03_genre-first.png) | - |
| TC-03-13 | Combined search - mismatch | Display "No books found" | (1) If keyword entered first then category - display 3 Economics books: BOOK007, BOOK014, BOOK015 (category overrides keyword); (2) If category entered first then keyword - display 2 books: BOOK001, BOOK009 (keyword overrides category); | Observation | [TC-03-13 author 1st](evidence/TC-03-13_OBS-03_author-first.png), [TC-03-13 genre 1st](evidence/TC-03-13_OBS-03_genre-first.png) | - |
| TC-03-14 | Bilingual support - category bar | Same as TC-03-03 | Display "No books found" | Observed/TBD | [TC-03-14](evidence/TC-03-14_OBS-04.png) | - |
---

## Tổng hợp kết quả

| Chỉ số (Metric) | Giá trị (Value) |
|--------|---------|
| Tổng số test case (Total TC) | 14 |
| Pass | 6 |
| Fail | 1 |
| Blocked | 0 |
| Not Run | 0 |
| Observed | 7 |
| **Tỷ lệ Pass (Pass rate)** | 86% |

### Kết quả theo nhóm chức năng

| Nhóm (Group) | Tổng TC (Total TC) | Pass | Fail | Observed | Tỷ lệ Pass (Pass rate) |
|------|---------|------|------|------|------------|
| Search by title/author | 3 | 3 | 0 | 0 | 100% |
| Filter by category | 1 | 1 | 0 | 0 | 100% |
| Case sensitivity | 2 | 1 | 1 | 0 | 50% |
| Diacritic sensitivity | 2 | 0 | 0 | 2 | 0% |
| Partial keyword | 2 | 0 | 0 | 2 | 0% |
| Empty fields | 1 | 1 | 0 | 0 | 100% |
| Combined search | 2 | 0 | 0 | 2 | 0% |
| Bilingual support | 1 | 0 | 0 | 1 | 0% |
