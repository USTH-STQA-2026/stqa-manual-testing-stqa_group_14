# Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | STQA-14 |
| **Ngày thực thi** | 24/05/2026 |
| **Trình duyệt** | Chrome |
| **Hệ điều hành** | Windows 10 |

---

## Kết quả chi tiết

| Mã TC | Nhóm chức năng | Kết quả mong đợi (tóm tắt) | Kết quả thực tế | Kết luận | Minh chứng | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-01 | Members | Tạo member hợp lệ | Hệ thống từ chối, báo "Email invalid" | Fail | | BUG-07 |
| TC-02 | Members | Từ chối email thiếu "." | Created Successfully | Fail | | BUG-07 |
| TC-03 | Members | Từ chối email thiếu "@" | Created Successfully | Fail | | BUG-07 |
| TC-04 | Members | Từ chối email trùng | Hệ thống từ chối (email exists) | Pass | | |
| TC-05 | Members | Member không thấy tab "Add member" | Tab không hiển thị / không truy cập được | Pass | | |
| TC-06 | Members | Tạo member với a@b.co thành công | Hệ thống từ chối (email invalid) | Fail | | BUG-07 |
| TC-07 | Borrow/Return | Hiển thị BR001–BR005 (Librarian) | Hiển thị đủ các phiếu | Pass | | |
| TC-08 | Borrow/Return | Member chỉ thấy BR001 & BR004 | Chỉ thấy BR001 & BR004 | Pass | | |
| TC-09 | Borrow/Return | Member không xem được ticket khác | Tickets của MEM003 hiển thị | Fail | | BUG-08 |
| TC-10 | Borrow/Return | Xem chi tiết BR001 đầy đủ | Hiển thị đầy đủ thông tin | Pass | | |
| TC-11 | Borrow/Return | BR002 hiển thị "Returned" | Hiển thị "Returned" | Pass | | |
| TC-12 | Borrow/Return | Check Overdue đánh dấu BR001 | BR001 chuyển thành "Overdue" khi tới hạn | Pass | | |
| TC-13 | Borrow/Return | BR002 vẫn "Returned" sau check | BR002 vẫn hiển thị "Returned" | Pass | | |
| TC-14 | Members | Từ chối email nhiều @ hoặc .. | Hệ thống từ chối (email invalid) | Pass | | |
| TC-15 | Members | Từ chối username trống | Hệ thống từ chối (Username blank) | Pass | | |

---

## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 15 |
| Pass | 10 |
| Fail | 5 |
| Blocked | 0 |
| Not Run | 0 |
| **Tỷ lệ Pass** | 66.7% |

### Kết quả theo nhóm chức năng

| Nhóm | Tổng TC | Pass | Fail | Tỷ lệ Pass |
|------|---------|------|------|------------|
| Members | 8 | 4 | 4 | 50% |
| Borrow/Return | 7 | 6 | 1 | 85.7% |
