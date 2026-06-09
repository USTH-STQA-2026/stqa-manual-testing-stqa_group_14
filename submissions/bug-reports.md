# Bug Reports — Báo cáo lỗi

> **Hướng dẫn**: Tạo 1 mục bug cho mỗi TC có kết quả **Fail**.
> Xem [examples/sample-bug-report.md](../examples/sample-bug-report.md) để hiểu cách viết bug report tốt.
> Mỗi bug cần: tiêu đề mô tả hành vi lỗi, bước tái hiện, expected vs actual, severity + giải thích.

| Thông tin | |
|---|---|
| **Nhóm** | Group 14 |
| **Ngày báo cáo** | 23/05/2026 |

---

## BUG-01

| Thuộc tính (Attribute) | Chi tiết (Detail) |
|-----------|---------|
| **Mã lỗi (Bug ID)** | BUG-01 |
| **TC liên quan (Related TC)** | TC-03-06 |
| **REQ liên quan (Related REQ)** | REQ-03 |
| **Mức độ (Severity)** | Medium |
| **Người phát hiện (Found by)** | Nguyễn Minh Nhật |
| **Ngày phát hiện (Date found)** | 19/05/2026 |
| **Trạng thái (Status)** | Open |

**Tiêu đề (Title):**
Category filter returns no results when input is lowercase or uppercase

**Môi trường (Environment):**
- Trình duyệt (Browser): Chrome version 142
- Hệ điều hành (OS): Windows 10
- Web application: Library Management System
- Ngôn ngữ giao diện (UI language): Vietnamese, English

**Điều kiện tiên quyết (Preconditions):**
- Logged in as `ba.nguyen@email.com`
- On Books tab
- Data has been reset to seed data

**Bước tái hiện (Steps to reproduce):**
1. Go to **Books** tab.
2. Click on the category filter bar.
3. Type `"công nghệ"` (all lowercase).
4. Observe the book list.
5. Clear the filter.
6. Type `"CÔNG NGHỆ"` (all uppercase)
7. Observe the book list.

**Kết quả mong đợi (Expected result):**
Both inputs display 8 books in Technology category - same as typing `"Công nghệ"`. SRS REQ-03 states search must be case-insensitive.

**Kết quả thực tế (Actual result):**
Both inputs return "No books found". No books shown.

**Tác động (Impact):**
Users who type category names in lowercase or uppercase get no results despite matching books existing in the system. This is inconsistent with keyword search bar which correctly handles case-insensitive input (verified in TC-03-05).

**Severity explanation:**
Medium - the category filter still works with exact casing but violates the case-insensitive rule stated in SRS REQ-03. Core functionality is not broken, but the inconsistency with the keyword bar and the SRS violation reduce reliability and usability.

**Priority:**
P2

**Minh chứng (Evidence):**
- Screenshot lowecase: ![TC-03-06 lowercase](evidence/TC-03-06_BUG-01_lowercase.png)
- Screenshot uppercase: ![TC-03-06 uppercase](evidence/TC-03-06_BUG-01_uppercase.png)

**Đề xuất xử lý (Suggested fix):**
Apply `.toLowerCase()` or equivalent normalization to both the user input and the stored category values before comparison, consistent with how the keyword search bar already handles case. 

---

# Observation Reports

## OBSERVATION-01

| Thuộc tính (Attribute) | Chi tiết (Detail) |
|-----------|---------|
| **Mã lỗi (Bug ID)** | OBS-01 |
| **TC liên quan (Related TC)** | TC-03-07, TC-03-08 |
| **REQ liên quan (Related REQ)** | REQ-03 |
| **Mức độ (Severity)** | Low |
| **Type** | Requirement gap |
| **Người phát hiện (Found by)** | Nguyễn Minh Nhật |
| **Ngày phát hiện (Date found)** | 20/05/2026 |
| **Trạng thái (Status)** | Open |

**Tiêu đề (Title):**
Both search bars do not support diacritic-insensitive input - typing without Vietnamese diacritics returns no results

**Bước tái hiện (Steps to reproduce):**
1. Go to **Books** tab.
2. Click on the title or author search bar.
3. Type `"Nguyen Minh Duc"` (without diacritics).
4. Observe the book list.
5. Clear the search bar.
6. Click on the category filter bar.
7. Type `"Cong nghe"` (without diacritics).
8. Observe the book list.

**Kết quả mong đợi (Expected result):**
- Step 4: Display 2 books by Nguyễn Minh Đức - same result as TC-03-02.
- Step 8: Display 8 Technology books - same result as TC-03-03.

**Kết quả thực tế (Actual result):**
Display "No books found" for both cases. No books shown.

