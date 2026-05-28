# Test Summary — Báo cáo tổng hợp kiểm thử

# Test Summary — Báo cáo tổng hợp kiểm thử

> **Hướng dẫn**: Đây là hoạt động **Quality Assurance** — bạn đánh giá chất lượng tổng thể của phần mềm, không chỉ liệt kê lỗi.

---

## 1. Thông tin nhóm

| Mục | Thông tin |
|-----|----------|
| **Nhóm** | Group 14 |
| **Lớp** | ICT |
| **Ngày báo cáo** | 23/05/2026 |
| **Hệ thống kiểm thử** | https://stqa.rbc.vn — v1.0 |

---

## 2. Tổng quan kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 53 |
| Pass | 34 |
| Fail | 13 |
| Observed / Inconclusive | 6 |
| Blocked | 0 |
| Not Run | 0 |
| **Tỷ lệ Pass** | 64.15% |
| **Số bug phát hiện** | 6 |

### Phân bổ theo nhóm chức năng

| Nhóm chức năng | TC | Pass | Fail | Bug | Đánh giá |
|---------------|-----|------|------|-----|---------|
| REQ-01 & REQ-02 — Login / View Book List | 16 | 10 | 2 | 0 | Partially Passed — Core login and book list functions worked correctly in normal scenarios, but localization inconsistency and requirement ambiguity were observed. |
| REQ-03 — Search and Filter Books | 12 | 7 | 3 | 2 | Needs Improvement — Basic search and category filtering worked in isolation, but combined search logic and category case-insensitivity did not fully comply with requirements. |
| REQ-05 & REQ-06 — Return Book / Overdue Handling | 10 | 7 | 3 | 2 | Partially Passed — Core return and overdue checking worked, but overdue warning and member ownership control issues were found. |
| REQ-07 & REQ-08 — Member Management / Borrow-Return Access | 15 | 10 | 5 | 2 | Needs Improvement — Core workflows mostly functioned, but high-severity validation and access-control issues affected reliability and privacy. |
| **Total** | **53** | **34** | **13** | **6** | **System requires fixes before release.** |

### Phân bổ bug theo mức độ

| Mức độ | Số lượng | Bug IDs |
|--------|---------|---------|
| High | 4 | BUG-01, BUG-03, BUG-05, BUG-06 |
| Medium | 2 | BUG-02, BUG-04 |
| Low | 0 | None |

> Note: Observations, requirement ambiguities, and requirement gaps are tracked separately because they are not confirmed functional bugs.

---

## 3. Kỹ thuật thiết kế đã sử dụng

| Kỹ thuật | Áp dụng cho REQ nào? | Số TC sử dụng | Giải thích cách áp dụng |
|----------|---------------------|---------------|------------------------|
| Equivalence Partitioning (EP) | REQ-01, REQ-02, REQ-03, REQ-05, REQ-06, REQ-07, REQ-08 | 45 | Input conditions were divided into valid and invalid partitions, including valid/invalid login data, user roles, book status, search keywords, category values, overdue/non-overdue records, member permissions, valid/invalid emails, and active/returned borrow records. |
| Boundary Value Analysis (BVA) | REQ-03, REQ-05, REQ-06, REQ-07 | 9 | Boundary conditions were tested for empty input fields, due date limits such as `currentDate = dueDate`, and input validation limits such as email and phone number format/length. |
| Decision Table | REQ-03 | 2 | Applied to combined search scenarios to verify different combinations of keyword and category input, especially cases where both fields match or only one field matches. |
| Negative Testing | REQ-05, REQ-07, REQ-08 | 2+ | Used to verify invalid or unauthorized behavior, such as returning an already returned book, returning another member’s borrowed book, invalid member information, and unauthorized access to another member’s borrow data. |

---

## 4. Phân tích chất lượng phần mềm

### 4.1. Điểm mạnh

