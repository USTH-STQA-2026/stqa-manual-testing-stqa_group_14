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
| Email | Thiếu @ or Thiếu . | memberso.com or member@socom | Từ chối, hiển thị "Please enter your email" |
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
|  | Active member | ba.nguyen@email.com (MEM002) | Chỉ hiển thị ticket của MEM002 |
|  | Suspended member | cu.le@email.com (MEM004) | Chỉ hiển thị ticket của MEM004 |
| Search member ID | Librarian tìm MEM002/MEM003/MEM006 | MEM002, MEM003, MEM006 | Hiển thị tất cả ticket tương ứng |
|  | Member tìm chính họ | MEM002 tìm MEM002 | Hiển thị lịch sử mượn của MEM002 |
|  | Member tìm người khác | MEM002 tìm MEM003 | Không hiển thị ticket, thông báo "Not found" |
|  | ID không tồn tại | MEM099 | Thông báo "Not exist" hoặc "Not found" |
| Borrow record ID | ID tồn tại - Borrowed | BR001 | Hiển thị trạng thái tương ứng |
|  | ID tồn tại - Returned | BR002 | Hiển thị thông báo "Returned" |
|  | ID tồn tại - Expired | BR001 (sau check overdue) | Hiển thị thông báo "Expired" |
|  | ID không tồn tại | BR369 | Thông báo "Not found" |
| Borrow history | Có lịch sử | MEM002 có BR001, BR004 | Hiển thị lịch sử mượn |
| Borrow history | Chưa mượn | New member | Danh sách rỗng |

> 💡 **Gợi ý kỹ thuật**: Sử dụng **Phân lớp tương đương (EP)** cho các phân vùng rời rạc, **Phân tích giá trị biên (BVA)** cho các phân vùng số (ví dụ: giới hạn 3 sách). Xem textbook §6.1–6.3.

---

## Step 2: Test Cases

<!-- Organize test case table yourself: can be grouped by function, by REQ, or by business flow — depends on group decision. -->
<!-- Each TC must map back to at least 1 row in the IDM table in Step 1. -->

| Test Case ID | Test Objective | Pre-condition | Test Steps | Input Data | Expected Result | REQ | Technique |
|---|---|---|---|---|---|---|---|
| TC-01 | Add new valid member | Login with Librarian account | 1. Go to Members tab<br>2. Click "Add member"<br>3. Fill in information<br>4. Confirm | Username: Nguyen Van Test<br>Email: newmember@test.com<br>Phone: 0901234567 | Member is created successfully, appears in list | REQ-07 | EP |
| TC-02 | Add member with email missing dot in domain | Login as Librarian | 1. Go to Members<br>2. Click Add<br>3. Enter email user@domain<br>4. Confirm | Email: user@domain | System rejects, displays email error message | REQ-07 | BVA |
| TC-03 | Add member with email missing @ | Login as Librarian | 1. Go to Members<br>2. Click Add<br>3. Enter email userdomain.com<br>4. Confirm | Email: userdomain.com | System rejects, displays email error message | REQ-07 | BVA |
| TC-04 | Add member with duplicate email | Login as Librarian | 1. Go to Members<br>2. Click Add<br>3. Enter existing email (ba.nguyen@email.com)<br>4. Confirm | Email: ba.nguyen@email.com | System rejects, displays email already exists message | REQ-07 | EP |
| TC-05 | Check Member permission cannot see Members tab | Login with Member account (ba.nguyen) | 1. Login with MEM002<br>2. Observe displayed tabs | (no additional input needed) | "Members" tab does not appear or is not accessible | REQ-07 | EP |
| TC-06 | Shortest valid email (BVA) | Login as Librarian | 1. Go to Members<br>2. Click Add<br>3. Enter email a@b.co<br>4. Confirm | Email: a@b.co<br>Phone: 0900000001 | Member is created successfully | REQ-07 | BVA |
| TC-07 | Display borrow ticket list (Librarian) | Login as Librarian | 1. Login as Librarian<br>2. Go to Borrow/Return tab<br>3. Observe list | (no data input needed) | Display BR001–BR005 for all members | REQ-08 | EP |
| TC-08 | Display borrow ticket for Member (only theirs) | Login as MEM002 | 1. Login as MEM002<br>2. Go to Borrow/Return<br>3. Observe list | (MEM002) | Only see BR001 and BR004 (belonging to MEM002) | REQ-08 | EP |
| TC-09 | Search borrow ticket of another member (not allowed) | Login as MEM002 | 1. Login as MEM002<br>2. Go to Borrow/Return<br>3. Search for ID MEM003 | Search for MEM003 | Does not display MEM003 tickets; or displays "Not found" message | REQ-08 | EP, BUG |
| TC-10 | View details of ticket BR001 | Login as Librarian | 1. Login as Librarian<br>2. Go to Borrow/Return<br>3. Open BR001 | BR001 | Display complete: code, book, borrow date, return date, status | REQ-08 | EP |
| TC-11 | View ticket BR002 (returned) | Login as Librarian or MEM003 | 1. Login<br>2. Go to Borrow/Return<br>3. Open BR002 | BR002 (returned 20/08/2024) | Status displays "Returned" | REQ-08 | EP |
| TC-12 | Check overdue marking (Check Overdue) | Login as Librarian | 1. Login as Librarian<br>2. Click "Check Overdue"<br>3. Go to Borrow/Return, open BR001 | BR001 (expiry 15/09/2024) | BR001 status is changed to "Overdue" if expired | REQ-06, REQ-08 | EP |
| TC-13 | Check BR002 displays correct status after check overdue | Login as Librarian | 1. Login as Librarian<br>2. Check Overdue<br>3. Open BR002 | BR002 (returned) | BR002 still displays "Returned" | REQ-08 | EP |
| TC-14 | Add member with email having multiple @ or consecutive dots | Login as Librarian | 1. Click Add member<br>2. Enter email admin@@vn.com or admin@vn..com<br>3. Confirm | Email: admin@@vn.com / admin@vn..com | System rejects, displays email error message | REQ-07 | EP |
| TC-15 | Add member with blank username | Login as Librarian | 1. Click Add member<br>2. Leave Username blank<br>3. Confirm | Username: (blank), Email: admin@vn.com | System rejects, displays "Username blank" message | REQ-07 | EP |

---

## Summary

| Function Group | Number of TC | REQ Coverage | IDM Technique Applied |
|----------------|-------|---------|----------------------|
| Members | 9 | REQ-07 | EP, BVA |
| Borrow/Return | 6 | REQ-06, REQ-08 | EP |
| **Total** | **15** | REQ-06 → REQ-08 | EP, BVA |
