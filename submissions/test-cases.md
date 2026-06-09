# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | Group 14 |
| **Ngày tạo** | 18/05/2026 |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.


### IDM — Search & Filter Books (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi (Result) |
|---|---|---|---|
| Keywords exists in DB | Book title | `"Flutter"` | Display books containing "Flutter" |
| | Author name | `"Nguyễn Minh Đức"` | Display books by Nguyễn Minh Đức |
| | Books (category) | `"Công nghệ"` | Display 8 books in Technology category |
| | No match | `"XYZ123"` | Display "Không tìm thấy sách" |
| | Completely empty search | no input | Display all 20 books |
| Case sensitivity | Mixed case - keyword bar | `"Nguyễn Minh Đức"` | Display correct result (baseline) |
| | category bar | `"Công nghệ"` | Display correct result (baseline) |
| | Lowercase - keyword bar | `"nguyễn minh đức"` | Same result as "Flutter" |
| | category bar | `"công nghệ"` | Same result as "Công nghệ" |
| | Uppercase - keyword bar| `"NGUYỄN MINH ĐỨC"` | Same result as "Flutter" |
| | category bar | `"CÔNG NGHỆ"` | Same result as "Công nghệ" |
| Diacritic sensitivity | No diacritics - keyword bar | `"Nguyen Minh Duc"` | Show all books by author matching "Nguyen Minh Duc" (SRS does not require) |
| | category bar | `"Cong nghe"` | Show all books with genre matching "Cong nghe" (SRS does not require) |
| Partial keyword | Partial input - keyword bar | `"Nguyễn"` | Display all books whose author contains "Nguyễn" (SRS does not specify) |
| | category bar | `"Công"` | Display all books whose genre contains "Công" (SRS does not specify) |
| Keyword + category combined | Both match | `"Nguyễn Minh Đức"` + `"Công nghệ"` | Display 2 books: BOOK008, BOOK011 |
| | Keyword and category mismatch| `"Nguyễn Minh Đức"` + `"Kinh tế"` | Display "No books found" |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC (TC ID) | Mục tiêu kiểm thử (Test Objective) | Tiền điều kiện (Preconditions) | Bước thực hiện (Test Steps) | Dữ liệu đầu vào (Input Data) | Kết quả mong đợi (Expected Result) | REQ | Kỹ thuật (Technique) |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-03-01 | Search by valid book title | Logged in as `ba.nguyen@email.com`. On Books tab. | 1. Click on the title or author search bar. 2. Type `"Flutter"`. 3. Observe the book list. | Keyword: `"Flutter"` | Display books whose title contains 'Flutter'. No other books shown. | REQ-03 | EP |
| TC-03-02 | Search by valid author name (Baseline for case sensitivity test) | Similar to the above | 1. Click on the title or author search bar. 2. Type `"Nguyễn Minh Đức"`. 3. Observe the book list. | Keyword: `"Nguyễn Minh Đức"` | Display 2 books whose author is "Nguyễn Minh Đức". No other books shown. Used as baseline for TC-03-05. | REQ-03 | EP |
| TC-03-03 | Filter books by category (Baseline for case sensitivity test) | Similar to the above | 1. Click on the category filter. 2. Type `"Công nghệ"`. 3. Observe the book list. | Keyword: `"Công nghệ"` | Display 8 books from Technology category that include the word 'Công nghệ'. No other books shown. Used as baseline for TC-03-06. | REQ-03 | EP |
| TC-03-04 | Search with keyword that does not exist in DB | Similar to the above | 1. Click on each search bar. 2. Type `"XYZ123"`. 3. Observe the book list. | Keyword: `"XYZ123"` | Display message "Không tìm thấy sách"/"No books found". No books shown. | REQ-03 | EP |
| TC-03-05 | Name bar - lowercase & uppercase input (case-insensitive) | Similar to the above | 1. Go to the title or author search bar. 2. Type `"nguyễn minh đức"`. 3. Observe the book list. 4. Do it again with `"NGUYỄN MINH ĐỨC"`. | Keyword: `"nguyễn minh đức"` & `"NGUYỄN MINH ĐỨC"` | Display 2 books whose title or author is "Nguyễn Minh Đức". Same result as TC-03-02. SRS requires case-insensitive search. | REQ-03 | EP |
| TC-03-06 | Category bar - lowercase & uppercase input (case-insensitive) | Similar to the above | 1. Go to the category filter. 2. Type `"công nghệ"`. 3. Observe the book list. 4. Do it again with `"CÔNG NGHỆ"`. | Keyword: `"công nghệ"` & `"CÔNG NGHỆ"` |  Display 8 Technogy books whose category is "Công nghệ". Same result as TC-03-03. | REQ-03 | EP |
| TC-03-07 | Name bar - input without diacritics | Similar to the above | 1. Go to the title or author search bar. 2. Type `"Nguyen Minh Duc"`. 3. Observe the book list. | Keyword: `"Nguyen Minh Duc"` | Same result as TC-03-02. Observation: SRS does not require diacritic-insensitive search. Record actual result only. | REQ-03 | EP |
| TC-03-08 | Category bar - input without diacritics | Similar to the above | 1. Go to the category filter. 2. Type Type `"Cong nghe"`. 3. Observe the book list. | Keyword: `"Cong nghe"` | Same result as TC-03-03. Observation: SRS does not require diacritic-insensitive search. Record actual result only. | REQ-03 | EP |
| TC-03-09 | Name bar - partial keyword input | Similar to the above | 1. Go to the title or author search bar. 2. Type `"Nguyễn"`. 3. Observe the book list. | Keyword: `"Nguyễn"` | Display all books whose author name contains 'Nguyễn'. Observation: SRS does not specify partial match. | REQ-03 | EP |
| TC-03-10 | Category bar - partial keyword input | Similar to the above | 1. Go to the category filter. 2. Type `"Công"`. 3. Observe the book list. | Keyword: `"Công"` | Display all books whose category contains 'Công'. Observation: SRS does not specify partial match. | REQ-03 | EP |
| TC-03-11 | Both fields empty | Similar to the above | 1. Go to both search bars. 2. Leave search bar empty. 3. Do not select any category. 4. Observe the book list. | Search bar: empty. Category: none selected. | Display all 20 books. | REQ-03 | BVA |
| TC-03-12 | Combined search - both keyword and category match | Similar to the above | 1. Go to both search bars. 2. Type `"Nguyễn Minh Đức"` in the title or author search bar. 3. Type `"Công nghệ"` in the category filter. 4. Observe the book list. 5. Clear and then repeat this process, but reverse steps 2 and 3. | Keyword: `"Nguyễn Minh Đức"`. Category: `"Công nghệ"`. | Display 2 books whose author is "Nguyễn Minh Đức" and category is "Công nghệ". | REQ-03 | Decision Table |
| TC-03-13 | Combined search - keyword matches but category mismatches | Similar to the above | 1. Go to both search bars. 2. Type `"Nguyễn Minh Đức"` in the title or author search bar. 3. Type `"Kinh tế"` in the category filter. 4. Observe the book list. 5. Clear and then repeat this process, but reverse steps 2 and 3. | Keyword: `"Nguyễn Minh Đức"`. Category: `"Kinh tế"`. | Display message "Không tìm thấy sách"/"No books found". System must apply both filters simultaneously. | REQ-03 | Decision Table |
| TC-03-14 | Category bar - English keyword input (bilingual support) | Logged in as `ba.nguyen@email.com`. On Books tab. Interface language set to English. | 1. Go to **Books** tab. 2. Switch interface language to English. 3. Click on the category filter bar. 4. Type `"Technology"`. 5. Observe the book list. | Category: `"Technology"` | Display 8 books in Technology category (Same result as TC-03-03) | REQ-03 | EP |
---

## Tổng hợp

| Nhóm chức năng (Feature Group) | Số TC (Total TC) | REQ phủ | Kỹ thuật IDM áp dụng (IDM Technique) |
|----------------|-------|---------|----------------------|
| Search by title/author | 3 | REQ-03 | EP |
| Filter by category | 1 | REQ-03 | EP |
| Case sensitivity | 2 | REQ-03 | EP |
| Diacritic sensitivity | 2 | REQ-03 | EP |
| Partial keyword | 2 | REQ-03 | EP |
| Search field empty | 1 | REQ-03 | BVA |
| Combined 2 search bars | 2 | REQ-03 | Decision Table |
| Bilingual support | 1 | REQ-03 | EP |
| **Tổng (Total)** | **14** | REQ-03 | EP, BVA, Decision Table |
