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

## Test Cases — REQ-05: Trả sách / Return Book

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|---|---|---|---|---|---|---|---|
| TC-05-01 | Trả sách đang được thành viên mượn | Thành viên đã đăng nhập. Thành viên đang mượn `BOOK001` với phiếu `RECORD001` | 1. Mở trang phiếu mượn. 2. Chọn phiếu `RECORD001`. 3. Nhấn nút Trả sách. 4. Xác nhận trả sách. | `RECORD001`, `BOOK001` | Trả sách thành công. Trạng thái sách chuyển sang `"Có sẵn"`. Trạng thái phiếu chuyển sang `"Đã trả"`. | REQ-05 | EP |
| TC-05-02 | Không cho trả sách mà thành viên không mượn | Thành viên đã đăng nhập. `BOOK009` không nằm trong danh sách sách đang mượn của thành viên | 1. Mở trang phiếu mượn. 2. Thử trả sách/phiếu không thuộc thành viên hiện tại. 3. Nhấn Trả sách. | `RECORD999`, `BOOK009` | Hệ thống từ chối trả sách. Không thay đổi trạng thái sách. | REQ-05 | EP |
| TC-05-03 | Trả sách đúng hạn | Thành viên đang mượn `BOOK001`. `returnDate` nhỏ hơn hoặc bằng `dueDate` | 1. Mở phiếu mượn `RECORD001`. 2. Nhấn Trả sách. 3. Xác nhận trả sách. | `returnDate = 14/06/2026`, `dueDate = 15/06/2026` | Trả sách thành công. Không hiển thị cảnh báo quá hạn. | REQ-05 | EP, BVA |
| TC-05-04 | Trả sách quá hạn | Thành viên đang mượn `BOOK001`. `returnDate` lớn hơn `dueDate` | 1. Mở phiếu mượn `RECORD002`. 2. Nhấn Trả sách. 3. Xác nhận trả sách. | `returnDate = 16/06/2026`, `dueDate = 15/06/2026` | Trả sách thành công. Hệ thống hiển thị cảnh báo quá hạn. Sách chuyển về `"Có sẵn"`. | REQ-05 | EP, BVA |

## Test Cases — REQ-06: Xử lý sách quá hạn / Overdue Handling

| Mã TC | Mục tiêu kiểm thử | Tiền điều kiện | Bước thực hiện | Dữ liệu đầu vào | Kết quả mong đợi | REQ | Kỹ thuật |
|---|---|---|---|---|---|---|---|
| TC-06-01 | Thủ thư kiểm tra phiếu chưa quá hạn | Thủ thư đã đăng nhập. Có phiếu mượn với `dueDate > today` | 1. Mở trang quản lý phiếu mượn. 2. Nhấn nút Kiểm tra quá hạn. 3. Quan sát trạng thái phiếu. | `today = 15/06/2026`, `dueDate = 20/06/2026` | Phiếu không bị đánh dấu `"Quá hạn"`. Trạng thái vẫn là `"Đang mượn"`. | REQ-06 | EP, BVA |
| TC-06-02 | Thủ thư kiểm tra phiếu có dueDate bằng ngày hiện tại | Thủ thư đã đăng nhập. Có phiếu mượn với `dueDate = today` | 1. Mở trang quản lý phiếu mượn. 2. Nhấn nút Kiểm tra quá hạn. 3. Quan sát trạng thái phiếu. | `today = 15/06/2026`, `dueDate = 15/06/2026` | Phiếu được đánh dấu `"Quá hạn"`. | REQ-06 | BVA |
| TC-06-03 | Thủ thư kiểm tra phiếu đã quá hạn | Thủ thư đã đăng nhập. Có phiếu mượn với `dueDate < today` | 1. Mở trang quản lý phiếu mượn. 2. Nhấn nút Kiểm tra quá hạn. 3. Quan sát trạng thái phiếu. | `today = 15/06/2026`, `dueDate = 10/06/2026` | Phiếu được đánh dấu `"Quá hạn"`. | REQ-06 | EP, BVA |
| TC-06-04 | Thủ thư xem tất cả phiếu quá hạn | Thủ thư đã đăng nhập. Hệ thống có nhiều phiếu quá hạn của nhiều thành viên | 1. Đăng nhập bằng tài khoản thủ thư. 2. Mở trang phiếu quá hạn. 3. Quan sát danh sách hiển thị. | `Librarian`, `RECORD001`, `RECORD002` | Thủ thư xem được tất cả phiếu quá hạn của mọi thành viên. | REQ-06 | EP |
| TC-06-05 | Thành viên chỉ xem phiếu quá hạn của chính mình | Thành viên `MEM001` đã đăng nhập. Có phiếu quá hạn của `MEM001` và `MEM002` | 1. Đăng nhập bằng tài khoản `MEM001`. 2. Mở trang phiếu mượn/quá hạn. 3. Quan sát danh sách hiển thị. | `MEM001`, `RECORD001 của MEM001`, `RECORD002 của MEM002` | Thành viên chỉ thấy phiếu quá hạn của chính mình. Không thấy phiếu của thành viên khác. | REQ-06 | EP |

## Tổng hợp

| Nhóm chức năng | Số TC | REQ phủ | Kỹ thuật IDM áp dụng |
|---|---:|---|---|
| Trả sách | 4 | REQ-05 | EP, BVA |
| Xử lý sách quá hạn | 5 | REQ-06 | EP, BVA |
| **Tổng** | **9** | **REQ-05 → REQ-06** | **EP, BVA** |
