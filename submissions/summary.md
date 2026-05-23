# Test Summary — Báo cáo tổng hợp kiểm thử

> **Hướng dẫn**: Đây là hoạt động **Quality Assurance** — bạn đánh giá chất lượng tổng thể của phần mềm, không chỉ liệt kê lỗi.

---

## 1. Thông tin nhóm

| Mục | Thông tin |
|-----|----------|
| **Nhóm** | `<!-- Group 14 -->` |
| **Lớp** | `<!-- VD: SE001.P11 -->` |
| **Ngày báo cáo** | `<!-- 23/05/2026 -->` |
| **Hệ thống kiểm thử** | https://stqa.rbc.vn — v1.0 |

---

## 2. Tổng quan kết quả

| Chỉ số (Metric) | Giá trị (Value) |
|--------|---------|
| Tổng số test case (Total TC) | `<!-- 12 -->` |
| Pass | `<!-- 7 -->` |
| Fail | `<!-- 4 -->` |
| Blocked | `<!-- 0 -->` |
| Not Run | `<!-- 0 -->` |
| Observed | `<!-- 1 -->` |
| **Tỷ lệ Pass (Pass rate)** | `<!-- 63.6% -->` |
| **Số bug phát hiện (Total bugs found)** | `<!-- 3 -->` |

### Phân bổ theo nhóm chức năng

| Nhóm chức năng (Feature Group) | TC | Pass | Fail | Observed | Bug | Đánh giá (Assessment)|
|---------------|-----|------|------|-----|---------|
| Search by title/author | 3 | 3 | 0 | 0 | - | Good |
| Filter by category | 1 | 1 | 0 | 0 | — | Good |
| Case sensitivity | 2 | 1 | 1 | 0 | BUG-01 | ⚠ Needs improvement |
| Diacritic sensitivity | 1 | 0 | 0 | 1 | — | Observed — outside SRS scope, output TBD |
| Partial keyword | 2 | 1 | 1 | 1 | BUG-02 | ⚠ Needs improvement |
| Empty fields | 1 | 1 | 0 | 0 | — | Good |
| Combined search | 2 | 0 | 2 | 0 | BUG-03 | Critical issue |
| **Total** | **12** | **7** | **4** | **1** | **3** | |

### Phân bổ bug theo mức độ

| Mức độ (Severity) | Số lượng (Count) | Bug IDs |
|--------|---------|---------|
| High | 1 | BUG-03 |
| Medium | 1 | BUG-01 |
| Low | 1 | BUG-02 |

---

## 3. Kỹ thuật thiết kế đã sử dụng

| Kỹ thuật (Technique) | Áp dụng cho REQ nào? (Applied to REQ) | Số TC sử dụng (TC count) | Giải thích cách áp dụng (How it was applied) |
|----------|---------------------|---------------|------------------------|
| **EP (Equivalence Partitioning)** | REQ-03 | 9 | Divided search inputs into partitions: valid keyword (book title / author name), no match, case variants (lowercase / uppercase), diacritic variants, and partial input. Each partition has one representative value — testing one value covers the whole group. |
| **BVA (Boundary Value Analysis)** | REQ-03 | 1 | Applied to the empty input boundary (TC-10): when both search bars are empty, the system must display all 20 books. This is the lower boundary between "filtered" and "unfiltered" state. |
| **Decision Table** | REQ-03 | 2 | Applied to combined search (TC-11, TC-12): systematically covered all combinations of keyword and category inputs — both match, and keyword match but category mismatch — to verify AND logic is applied correctly. |

---

## 4. Phân tích chất lượng phần mềm

### 4.1. Điểm mạnh
`<!-- **Basic search works correctly**: Searching by book title and author name returns accurate results (TC-01, TC-02, TC-03 — all Pass). -->`
`<!-- **Category filter works with correct input**: Filtering by exact category name returns the correct book list (TC-04 — Pass). -->`
`<!-- **Case-insensitive search on keyword bar**: The title/author search bar correctly handles lowercase and uppercase input as required by SRS REQ-03 (TC-05 — Pass). -->`
`<!-- **Partial match on keyword bar**: Typing a partial author name returns all matching books, improving usability beyond what SRS requires (TC-08 — Pass). -->`
`<!-- **Empty state handled correctly**: When both fields are empty, all 20 books are displayed as expected (TC-10 — Pass). -->`

