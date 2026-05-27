# Test Summary — Báo cáo tổng hợp kiểm thử

> **Hướng dẫn**: Đây là hoạt động **Quality Assurance** — bạn đánh giá chất lượng tổng thể của phần mềm, không chỉ liệt kê lỗi.

---

## 1. Thông tin nhóm

| Mục | Thông tin |
|-----|----------|
| **Nhóm** | STQA-14 |
| **Lớp** | `<!-- VD: SE001.P11 -->` |
| **Ngày báo cáo** | `<!-- DD/MM/YYYY -->` |
| **Hệ thống kiểm thử** | https://stqa.rbc.vn — v1.0 |

---

## 2. Tổng quan kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 15 |
| Pass | 10 |
| Fail | 5 |
| Blocked | 0 |
| Not Run | 0 |
| **Tỷ lệ Pass** | 50% |
| **Số bug phát hiện** | 2 |

### Phân bổ theo nhóm chức năng

| Nhóm chức năng | TC | Pass | Fail | Bug | Đánh giá |
|---------------|-----|------|------|-----|---------|
| Members | 8 | 4 | 4 | BUG-07 | Cần sửa: email validation gây từ chối sai |
| Borrow/Return | 7 | 6 | 1 | BUG-08 | Cần sửa: phân quyền/search lọc theo member |

### Phân bổ bug theo mức độ

| Mức độ | Số lượng | Bug IDs |
|--------|---------|---------|
| High | 2 | BUG-07, BUG-08 |
| Medium | 0 | |
| Low | 0 | |

---

## 3. Kỹ thuật thiết kế đã sử dụng

| Kỹ thuật | Áp dụng cho REQ nào? | Số TC sử dụng | Giải thích cách áp dụng |
|----------|---------------------|---------------|------------------------|
| EP (Equivalence Partitioning) | REQ-07, REQ-08 | 12 | Dùng để nhóm dữ liệu rời rạc (valid/invalid emails, roles) |
| BVA (Boundary Value Analysis) | REQ-07 | 3 | Áp dụng cho kiểm tra độ dài/định dạng email, số điện thoại |

---

## 4. Phân tích chất lượng phần mềm

### 4.1. Điểm mạnh
`- Core workflows mostly functional: adding members and borrow/return flows operate correctly for the majority of cases.`

`- IDM analysis applied: tests cover valid/invalid partitions and boundary values for member inputs.`

### 4.2. Điểm yếu
`- Two high-severity issues found:`
`  - BUG-07: Email validation currently rejects a valid email during member creation (blocks registrations) and accept invalid email into database.`
`  - BUG-08: Members can view other members' borrow tickets (data privacy / access control breach).`

---

## 5. Đề xuất ưu tiên sửa lỗi

> 💡 Đây là phần **Quality Assurance**: bạn không chỉ tìm lỗi mà còn **đề xuất thứ tự ưu tiên** sửa chữa và đánh giá tác động.
> Nêu rõ tiêu chí ưu tiên: dựa vào **severity** (mức độ nghiêm trọng kỹ thuật) và/hoặc **priority** (mức độ ưu tiên kinh doanh).

| Thứ tự | Bug | Mức độ | Lý do ưu tiên |
|--------|-----|--------|---------------|
| 1 | BUG-08 | High | Data privacy breach — immediate security/privacy risk |
| 2 | BUG-07 | High | Blocks core functionality (member registration) — business impact |

**Gợi ý xử lý ngắn:**
- BUG-08: Thực thi kiểm tra phân quyền ở server/data layer, thêm unit/integration test cho search API.
- BUG-07: Kiểm tra/điều chỉnh regex/validator email phía backend, thêm test cases cho email giới hạn và quốc tế hóa.

---

## 6. Kết luận

Hệ thống **chưa sẵn sàng phát hành**. Hai vấn đề thân trọng (privacy + registration) cần được khắc phục và retest trước release.

---

## 7. Bài học rút ra (Tùy chọn)

`- Thiết kế IDM trước khi viết TC giúp phát hiện các kịch bản biên và trường hợp xấu.
`- Cần bổ sung test tự động (unit & integration) cho validation và phân quyền truy xuất dữ liệu.

---

## 8. Khai báo sử dụng AI (Tùy chọn)

> Nếu nhóm có sử dụng công cụ AI (ChatGPT, Copilot, Gemini...), hãy ghi rõ bên dưới. Khai báo trung thực **không ảnh hưởng điểm** — đây là kỹ năng minh bạch trong nghề.

| Công cụ AI | Dùng cho phần nào | Bạn đã kiểm tra/chỉnh sửa thế nào |
|------------|-------------------|-----------------------------------|
| | | |
| Công cụ AI | Dùng cho phần nào | Bạn đã kiểm tra/chỉnh sửa thế nào |
|------------|-------------------|-----------------------------------|
| GitHub Copilot | Sửa lỗi, điều chỉnh chính tả tài liệu | Xem lại và chỉnh sửa thủ công trước khi lưu |
| Claud AI | Tìm Bug | Nhờ gợi ý những test cases chưa nghĩ đến |