- **Role-based access for normal login scenarios works correctly.** The system correctly distinguishes between librarian and member roles during normal login and access flows.
- **Book list display is stable.** The book list shows complete and accurate book information, and real-time book status updates function properly.
- **Basic search works correctly.** Searching by book title and author name returns accurate results.
- **Category filter works with exact valid input.** Filtering by exact category name returns the expected book list.
- **Keyword search supports case-insensitive input.** The title/author search bar correctly handles lowercase and uppercase input as required.
- **Partial keyword search works on the keyword bar.** Partial author/title input can return matching books, improving usability.
- **Empty search state is handled correctly.** When both search fields are empty, the full book list is displayed as expected.
- **Return book core workflow works in normal scenarios.** After a successful return, the book status is updated to `"Available"` and the borrow record status is updated to `"Returned"`.
- **Duplicate return prevention works.** The system prevents returning books that have already been returned.
- **Overdue checking works correctly.** The overdue checking function correctly handles before, on, and after due date scenarios.
- **Member and borrow/return core workflows mostly function.** Adding members and borrow/return flows operate correctly for most valid scenarios.
- **Input Domain Model (IDM) helped structure testing.** The test cases covered valid/invalid partitions and boundary values for multiple functional areas.

### 4.2. Điểm yếu

#### REQ-01 & REQ-02 — Login / View Book List

**High**
- None.

**Medium**
- None.

**Low / Observation**
- **OBS-01 — Error message localization inconsistency.** Some error messages are not consistently localized, causing English/Vietnamese mismatch in the user interface.
- **RA-01 — Requirement ambiguity for partially empty fields.** The SRS does not clearly define the expected behavior when only some login fields are empty.
- **RG-01 — Requirement gap for invalid email format validation.** The SRS does not clearly define how invalid email format should be handled during login.

#### REQ-03 — Search and Filter Books

**High**
- **BUG-01 — Combined search logic is broken.** When both search bars are used at the same time, the system does not correctly apply AND logic. The field typed last overrides the other field, causing results to differ depending on input order. This makes the combined search feature unreliable and misleading.

**Medium**
- **BUG-02 — Category filter is case-sensitive.** The category filter does not follow the case-insensitive rule stated in SRS REQ-03. For example, inputs such as `"công nghệ"` or `"CÔNG NGHỆ"` return no result, while the keyword search bar handles case variations correctly.

**Low / Observation**
- **OBS-02 — Diacritic-insensitive search is not supported.** The system does not recognize Vietnamese input without diacritics, such as `"Nguyen Minh Duc"` for `"Nguyễn Minh Đức"`. This is outside the explicit SRS scope but may affect usability in a Vietnamese-language interface.
- **OBS-03 — Category filter does not support partial match.** The category filter requires the full exact category name, while the keyword bar supports partial input. This inconsistency may confuse users, although it is not explicitly required by the SRS.

#### REQ-05 & REQ-06 — Return Book / Overdue Handling

**High**
- **BUG-03 — Member can return another member’s borrowed book.** The system allows a logged-in member to return a book borrowed by another member. This violates access control and borrow-record ownership rules, creating risks to data integrity and user privacy.

**Medium**
- **BUG-04 — Missing overdue warning when returning overdue books.** The system fails to display an overdue warning when returning overdue books where `returnDate >= dueDate`. This creates inconsistency between return behavior and overdue handling requirements.

**Low / Observation**
- None.

#### REQ-07 & REQ-08 — Member Management / Borrow-Return Access

**High**
- **BUG-05 — Member can view another member’s borrow tickets.** Members are able to view borrow tickets belonging to other members, causing a privacy and access-control breach.
- **BUG-06 — Email validation rejects valid email and accepts invalid email.** Email validation behavior is inconsistent during member creation. A valid email can be rejected, while invalid email data may be accepted into the database. This affects registration reliability and data quality.

**Medium**
- None.

**Low / Observation**
- None.

---

## 5. Đề xuất ưu tiên sửa lỗi

> 💡 Đây là phần **Quality Assurance**: bạn không chỉ tìm lỗi mà còn **đề xuất thứ tự ưu tiên** sửa chữa và đánh giá tác động.  
> Nêu rõ tiêu chí ưu tiên: dựa vào **severity** (mức độ nghiêm trọng kỹ thuật) và/hoặc **priority** (mức độ ưu tiên kinh doanh).