### 4.2. Điểm yếu
`<!-- **BUG-03 (High) — Combined search broken**: The most critical issue. When both search bars are used simultaneously, the system does not apply AND logic — whichever bar was typed in last overrides the other completely. Results differ based on input order, making the combined search feature unreliable and unpredictable. -->`
`<!-- **BUG-01 (Medium) — Category filter is case-sensitive**: The category filter does not follow the case-insensitive rule stated in SRS REQ-03. Typing `"công nghệ"` or `"CÔNG NGHỆ"` returns no results, while the keyword bar handles the same inputs correctly. This is an inconsistency between the two bars. -->`
`<!-- **BUG-02 (Low) — Category filter does not support partial match**: The category filter requires the full exact category name to return results, while the keyword bar supports partial input. SRS does not explicitly require this but the inconsistency may confuse users. -->`
`<!-- **Observed — Diacritic-insensitive search not supported (TC-07)**: The system does not recognize 
input without Vietnamese diacritics (e.g. `"Nguyen Minh Duc"` does not return results for 
`"Nguyễn Minh Đức"`). This is outside SRS scope so it is not classified as a bug, but given 
that the system supports a Vietnamese-language interface, users may naturally type without 
diacritics. This is worth considering as a usability improvement in future iterations. -->`

---

## 5. Đề xuất ưu tiên sửa lỗi

> 💡 Đây là phần **Quality Assurance**: bạn không chỉ tìm lỗi mà còn **đề xuất thứ tự ưu tiên** sửa chữa và đánh giá tác động.
> Nêu rõ tiêu chí ưu tiên: dựa vào **severity** (mức độ nghiêm trọng kỹ thuật) và/hoặc **priority** (mức độ ưu tiên kinh doanh).

| Thứ tự (Priority) | Bug | Mức độ (Severity) | Lý do ưu tiên (Reason)|
|--------|-----|--------|---------------|
| 1 | BUG-03 | High | Combined search is fundamentally broken — wrong results returned silently in 3 out of 4 input scenarios. Directly violates the core functionality of REQ-03. Must be fixed before release. |
| 2 | BUG-01 | Medium | Category filter violates the SRS case-insensitive requirement and is inconsistent with the keyword bar. Likely a quick fix (input normalization). Fix before release. |
| 3 | BUG-02 | Low | Category filter does not support partial match. Not required by SRS — treat as a usability improvement. Address in a follow-up iteration after BUG-01 and BUG-03 are resolved. |

---

## 6. Kết luận

`<!-- The system partially meets the requirements defined in SRS REQ-03. Basic search and filter functions work correctly in isolation, but **the system is NOT ready for release** in its current state for the following reasons:

1. **BUG-03** makes the combined search feature unreliable — results depend on input order rather than AND logic, which is a fundamental design flaw that directly misleads users.
2. **BUG-01** means the category filter silently violates the case-insensitive rule stated in SRS, creating inconsistent behavior between the two search bars.

**Recommendation**: Fix BUG-03 and BUG-01 before release. BUG-02 can be addressed in a follow-up iteration as a usability improvement. -->`

---

## 7. Bài học rút ra (Tùy chọn)

`<!-- **IDM structures testing effectively**: Building the Input Domain Model before writing test cases forced systematic thinking about all input partitions, including edge cases like diacritic sensitivity and partial input that might otherwise have been missed. -->`
`<!-- **Observation cases still have value**: TC-07 and TC-09 were marked Observed (outside SRS scope) but still revealed useful behavioral information — particularly that the category filter behaves differently from the keyword bar in multiple ways. -->`
`<!-- **Test input order matters**: Discovering that TC-11 and TC-12 produce different results depending on input order was only possible because both scenarios were tested. Always test different input orders when multiple fields interact. -->`
`<!-- **Root cause analysis saves time**: BUG-01, BUG-02, and BUG-03 likely share a common root cause in how the filter logic is implemented. Identifying this early helps developers fix multiple bugs in one change. -->`

---

## 8. Khai báo sử dụng AI (Tùy chọn)

> Nếu nhóm có sử dụng công cụ AI (ChatGPT, Copilot, Gemini...), hãy ghi rõ bên dưới. Khai báo trung thực **không ảnh hưởng điểm** — đây là kỹ năng minh bạch trong nghề.

| Công cụ AI (AI Tool) | Dùng cho phần nào (Used for) | Bạn đã kiểm tra/chỉnh sửa thế nào (How results were verified) |
|------------|-------------------|-----------------------------------|
| Claude | AI combines lecture knowledge and self-assessment to support the writing of IDM documentation, test cases and bug reports. | All content was reviewed and validated against actual test results on https://stqa.rbc.vn. Actual results, conclusions, and bug descriptions were recorded and adjusted by group members based on real observations. |
