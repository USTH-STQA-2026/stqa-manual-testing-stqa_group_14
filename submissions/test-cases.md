# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | STQA-14 |
| **Ngày tạo** | `<!-- DD/MM/YYYY -->` |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Email có tồn tại trong DB? | Có | `librarian@library.com` | Đăng nhập thành công |
| | Không | `noone@email.com` | Thông báo lỗi |
| Mật khẩu có đúng? | Đúng | `admin123` | Đăng nhập thành công |
| | Sai | `wrongpass` | Thông báo lỗi |
| Ô nhập có rỗng? | Không rỗng | (giá trị bất kỳ) | Xử lý bình thường |
| | Rỗng | `""` | Thông báo "Vui lòng nhập..." |

### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

### IDM — Mượn sách (REQ-04, REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Có sẵn | BOOK001 | Cho phép mượn |
| | Đang mượn | BOOK003 | Không cho phép |
| | Thất lạc | BOOK007 | Không cho phép |
| Trạng thái thành viên? | Hoạt động | MEM002 | Cho phép mượn |
| | Tạm ngưng | MEM004 | Từ chối, thông báo lỗi |
| | Hết hạn | MEM005 | Từ chối, thông báo lỗi |
| Số sách đang mượn? | < 3 (BVA: 0, 1, 2) | MEM006 (0 sách) | Cho phép mượn |
| | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách | Từ chối, thông báo vượt giới hạn |

### IDM — Members (REQ-07)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Username | Hợp lệ | "Kevin Hart" | Chấp nhận (Accept) |
| Username | Chỉ khoảng trắng | "   " (3 spaces) | Từ chối, hiển thị "Please enter your username" |
| Username | Blank | (blank) | Từ chối, hiển thị "Please enter your username" |
| Email | Hợp lệ | member@so.com | Chấp nhận |
| Email | Thiếu @ | memberso.com | Từ chối, hiển thị "Please enter your email" |
| Email | Thiếu . | member@socom | Từ chối, hiển thị "Please enter your email" |
| Email | Blank | (blank) | Từ chối, hiển thị "Please enter your email" |
| Phone number | Đúng 10 chữ số | 0988743321 | Chấp nhận |
| Phone number | Không đủ 10 chữ số | 09283189 | Từ chối, hiển thị "Please enter your phone number" |
| Phone number | Chứa chữ | abcxyz | Từ chối, hiển thị "Please enter your phone number" |
| Ability to add member | Admin | librarian@library.com | Cho phép thêm |
| Ability to add member | Member | ba.nguyen@email.com | Không cho phép |