**Tác động (Impact):**
Users who type Vietnamese names or categories without diacritics get no results despite matching books existing in the system. Given that the system supports a Vietnamese-English language interface, this may affect a significant portion of users.

**Severity explanation:**
Low - SRS does not require diacritic-insensitive search. This problem is within spec. Reported as an observation for future consideration.

**Priority:**
P3

**Minh chứng (Evidence):**
- Screenshot: ![TC-03-07](evidence/TC-03-07_OBS-01_author-without-diacritics.png)
- Screenshot: ![TC-03-08](evidence/TC-03-08_OBS-01_genre-without-diacritics.png)

**Đề xuất xử lý (Suggested fix):**
Implement diacritic normalization (e.g. convert `"Nguyen Minh Duc"` → `"Nguyễn Minh Đức"` before comparison) for both search bars. This is a common requirement for Vietnamese-language applications.

---

## OBSERVATION-02

| Thuộc tính (Attribute) | Chi tiết (Detail) |
|-----------|---------|
| **Mã lỗi (Bug ID)** | OBS-02 |
| **TC liên quan (Related TC)** | TC-03-10 |
| **REQ liên quan (Related REQ)** | REQ-03 |
| **Mức độ (Severity)** | Low |
| **Type** | Requirement gap |
| **Người phát hiện (Found by)** | Nguyễn Minh Nhật |
| **Ngày phát hiện (Date found)** | 20/05/2026 |
| **Trạng thái (Status)** | Open |

**Tiêu đề (Title):**
Category filter does not support partial keyword input - requires full exact category name to return results

**Bước tái hiện (Steps to reproduce):**
1. Go to **Books** tab.
2. Click on the category filter bar.
3. Type `"Công"` (partial keyword).
4. Observe the book list.

**Kết quả mong đợi (Expected result):**
Display 8 books whose category contains "Công": BOOK001, BOOK002, BOOK003, BOOK005, BOOK008, BOOK009, BOOK010, BOOK011.

**Kết quả thực tế (Actual result):**
Display "No books found". No books shown. Only typing the full exact name `"Công nghệ"` returns results.

**Tác động (Impact):**
Category filter behaves inconsistently compared to the title/author search bar - which supports partial input (verified in TC-08). Users who type partial category names get no results and assume no books exist in that category.

**Severity explanation:**
Low - SRS does not explicitly require partial match for the category filter. However the inconsistency with the title/author bar creates a confusing user experience.

**Priority:**
P3

**Minh chứng (Evidence):**
- Screenshot: ![TC-03-10](evidence/TC-03-10_OBS-02.png)

**Đề xuất xử lý (Suggested fix):**
Implement partial match logic for the category filter (e.g. use `.contains()` instead of exact match), consistent with how the title/author search bar handles input.

---

## OBSERVATION-03 (BUG-02)

| Thuộc tính (Attribute) | Chi tiết (Detail) |
|-----------|---------|
| **Mã lỗi (Bug ID)** | OBS-03 |
| **TC liên quan (Related TC)** | TC-03-12, TC-03-13 |
| **REQ liên quan (Related REQ)** | REQ-03 |
| **Mức độ (Severity)** | High |
| **Type** | Requirement gap |
| **Người phát hiện (Found by)** | Nguyễn Minh Nhật |
| **Ngày phát hiện (Date found)** | 19/05/2026 |
| **Trạng thái (Status)** | Open |

**Tiêu đề (Title):**
Combined search does not apply AND logic - the last-entered search bar overrides the other, returning wrong results

**Bước tái hiện (Steps to reproduce):**
- TC-03-12 - 1. keyword first
1. Go to **Books** tab.
2. Type `"Nguyễn Minh Đức"` in the title/author search bar.
3. Observe - display 2 books: BOOK001, BOOK009.
4. Type `"Công nghệ"` in the category filter.
5. Observe the book list.
- TC-03-12 - 2. category first
1. Go to **Books** tab.
2. Type `"Công nghệ"` in the category filter.
3. Observe - display 8 Technology books.
4. Type `"Nguyễn Minh Đức"` in the title/author search bar.
5. Observe the book list.
- TC-03-13 - 1. keyword first
1. Go to **Books** tab.
2. Type `"Nguyễn Minh Đức"` in the title/author search bar.
3. Observe - display 2 books: BOOK001, BOOK009.
4. Type `"Kinh tế"` in the category filter.
5. Observe the book list.
- TC-03-13 - 2. category first
1. Go to **Books** tab.
2. Type `"Kinh tế"` in the category filter.
3. Observe - display 3 Economics books: BOOK007, BOOK014, BOOK015.
4. Type `"Nguyễn Minh Đức"` in the title/author search bar.
5. Observe the book list.