| Thứ tự | Bug | Mức độ | Lý do ưu tiên |
|--------|-----|--------|---------------|
| 1 | BUG-05 | High | This is a direct privacy and access-control issue because members can view borrow tickets belonging to other users. It should be fixed first to prevent unauthorized data exposure. |
| 2 | BUG-03 | High | This bug allows members to return books borrowed by other users. It can modify another user's borrow record and book status, causing data integrity and ownership issues. |
| 3 | BUG-06 | High | This affects member registration and database quality because valid emails may be rejected and invalid emails may be accepted. It can block core member-management functionality. |
| 4 | BUG-01 | High | Combined search is a core REQ-03 feature. Incorrect AND logic returns misleading results and makes search behavior unpredictable. |
| 5 | BUG-04 | Medium | Missing overdue warning violates overdue-return requirements and creates inconsistency between return and overdue checking behavior, although the core return process still works. |
| 6 | BUG-02 | Medium | Category filter case-sensitivity violates the SRS requirement and creates inconsistent behavior between the keyword bar and category bar. This should be fixed before release. |

---

## 6. Kết luận

The system is **not ready for release** in its current state.

Overall, the system demonstrates that several core workflows are functional: login works in normal cases, the book list displays correctly, basic search and filtering work in isolation, return status updates are performed correctly, duplicate returns are prevented, and overdue checking works for tested date conditions.

However, the system still contains several important issues that must be fixed before production release. The most serious problems are related to **access control, privacy, data integrity, and core search correctness**. In particular, members can view or modify records belonging to other members, combined search does not apply the required AND logic, and email validation is inconsistent during member creation.

Therefore, the group recommends fixing all **High** and **Medium** severity bugs before release, then retesting the affected requirements. Observations and requirement issues should also be clarified in the SRS or considered for later usability improvements.

---

## 7. Bài học rút ra (Tùy chọn)

- Building the **Input Domain Model (IDM)** before writing test cases helped the group identify important input partitions, boundary values, invalid cases, and edge cases more systematically.
- Testing multiple input orders is important when several fields interact. The combined search issue in REQ-03 was only discovered because different input orders were tested.
- Observation cases are still valuable even when they are outside the SRS scope. They reveal usability concerns such as diacritic-insensitive search and inconsistent partial matching behavior.
- Requirement ambiguity can affect test evaluation. Some cases could not be fully judged as pass or fail because the SRS did not clearly define the expected behavior.
- Access-control testing is critical for systems involving different user roles. Several serious issues were related to members accessing or modifying data that should belong to other users.
- Root cause analysis can help developers fix multiple related bugs more efficiently, especially when issues come from shared validation or filtering logic.
- Manual testing should be combined with unit and integration tests for validation rules, authorization checks, and search/filter behavior.

---

## 8. Khai báo sử dụng AI (Tùy chọn)

> Nếu nhóm có sử dụng công cụ AI (ChatGPT, Copilot, Gemini...), hãy ghi rõ bên dưới. Khai báo trung thực **không ảnh hưởng điểm** — đây là kỹ năng minh bạch trong nghề.

| Công cụ AI | Dùng cho phần nào | Bạn đã kiểm tra/chỉnh sửa thế nào |
|------------|-------------------|-----------------------------------|
| ChatGPT | Reviewing test cases, improving wording, organizing report structure, and merging documentation | All outputs were manually reviewed, adjusted, and verified against actual test results before being included in the final documentation. |
| Claude | Supporting IDM documentation, test case ideas, bug report wording, and report formatting | Suggestions were checked by group members and only used when they matched real observations from testing. |
| Gemini | Explaining testing concepts and supporting understanding of QA techniques | Concepts were manually applied to the group’s own test design and documentation. |
| GitHub Copilot | Supporting spelling correction and minor documentation editing | All generated or suggested content was reviewed and edited manually before saving. |