### IDM — Search borrow tickets (REQ-08)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Role | Librarian | librarian@library.com | Hiển thị tất cả ticket |
| Role | Active member | ba.nguyen@email.com (MEM002) | Chỉ hiển thị ticket của MEM002 |
| Role | Suspended member | cu.le@email.com (MEM004) | Chỉ hiển thị ticket của MEM004 |
| Search member ID | Librarian tìm MEM002/MEM003/MEM006 | MEM002, MEM003, MEM006 | Hiển thị tất cả ticket tương ứng |
| Search member ID | Member tìm chính họ | MEM002 tìm MEM002 | Hiển thị lịch sử mượn của MEM002 |
| Search member ID | Member tìm người khác | MEM002 tìm MEM003 | Không hiển thị ticket, thông báo "Not found" |
| Search member ID | ID không tồn tại | MEM099 | Thông báo "Not exist" hoặc "Not found" |
| Borrow record ID | ID tồn tại - Borrowed | BR001 | Hiển thị trạng thái tương ứng |
| Borrow record ID | ID tồn tại - Returned | BR002 | Hiển thị thông báo "Returned" |
| Borrow record ID | ID tồn tại - Expired | BR001 (sau check overdue) | Hiển thị thông báo "Expired" |
| Borrow record ID | ID không tồn tại | BR369 | Thông báo "Not found" |
| Borrow history | Có lịch sử | MEM002 có BR001, BR004 | Hiển thị lịch sử mượn |
| Borrow history | Chưa mượn | New member | Danh sách rỗng |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| TC-01 | Thêm thành viên mới hợp lệ | Đăng nhập bằng tài khoản Librarian | 1. Vào tab Members<br>2. Click "Add member"<br>3. Điền thông tin<br>4. Xác nhận | Username: Nguyễn Văn Test<br>Email: newmember@test.com<br>Phone: 0901234567 | Thành viên được tạo thành công, xuất hiện trong danh sách | REQ-07 | EP |
| TC-02 | Thêm thành viên với email thiếu dấu chấm trong domain | Đăng nhập Librarian | 1. Vào Members<br>2. Click Add<br>3. Nhập email user@domain<br>4. Xác nhận | Email: user@domain | Hệ thống từ chối, thông báo lỗi email không hợp lệ | REQ-07 | BVA |
| TC-03 | Thêm thành viên với email thiếu @ | Đăng nhập Librarian | 1. Vào Members<br>2. Click Add<br>3. Nhập email userdomain.com<br>4. Xác nhận | Email: userdomain.com | Hệ thống từ chối, thông báo lỗi email không hợp lệ | REQ-07 | BVA |
| TC-04 | Thêm thành viên trùng email | Đăng nhập Librarian | 1. Vào Members<br>2. Click Add<br>3. Nhập email đã tồn tại (ba.nguyen@email.com)<br>4. Xác nhận | Email: ba.nguyen@email.com | Hệ thống từ chối, thông báo email đã tồn tại | REQ-07 | EP |
| TC-05 | Kiểm tra quyền Member không thấy tab Members | Đăng nhập bằng tài khoản Member (ba.nguyen) | 1. Đăng nhập bằng MEM002<br>2. Quan sát các tab hiển thị | (không cần nhập thêm) | Tab "Members" không xuất hiện hoặc không truy cập được | REQ-07 | EP |
| TC-06 | Email ngắn nhất hợp lệ (BVA) | Đăng nhập Librarian | 1. Vào Members<br>2. Click Add<br>3. Nhập email a@b.co<br>4. Xác nhận | Email: a@b.co<br>Phone: 0900000001 | Thành viên được tạo thành công | REQ-07 | BVA |
| TC-07 | Hiển thị danh sách phiếu mượn (Librarian) | Đăng nhập Librarian | 1. Đăng nhập Librarian<br>2. Vào tab Borrow/Return<br>3. Quan sát danh sách | (không cần dữ liệu) | Hiển thị đủ BR001–BR005 cho tất cả thành viên | REQ-08 | EP |
| TC-08 | Hiển thị phiếu mượn cho Member (chỉ của họ) | Đăng nhập MEM002 | 1. Đăng nhập MEM002<br>2. Vào Borrow/Return<br>3. Quan sát danh sách | (MEM002) | Chỉ thấy BR001 và BR004 (của MEM002) | REQ-08 | EP |
| TC-09 | Tìm kiếm phiếu mượn của thành viên khác (không cho phép) | Đăng nhập MEM002 | 1. Đăng nhập MEM002<br>2. Vào Borrow/Return<br>3. Tìm ID MEM003 | Tìm MEM003 | Không hiển thị ticket của MEM003; hoặc thông báo "Not found" | REQ-08 | EP, BUG |
| TC-10 | Xem chi tiết phiếu BR001 | Đăng nhập Librarian | 1. Đăng nhập Librarian<br>2. Vào Borrow/Return<br>3. Mở BR001 | BR001 | Hiển thị đầy đủ: mã, sách, ngày mượn, ngày trả, trạng thái | REQ-08 | EP |
| TC-11 | Xem phiếu BR002 (đã trả) | Đăng nhập Librarian hoặc MEM003 | 1. Đăng nhập<br>2. Vào Borrow/Return<br>3. Mở BR002 | BR002 (đã trả 20/08/2024) | Trạng thái hiển thị "Returned" | REQ-08 | EP |
| TC-12 | Kiểm tra đánh dấu quá hạn (Check Overdue) | Đăng nhập Librarian | 1. Đăng nhập Librarian<br>2. Click "Check Overdue"<br>3. Vào Borrow/Return, mở BR001 | BR001 (expiry 15/09/2024) | BR001 được chuyển trạng thái thành "Overdue" nếu đến hạn | REQ-06, REQ-08 | EP |
| TC-13 | Kiểm tra BR002 hiển thị đúng trạng thái sau check overdue | Đăng nhập Librarian | 1. Đăng nhập Librarian<br>2. Check Overdue<br>3. Mở BR002 | BR002 (returned) | BR002 vẫn hiển thị "Returned" | REQ-08 | EP |
| TC-14 | Thêm member với email có nhiều @ hoặc nhiều dấu chấm liên tiếp | Đăng nhập Librarian | 1. Click Add member<br>2. Nhập email admin@@vn.com hoặc admin@vn..com<br>3. Xác nhận | Email: admin@@vn.com / admin@vn..com | Hệ thống từ chối, thông báo lỗi email không hợp lệ | REQ-07 | EP |
| TC-15 | Thêm member với username trống | Đăng nhập Librarian | 1. Click Add member<br>2. Để trống Username<br>3. Xác nhận | Username: (blank), Email: admin@vn.com | Hệ thống từ chối, thông báo "Username blank" | REQ-07 | EP |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| Members | 9 | REQ-07 | EP, BVA |
| Borrow/Return | 6 | REQ-06, REQ-08 | EP |
| **Tổng** | **15** | REQ-06 → REQ-08 | EP, BVA |