**Kết quả mong đợi (Expected result):**
- TC-03-12: Display exactly 2 books - BOOK001 (Lập trình Flutter cơ bản) and BOOK009 (Nhập môn lập trình Python), authored by Nguyễn Minh Đức and in Technology category. Result must be identical regardless of input order.
- TC-03-13: Display "Không tìm thấy sách" - Nguyễn Minh Đức has no books in Economics category. Result must be identical regardless of input order.

**Kết quả thực tế (Actual result):**
- TC-03-12 - 1: Display 8 Technology books - category filter overrides keyword entirely.
- TC-03-12 - 2: Display 2 books BOOK001, BOOK009 - keyword overrides category (accidentally correct but inconsistent).
- TC-03-13 - 1: Display 3 Economics books: BOOK007, BOOK014, BOOK015 - category overrides keyword.
- TC-03-13 - 2: Display 2 books BOOK001, BOOK009 - keyword overrides category, ignores category filter

**Tác động (Impact):**
Combined search is fundamentally broken. Results are unpredictable and depend entirely on input order (based on which bar is entered last). Users cannot narrow down results using both filters simultaneously, which defeats the purpose of having two search bars. Wrong books are returned with no error message.

**Severity explanation:**
High - combined filtering is a core use case of REQ-03 (especially when users don't remember the exact the detail of name). The feature returns incorrect results in 3 out of 4 scenarios with no warning to the user. This directly distorts information and misleads users. This is reported as an observation rather than a bug because it is not mentioned in the SRS requirements.

**Priority:**
P1

**Minh chứng (Evidence):**
- Screenshot match - author 1st: ![TC-03-12 author 1st](evidence/TC-03-12_OBS-03_author-1st_1.png) ![TC-03-12 author 1st](evidence/TC-03-12_OBS-03_author-1st_2.png) ![TC-03-12 author 1st](evidence/TC-03-12_OBS-03_author-1st_3.png)
- Screenshot match - genre 1st: ![TC-03-12 category 1st](evidence/TC-03-12_OBS-03_genre-1st.png)
- Screenshot mismatch - author 1st: ![TC-03-13 author 1st](evidence/TC-03-13_OBS-03_author-1st.png)
- Screenshot mismatch - genre 1st: ![TC-03-13 category 1st](evidence/TC-03-13_OBS-03_genre-1st.png)

**Đề xuất xử lý (Suggested fix):**
Refactor the search/filter logic to evaluate both conditions simultaneously using AND logic: a book must satisfy both the keyword condition (title or author contains keyword) and the category condition (category matches filter) to appear in results. The result must be consistent regardless of which bar is filled in first.

---

## OBSERVATION-04

| Thuộc tính (Attribute) | Chi tiết (Detail) |
|-----------|---------|
| **Mã lỗi (Bug ID)** | OBS-04 |
| **TC liên quan (Related TC)** | TC-03-14 |
| **REQ liên quan (Related REQ)** | REQ-03 |
| **Mức độ (Severity)** | Low |
| **Type** | Requirement gap |
| **Người phát hiện (Found by)** | Nguyễn Minh Nhật |
| **Ngày phát hiện (Date found)** | 21/05/2026 |
| **Trạng thái (Status)** | Open |

**Tiêu đề (Title):**
Category filter returns no results when input is typed in English (e.g. `"Technology"`) despite system supporting bilingual interface

**Bước tái hiện (Steps to reproduce):**
1. Go to **Books** tab.
2. Switch interface language to English.
3. Click on the category filter bar.
4. Type `"Technology"`.
5. Observe the book list.

**Kết quả mong đợi (Expected result):**
Display all books whose category is "Công nghệ" (since the interface is set to English, the English equivalent "Technology" should be recognized by the filter).

**Kết quả thực tế (Actual result):**
Display "No books found". No books shown.

**Tác động (Impact):**
Users who switch the interface to English and type category names in English get no results despite matching books existing in the system. 

**Severity explanation:**
Low - since SRS does not require bilingual input for the category filter. However this is inconsistent with the bilingual support mentioned in BRD. This is reported as an observation for future consideration.

**Priority:**
P3

**Minh chứng (Evidence):**
- Screenshot: ![TC-03-14](evidence/TC-03-14_OBS-04.png)

**Đề xuất xử lý (Suggested fix):**
Map English category keywords to their Vietnamese equivalents before filtering (e.g. `"Technology"` → `"Công nghệ"`). This would make the filter consistent with the bilingual interface experience stated in BRD.

---

<!-- Copy template BUG trên để thêm BUG-03, BUG-04, ... cho mỗi TC Fail -->
