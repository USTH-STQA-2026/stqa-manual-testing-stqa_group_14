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

### IDM — Return Book (REQ-05)

| Characteristic | Block / Partition | Representative Value | Expected Result |
|---|---|---|---|
| Borrow record status | Borrowing (active) | `BR001` | Allow return process |
| | Returned | `BR004` | Return action is not allowed |
| Due date compared to current date | `currentDate < dueDate` | `10/09/2024 < 15/09/2024` | Return successfully without overdue warning |
| | `currentDate = dueDate` (Boundary) | `15/09/2024 = 15/09/2024` | Return successfully and display overdue warning |
| | `currentDate > dueDate` | `27/05/2026 > 15/09/2024` | Return successfully and display overdue warning |
| Record owner | Record belongs to the current member | `BR001` belongs to `MEM002` | `MEM002` can return the book |
| | Record does not belong to the current member | `BR001` belongs to `MEM002`, current user is `MEM003` | `MEM003` cannot view or return the book |

### Decision Table — Return Book (REQ-05)

| Rule | Borrow Record Status | Due Date vs Current Date | Record Owner | Expected Result | Covered TC |
|---|---|---|---|---|---|
| R1 | Borrowing | `currentDate < dueDate` | Current member | Return successfully without overdue warning | TC-05-01 |
| R2 | Borrowing | `currentDate = dueDate` | Current member | Return successfully and display overdue warning | TC-05-02 |
| R3 | Borrowing | `currentDate > dueDate` | Current member | Return successfully and display overdue warning | TC-05-03 |
| R4 | Returned | Any | Current member | Return action is not allowed | TC-05-04 |
| R5 | Borrowing | Any | Another member | Return action is not allowed | TC-05-05 |

### IDM — Overdue Handling (REQ-06)

| Characteristic | Block / Partition | Representative Value | Expected Result |
|---|---|---|---|
| User role | Librarian | `librarian@library.com` | Can access **Check Overdue** function |
| | Member | `ba.nguyen@email.com` | Cannot access function |
| Due date compared to current date | `dueDate > currentDate` | `20/09/2024 > 15/09/2024` | Record is **not marked overdue** |
| | `dueDate = currentDate` (Boundary) | `15/09/2024 = 15/09/2024` | Record is marked **"Overdue"** |
| | `dueDate < currentDate` | `10/09/2024 < 15/09/2024` | Record is marked **"Overdue"** |
| Borrow record status | Borrowing | `Borrowing` | Eligible for overdue checking |
| | Returned | `Returned` | Not marked overdue / ignored |

---

## Bước 2: Test Cases

## Test Cases — REQ-05: Return Book

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|---|---|---|---|---|---|---|---|
| TC-05-01 | Return a currently borrowed, non-overdue book successfully | - Member has an active borrow record.<br>- A borrow record exists with `currentDate < dueDate`.<br>- The system date/time can be adjusted on the test machine. | 1. Set the system date to a date **before the record due date**.<br>2. Refresh the web page.<br>3. Log in as the member who owns the borrow record.<br>4. Open **Borrow / Return** page.<br>5. Select an active borrow record that is not overdue.<br>6. Click **Return Book**.<br>7. Confirm return action.<br>8. Open **Book List** and verify the book status. | Example record: `BR001`.<br>`currentDate < dueDate`.<br>Example: `10/09/2024 < 15/09/2024`. | - Book is returned successfully.<br>- No overdue warning message is displayed.<br>- Book status changes to **"Available"**.<br>- Borrow record status changes to **"Returned"**. | REQ-05 | EP, BVA, Decision Table |
| TC-05-02 | Return a book on the due date (boundary case) | - Member has an active borrow record.<br>- A borrow record exists with `currentDate = dueDate`.<br>- The system date/time can be adjusted on the test machine. | 1. Set the system date to the **same date as the borrow record due date**.<br>2. Refresh the web page.<br>3. Log in as the member who owns the borrow record.<br>4. Open **Borrow / Return** page.<br>5. Select a borrow record due today.<br>6. Click **Return Book**.<br>7. Observe whether an overdue warning is displayed. | Example record: `BR001`.<br>`currentDate = dueDate`.<br>Example: `15/09/2024 = 15/09/2024`. | - Book is returned successfully.<br>- System displays a clear overdue warning.<br>- Book status changes to **"Available"**.<br>- Borrow record status changes to **"Returned"**. | REQ-05 | BVA, Decision Table |
| TC-05-03 | Return an overdue book | - Member has an active borrow record.<br>- A borrow record exists with `currentDate > dueDate`.<br>- The system date/time can be adjusted on the test machine. | 1. Set the system date to a date **after the borrow record due date**.<br>2. Refresh the web page.<br>3. Log in as the member who owns the borrow record.<br>4. Open **Borrow / Return** page.<br>5. Select an overdue borrow record.<br>6. Click **Return Book**.<br>7. Observe whether an overdue warning is displayed. | Example record: `BR001`.<br>`currentDate > dueDate`.<br>Example: `27/05/2026 > 15/09/2024`. | - Book is returned successfully.<br>- System displays a **clear overdue warning**.<br>- Book status changes to **"Available"**.<br>- Borrow record status changes to **"Returned"**. | REQ-05 | EP, BVA, Decision Table |
| TC-05-04 | Return a book that has already been returned | - Member has a borrow record that has already been returned.<br>- Book status is **Available**. | 1. Log in as the member who owns the returned borrow record.<br>2. Open **Borrow / Return** page.<br>3. Select/view a borrow record with status **Returned**.<br>4. Check whether the return action is available. | Example record: `BR004`.<br>`recordStatus = Returned`. | - The system does not allow returning the same book again.<br>- The **Return Book** button is not displayed or cannot be used.<br>- Borrow record status remains **"Returned"**.<br>- Book status remains **"Available"**. | REQ-05 | EP, Negative Testing, Decision Table |
| TC-05-05 | Verify that a member cannot return another member’s borrowed book | - Login as a member account.<br>- Another member has an active borrow record.<br>- The borrow record does not belong to the current logged-in member. | 1. Login as `dam.tran@email.com` / `MEM003`.<br>2. Open **Borrow / Return** page.<br>3. Search for or try to access records belonging to another member, e.g. `MEM002`.<br>4. Try to view or select `BR001`, which belongs to `MEM002`.<br>5. If the **Return Book** button is available, click **Return Book**.<br>6. Observe whether the system allows the action. | Current user: `MEM003`.<br>Target record owner: `MEM002`.<br>Target record: `BR001`.<br>`recordOwner != currentUser`. | - The system must not allow `MEM003` to view or return `MEM002`’s borrow record.<br>- The **Return Book** button must not be displayed or must be disabled for records that do not belong to the current member.<br>- The borrow record status remains unchanged.<br>- The book status remains unchanged. | REQ-05, REQ-08 | EP, Negative Testing, Access Control, Decision Table |

