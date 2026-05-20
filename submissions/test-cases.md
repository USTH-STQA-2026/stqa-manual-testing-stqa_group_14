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

## Test Cases — REQ-05: Return Book

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|---|---|---|---|---|---|---|---|
| TC-05-01 | Return a borrowed book successfully | - Member `MEM002 (Nguyễn Học Bá)` is logged in.<br>- Book `BOOK003` is currently borrowed by the member. | 1. Open **Borrow / Return** page.<br>2. Locate borrowed record `BR001`.<br>3. Click **Return Book**.<br>4. Confirm return action. | `BR001`<br>`BOOK003` | - Book is returned successfully.<br>- Book status changes to **"Available"**.<br>- Borrow record status changes to **"Returned"**. | REQ-05 | EP |
| TC-05-02 | Return a book before overdue date | - Member `MEM002` is logged in and has an active borrow record.<br>- `returnDate < dueDate`. | 1. Open **Borrow / Return** page.<br>2. Select an active borrow record.<br>3. Click **Return Book**. | `returnDate = 14/06/2026`<br>`dueDate = 15/06/2026` | - Book is returned successfully.<br>- No overdue warning message is displayed.<br>- Book status changes to **"Available"**. | REQ-05 | EP, BVA |
| TC-05-03 | Return a book on the due date (boundary case) | - Member has an active borrow record.<br>- `returnDate = dueDate`. | 1. Open **Borrow / Return** page.<br>2. Select an active borrow record.<br>3. Click **Return Book**. | `returnDate = 15/06/2026`<br>`dueDate = 15/06/2026` | - Book is returned successfully.<br>- System displays a **clear overdue warning**.<br>- `dueDate <= today` is considered overdue. | REQ-05 | BVA |
| TC-05-04 | Return an overdue book | - Member has an active borrow record.<br>- `returnDate > dueDate`. | 1. Open **Borrow / Return** page.<br>2. Select overdue borrow record.<br>3. Click **Return Book**. | `returnDate = 16/06/2026`<br>`dueDate = 15/06/2026` | - Book is returned successfully.<br>- System displays a **clear overdue warning**.<br>- Book status changes to **"Available"**.<br>- Borrow record status changes to **"Returned"**. | REQ-05 | EP, BVA |
| TC-05-05 | Member cannot access borrow records of other members | - Member `MEM002` is logged in.<br>- Another member (`MEM003`) has borrow records. | 1. Login as `MEM002`.<br>2. Open **Borrow / Return** page.<br>3. Observe displayed borrow records. | `MEM002`<br>`records of MEM003` | - Member only sees their own borrow records.<br>- Borrow records of other members are not displayed and cannot be returned. | REQ-05, REQ-08 | EP |

## Test Cases — REQ-06: Overdue Handling

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|---|---|---|---|---|---|---|---|
| TC-06-01 | Check borrow record not overdue | - Librarian is logged in.<br>- A borrow record exists with `dueDate > today`. | 1. Open **Borrow Records Management** page.<br>2. Click **Check Overdue** button.<br>3. Observe borrow record status. | `today = 15/06/2026`<br>`dueDate = 20/06/2026` | - Borrow record is **not marked as "Overdue"**.<br>- Status remains **"Borrowing"**. | REQ-06 | EP, BVA |
| TC-06-02 | Check borrow record due today (boundary case) | - Librarian is logged in.<br>- A borrow record exists with `dueDate = today`. | 1. Open **Borrow Records Management** page.<br>2. Click **Check Overdue** button.<br>3. Observe borrow record status. | `today = 15/06/2026`<br>`dueDate = 15/06/2026` | - Borrow record is marked as **"Overdue"**.<br>- `dueDate <= today` is considered overdue. | REQ-06 | BVA |
| TC-06-03 | Check overdue borrow record | - Librarian is logged in.<br>- A borrow record exists with `dueDate < today`. | 1. Open **Borrow Records Management** page.<br>2. Click **Check Overdue** button.<br>3. Observe borrow record status. | `today = 15/06/2026`<br>`dueDate = 10/06/2026` | - Borrow record is marked as **"Overdue"**. | REQ-06 | EP, BVA |
| TC-06-04 | Librarian can view all overdue records | - Librarian account is logged in.<br>- Multiple overdue records exist from different members. | 1. Login as librarian.<br>2. Open **Overdue Records** page.<br>3. Observe displayed records. | `librarian@library.com` | - Librarian can view **all overdue borrow records** from all members. | REQ-06 | EP |
| TC-06-05 | Member can only view their own overdue records | - Member `MEM002` is logged in.<br>- Overdue records exist for both `MEM002` and `MEM003`. | 1. Login as `MEM002`.<br>2. Open **Borrow / Return** page.<br>3. Observe displayed records. | `MEM002` | - Member only sees their own overdue records.<br>- Records belonging to other members are not displayed. | REQ-06 | EP |

## Summary

| Functional Group | Number of TCs | Covered REQ | Applied IDM Techniques |
|---|---:|---|---|
| Return Book | 5 | REQ-05 | EP, BVA |
| Overdue Handling | 5 | REQ-06 | EP, BVA |
| **Total** | **10** | **REQ-05 → REQ-06** | **EP, BVA** |
