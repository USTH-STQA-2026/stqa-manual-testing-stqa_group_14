# Test Cases — Test Cases Table

> **Instructions**: Write at least **20 TC** covering all main functions (REQ-01 → REQ-08).
> See [examples/sample-test-case.md](../examples/sample-test-case.md) to understand how to write good TC.
> Organize and group test cases in the most logical way.

| Information | |
|---|---|
| **Group** | STQA-14 |
| **Creation Date** | `<!-- DD/MM/YYYY -->` |
| **System** | https://stqa.rbc.vn |
| **Reference** | SRS v1.0 |

---

## Step 1: Input Domain Modeling — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chapter 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Before writing Test Cases**, the group **must** analyze the input domain using the IDM table below.
> Each function needs to identify: **Characteristic**, **Partition**, and **Representative Value**.

### IDM — Login (REQ-01)

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| Email exists in DB? | Yes | `librarian@library.com` | Login successful |
| | No | `noone@email.com` | Error message |
| Password correct? | Yes | `admin123` | Login successful |
| | No | `wrongpass` | Error message |
| Input field empty? | Not empty | (any value) | Normal processing |
| | Empty | `""` | Display "Please enter..." |

### IDM — Search book (REQ-03)

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| Keyword exists in DB? | Yes (book name) | `"Flutter"` | Display books containing "Flutter" |
| | Yes (author name) | `"Nguyen"` | Display books by author Nguyen |
| | No | `"XYZ123"` | Empty list |
| Case-sensitive? | Lowercase | `"flutter"` | Results same as "Flutter" |
| | Uppercase | `"FLUTTER"` | Results same as "Flutter" |

### IDM — Borrow book (REQ-04, REQ-05)

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| Book status? | Available | BOOK001 | Allow borrow |
| | Borrowed | BOOK003 | Not allowed |
| | Lost | BOOK007 | Not allowed |
| Member status? | Active | MEM002 | Allow borrow |
| | Suspended | MEM004 | Reject, display error |
| | Expired | MEM005 | Reject, display error |
| Books currently borrowed? | < 3 (BVA: 0, 1, 2) | MEM006 (0 books) | Allow borrow |
| | = 3 (BVA: limit) | Member borrowed 3 books | Reject, display limit exceeded |

### IDM — Members (REQ-07)

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| Username | Valid | "Kevin Hart" | Accept |
|  | Only spaces | "   " (3 spaces) | Reject, display "Please enter your username" |
|  | Blank | (blank) | Reject, display "Please enter your username" |
| Email | Valid | member@so.com | Accept |
|  | Missing @ or . | memberso.com or member@socom | Reject, display "Please enter your email" |
|  | Blank | (blank) | Reject, display "Please enter your email" |
| Phone number | Exactly 10 digits | 0988743321 | Accept |
|  | Less than 10 digits | 09283189 | Reject, display "Please enter your phone number" |
|  | Contains letters | abcxyz | Reject, display "Please enter your phone number" |
|  | Not start with 0 | 9849927236 | Reject, display "Please enter your phone number" |
| Ability to add member | Admin | librarian@library.com | Allow add |
|  | Member | ba.nguyen@email.com | Not allowed |

### IDM — Search borrow tickets (REQ-08)

| Characteristic | Partition | Representative Value | Expected Result |
|---|---|---|---|
| Role | Librarian | librarian@library.com | Display all tickets |
| | Active member | ba.nguyen@email.com (MEM002) | Only display MEM002 tickets |
| | Suspended member | cu.le@email.com (MEM004) | Only display MEM004 tickets |
| Search member ID | Librarian search MEM002/MEM003/MEM006 | MEM002, MEM003, MEM006 | Display all corresponding tickets |
| | Member search self | MEM002 search MEM002 | Display borrow history of MEM002 |
| | Member search another | MEM002 search MEM003 | No tickets displayed, display "Not found" |
| | ID does not exist | MEM099 | Display "Not exist" or "Not found" |
| Borrow record ID | ID exists - Borrowed | BR001 | Display corresponding status |
| | ID exists - Returned | BR002 | Display "Returned" message |
| | ID exists - Expired | BR001 (after check overdue) | Display "Expired" message |
| | ID does not exist | BR369 | Display "Not found" |
| Borrow history | Has history | MEM002 has BR001, BR004 | Display borrow history |
| Borrow history | Never borrowed | New member | Empty list |

> 💡 **Technical Tip**: Use **Equivalence Partitioning (EP)** for discrete partitions, **Boundary Value Analysis (BVA)** for numeric partitions (e.g., limit of 3 books). See textbook §6.1–6.3.

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
| TC-16 | Phone number not start with 0 | Log in as Librarian | 1. Go to Members tab<br>2. Click "Add member"<br>3. Fill in information<br>4. Confirm | Username: Stranger, Email: admin@vn.com, Phone number: 9839219743 | REQ-07 | EP |

---

## Summary

| Function Group | Number of TC | REQ Coverage | IDM Technique Applied |
|----------------|-------|---------|----------------------|
| Members | 9 | REQ-07 | EP, BVA |
| Borrow/Return | 6 | REQ-06, REQ-08 | EP |
| **Total** | **15** | REQ-06 → REQ-08 | EP, BVA |