---

## Test Cases — REQ-06: Overdue Handling

| TC ID | Test Objective | Preconditions | Test Steps | Input Data | Expected Result | REQ | Technique |
|---|---|---|---|---|---|---|---|
| TC-06-01 | Librarian can check overdue records | - Librarian account is logged in.<br>- Borrow records exist in the system. | 1. Login as librarian.<br>2. Open **Borrow / Return** page.<br>3. Click **Check Overdue** button.<br>4. Observe displayed records. | `librarian@library.com` | - Librarian can access and use the **Check Overdue** function.<br>- Overdue borrow records are displayed or updated after checking. | REQ-06 | EP |
| TC-06-02 | Check borrow record not overdue | - Librarian is logged in.<br>- A borrow record exists with `dueDate > current date`.<br>- The system date/time can be adjusted on the test machine. | 1. Set the system date to a date **before the record due date**.<br>2. Refresh the web page.<br>3. Login as librarian.<br>4. Open **Borrow / Return** page.<br>5. Click **Check Overdue** button.<br>6. Observe borrow record status. | `currentDate < dueDate`.<br>Example: `10/09/2024 < 15/09/2024`. | - Borrow record is **not marked as "Overdue"**.<br>- Status remains **"Borrowing"**. | REQ-06 | EP, BVA |
| TC-06-03 | Check borrow record due today (boundary case) | - Librarian is logged in.<br>- A borrow record exists with `dueDate = current date`.<br>- The system date/time can be adjusted on the test machine. | 1. Set the system date to the **same date as the borrow record due date**.<br>2. Refresh the web page.<br>3. Login as librarian.<br>4. Open **Borrow / Return** page.<br>5. Click **Check Overdue** button.<br>6. Observe borrow record status. | `currentDate = dueDate`.<br>Example: `15/09/2024 = 15/09/2024`. | - Borrow record is marked as **"Overdue"**.<br>- `dueDate <= currentDate` is considered overdue. | REQ-06 | BVA |
| TC-06-04 | Check overdue borrow record | - Librarian is logged in.<br>- A borrow record exists with `dueDate < current date`.<br>- The system date/time can be adjusted on the test machine. | 1. Set the system date to a date **after the record due date**.<br>2. Refresh the web page.<br>3. Login as librarian.<br>4. Open **Borrow / Return** page.<br>5. Click **Check Overdue** button.<br>6. Observe borrow record status. | `currentDate > dueDate`.<br>Example: `20/09/2024 > 15/09/2024`. | - Borrow record is marked as **"Overdue"**. | REQ-06 | EP, BVA |
| TC-06-05 | Member cannot use Check Overdue function | - Member account is logged in. | 1. Login as a member account.<br>2. Open **Borrow / Return** page.<br>3. Check whether the **Check Overdue** function is available.<br>4. Try to access or use the function if possible. | `ba.nguyen@email.com` / `MEM002` | - Member cannot access or use the **Check Overdue** function.<br>- The **Check Overdue** button is not displayed or cannot be used.<br>- Member cannot mark records as **"Overdue"**. | REQ-06 | EP |

---

## Summary

| Functional Group | Number of TCs | Covered REQ | Applied IDM Techniques |
|---|---:|---|---|
| Return Book | 5 | REQ-05, REQ-08 | EP, BVA, Decision Table, Negative Testing, Access Control |
| Overdue Handling | 5 | REQ-06 | EP, BVA |
| **Total** | **10** | **REQ-05 → REQ-06, REQ-08** | **EP, BVA, Decision Table, Negative Testing, Access Control** |
