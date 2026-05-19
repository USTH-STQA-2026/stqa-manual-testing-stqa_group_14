# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | `<!-- Tên nhóm -->` |
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
### IDM — Xem danh sách sách (REQ-02)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Người dùng có quyền xem danh sách sách? | Thủ thư | `Librarian` | Hiển thị danh sách sách |
| | Thành viên | `Member` | Hiển thị danh sách sách |
| Danh sách sách có dữ liệu không? | Có dữ liệu | `BOOK001` | Hiển thị danh sách sách |
| | Không có dữ liệu | `Empty list` | Hiển thị danh sách rỗng |
| Thông tin sách có đầy đủ không? | Đầy đủ | `Title + Author + Category + Year + Status` | Hiển thị đầy đủ thông tin |
| | Thiếu thông tin | `Missing author` | Hiển thị dữ liệu thiếu / báo lỗi |
| Trạng thái sách? | Có sẵn | `Available` | Hiển thị trạng thái "Có sẵn" |
| | Đã mượn | `Borrowed` | Hiển thị trạng thái "Đã mượn" |
| Cập nhật real-time? | Sách được mượn | `BOOK001 → Borrowed` | Trạng thái cập nhật ngay lập tức |
| | Sách được trả | `BOOK001 → Available` | Trạng thái cập nhật ngay lập tức |
|
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

### IDM — Trả sách (REQ-05)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Thành viên có đang mượn sách này? | Có | `RECORD001` | Cho phép trả sách |
| | Không | `RECORD999` | Từ chối trả sách |
| Sách có quá hạn không? | Không quá hạn | `returnDate < dueDate` | Trả thành công |
| | Đúng hạn | `returnDate = dueDate` | Trả thành công |
| | Quá hạn | `returnDate > dueDate` | Hiển thị cảnh báo quá hạn |
| Trạng thái sách sau trả? | Trả thành công | `BOOK001` | Chuyển sang trạng thái "Có sẵn" |

### IDM — Xử lý sách quá hạn (REQ-06)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Ai thực hiện thao tác? | Thủ thư | `Librarian` | Cho phép kiểm tra quá hạn |
| | Thành viên | `Member` | Không có quyền |
| DueDate so với ngày hiện tại? | `dueDate > today` | `20/06 > 15/06` | Không đánh dấu quá hạn |
| | `dueDate = today` | `15/06 = 15/06` | Đánh dấu "Quá hạn" |
| | `dueDate < today` | `10/06 < 15/06` | Đánh dấu "Quá hạn" |
| Quyền xem phiếu quá hạn? | Thủ thư | `Librarian` | Xem tất cả phiếu quá hạn |
| | Thành viên | `MEM001` | Chỉ xem phiếu của chính mình |

### IDM — Quản lý thành viên (REQ-07)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Người dùng có quyền thêm thành viên? | Thủ thư | `Librarian` | Cho phép thêm thành viên |
| | Thành viên | `Member` | Không cho phép |
| Email có hợp lệ? | Hợp lệ | `user@gmail.com` | Cho phép tạo |
| | Không có @ | `usergmail.com` | Thông báo lỗi |
| | Không có dấu . ở domain | `user@domain` | Thông báo lỗi |
| Email có bị trùng? | Không | `new@gmail.com` | Tạo thành công |
| | Có | `existing@gmail.com` | Thông báo lỗi email đã tồn tại |
| Input có đầy đủ? | Đầy đủ | `Name + Email + Phone` | Tạo thành công |
| | Thiếu thông tin | `Missing phone` | Thông báo lỗi |

### IDM — Tra cứu phiếu mượn (REQ-08)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Vai trò người dùng? | Thủ thư | `Librarian` | Xem tất cả phiếu mượn |
| | Thành viên | `Member` | Chỉ xem phiếu của mình |
| Thành viên có xem đúng phiếu không? | Phiếu của chính mình | `MEM001 → RECORD001` | Hiển thị thông tin |
| | Phiếu của người khác | `MEM001 → RECORD002 của MEM002` | Không cho phép truy cập |
| Trạng thái phiếu mượn? | Đang mượn | `Borrowing` | Hiển thị đúng trạng thái |
| | Đã trả | `Returned` | Hiển thị đúng trạng thái |
| | Quá hạn | `Overdue` | Hiển thị đúng trạng thái |
| Thông tin phiếu có đầy đủ? | Đầy đủ | `ID + Book + BorrowDate + DueDate + Status` | Hiển thị đầy đủ thông tin |


---

## Bước 2: Test Cases

<!-- Tự tổ chức bảng test case: có thể chia nhóm theo chức năng, theo REQ, hoặc theo luồng nghiệp vụ — tùy nhóm quyết định. -->
<!-- Mỗi TC phải ánh xạ ngược về ít nhất 1 dòng trong bảng IDM ở Bước 1. -->

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|-------|-------------------|---------------|---------------|-----------------|------------------|-----|---------|
| | | | | | | | |

---

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|----------------|-------|---------|----------------------|
| | | | |
| **Tổng** | **<!-- ≥ 20 -->** | | |
