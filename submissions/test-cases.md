# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Group 14 -->` |
| **Ngày tạo** | `<!-- 18/05/2026 -->` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.


### IDM — Search & Filter Books (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Keywords exists in DB? | Yes (book title) | `"Flutter"` | Display books containing "Flutter" |
| | Yes (author name) | `"Nguyễn Minh Đức"` | Display books by Nguyễn Minh Đức |
| | No match | `"XYZ123"` | Display "Không tìm thấy sách" |
| Filter by category | Books | `"Công nghệ"` | Display 8 books in Technology category only |
| Case sensitivity? | Mixed case (keyword bar) | `"Flutter"` | Display correct result (baseline) |
| | (category bar) | `"Công nghệ"` | Display correct result |
| | Lowercase | `"flutter"` | Same result as "Flutter" |
| | | `"công nghệ"` | Same result as "Công nghệ" |
| | Uppercase | `"FLUTTER"` | Same result as "Flutter" |
| | | `"CÔNG NGHỆ"` | Same result as "Công nghệ" |
| Diacritic sensitivity | No diacritics | `"Nguyen Minh Duc"` | Show all books by author matching "Nguyen Minh Duc" (SRS does not require) |
| | | `"Cong nghe"` | Show all books with genre matching "Cong nghe" (SRS does not require) |
| Partial keyword | Partial input | `"Nguyễn"` | Display all books whose author contains "Nguyễn" (SRS does not specify) |
| | | `"Công"` | Display all books whose genre contains "Công" (SRS does not specify) |
| Search field empty? | Completely empty | no input | Display all 20 books |
| Keyword + category combined | Both match | `"Lý Văn Tài"` + `"Công nghệ"` | Display 2 books: BOOK008, BOOK011 |
| | Keyword and category mismatch| `"Lý Văn Tài"` + `"Kinh tế"` | Display "Không tìm thấy sách" |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Search by valid book title/baseline for case sensitivity test | Logged in as `ba.nguyen@email.com`. On Books tab. | 1. Click on the title or author search bar. 2. Type `"Flutter"`. 3. Observe the book list. | Keyword: `"Flutter"` | Display exactly 1 book: "Lập trình Flutter cơ bản" (BOOK001). No other books shown. Used as baseline for TC-06 and TC-07. | REQ-03 | EP |
| TC-02 | Search by valid author name | Similar to the above | 1. Go to the title or author search bar. 2. Type `"Nguyễn Minh Đức"`. 3. Observe the book list. | Keyword: `"Nguyễn Minh Đức"` | Display exactly 2 books: BOOK001 and BOOK009. No other books shown. | REQ-03 | EP |
| TC-03 | Search with keyword that does not exist in DB | Similar to the above | 1. Go to the both search bars. 2. Type `"XYZ123"`. 3. Observe the book list. | Keyword: `"XYZ123"` | Display message "Không tìm thấy sách". No books shown. | REQ-03 | EP |
| TC-04 | Filter books by category/baseline for case sensitivity test | Similar to the above | 1. Click on the category filter. 2. Type `"Công nghệ"`. 3. Observe the book list. | Keyword: `"Công nghệ"` | Display exactly 8 books in Technology category: BOOK001, BOOK002, BOOK003, BOOK005, BOOK008, BOOK009, BOOK010, BOOK011. No other books shown. Used as baseline for TC-09 and TC-10. | REQ-03 | EP |
| TC-05 | Search bar — lowercase input (case-insensitive) | Similar to the above | 1. Go to the title or author search bar. 2. Type `"flutter"`. 3. Observe the book list. | Keyword: `"flutter"` | Display exactly 1 book: BOOK001. Same result as TC-05. SRS requires case-insensitive search. | REQ-03 | EP |
| TC-06 | Search bar — uppercase input (case-insensitive) | Similar to the above | 1. Go to the title or author search bar. 2. Type `"FLUTTER"`. 3. Observe the book list. | Keyword: `"FLUTTER"` | Display exactly 1 book: BOOK001. Same result as TC-05. SRS requires case-insensitive search. | REQ-03 | EP |
| TC-07 | Category bar — lowercase input (case-insensitive) | Similar to the above | 1. Go to the category filter. 2. Type `"công nghệ"`. 3. Observe the book list. | Keyword: `"công nghệ"` |  Same result as TC-08 — 8 books shown. | REQ-03 | EP |
| TC-08 | Category bar — uppercase input (case-insensitive) | Similar to the above | 1. Go to the category filter. 2. Type `"CÔNG NGHỆ"`. 3. Observe the book list. | Keyword: `"CÔNG NGHỆ"` | Same result as TC-08 — 8 books shown. | REQ-03 | EP |
| TC-09 | Search bar — input without diacritics | Similar to the above | 1. Go to the title or author search bar. 2. Type `"Nguyen Minh Duc"`. 3. Observe the book list. | Keyword" `"Nguyen Minh Duc"` | Same result as TC-02. ⚠ Observation: SRS does not require diacritic-insensitive search. Record actual result only.| REQ-03 | EP |
| TC-10 | Category bar — input without diacritics | Similar to the above | 1. Go to the category filter. 2. Type `"Cong nghe"`. 3. Observe the book list. | Keyword: `"Cong nghe"` | Same result as TC-04. ⚠ Observation: SRS does not require diacritic-insensitive search. Record actual result only.| REQ-03 | EP |
| TC-11 | Search bar — partial keyword input | Similar to the above | 1. Go to the title or author search bar. 2. Type `"Nguyễn"`. 3. Observe the book list. | Keyword: `"Nguyễn"` | Display all books whose author name contains "Nguyễn" | REQ-03 | EP |
| TC-12 | Category bar — partial keyword input | Similar to the above | 1. Go to the category filter. 2. Type `"Công"`. 3. Observe the book list. | Keyword: `"Công"` | Display all books whose category contains "Công" | REQ-03 | EP |
| TC-13 | Both fields empty — display all books | Similar to the above | 1. Go to both search bars. 2. Leave search bar empty. 3. Do not select any category. 4. Observe the book list. | Search bar: empty. Category: none selected. | Display all 20 books. | REQ-03 | BVA |
| TC-14 | Combined search — both keyword and category match | Similar to the above | 1. Go to both search bars. 2. Type `"Lý Văn Tài"` in the title or author search bar. 3. Type `"Công nghệ"` in the category filter. 4. Observe the book list. | Keyword: `"Lý Văn Tài"`. Category: `"Công nghệ"`. | Display exactly 2 books: BOOK008 (Mạng máy tính) and BOOK011 (Hệ điều hành Linux). | REQ-03 | Decision Table |
| TC-15 | Combined search — keyword matches but category mismatches | Similar to the above | 1. Go to both search bars. 2. Type `"Lý Văn Tài"` in the title or author search bar. 3. Type `"Kinh tế"` in the category filter. 4. Observe the book list. | Keyword: `"Lý Văn Tài"`. Category: `"Kinh tế"`. | Display message "Không tìm thấy sách". System must apply both filters simultaneously. | REQ-03 | Decision Table |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| Search by title/author | 3 | REQ-03 | EP |
| Filter by category | 1 | REQ-03 | EP |
| Case sensitivity | 4 | REQ-03 | EP |
| Diacritic sensitivity | 2 | REQ-03 | EP |
| Partial keyword | 2 | REQ-03 | EP |
| Search field empty | 1 | REQ-03 | BVA |
| Combined 2 search bars | 2 | REQ-03 | Decision Table |
| **Tổng** | **<!-- 15 -->** | REQ-03 | EP, BVA, Decision Table |
