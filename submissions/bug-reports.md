# BUG-01

| Attribute | Details |
|-----------|---------|
| **Bug ID** | BUG-01 |
| **Related TC** | TC-03 ,TC-04|
| **Related REQ** | REQ-01 |
| **Severity** | Low |
| **Reported By** | La Thi Bao Tram |
| **Date Reported** | 25/05/2026 |
| **Status** | Open |

## Title
- TC-03:Error message is displayed in Vietnamese instead of English when logging in with a non-existing email
- TC-04:Error message is displayed in Vietnamese instead of English when logging in with incorrect password
## Environment
- Browser: Chrome Version 148
- Operating System: Windows 10
- Application: Library Management System
- UI Language: English

## Preconditions
- Application is running
- System language is set to English
- User is on the login screen

## Steps to Reproduce
- TC-03:
1. Open the login page
2. Enter email: 'khongtontai@gmail.com'
3. Enter password: 'password123'
4. Click the **Login** button
- TC-04:
1. Open the login page
2. Enter email: 'ba.nguyen@email.com'
3. Enter password: 'wrongpassword123'
4. Click the **Login** button

## Expected Result
- TC03:System displays the error message:
'Member not found'(English Message)
- TC04:System displays the error message:
'Incorrect password'(English Message)

## Actual Result
- TC-03:System displays the Vietnamese message:
'Không tìm thấy thành viên'
- TC-04:System displays the Vietnamese message:
'Mật khẩu không đúng'

## Impact
English users may not understand the displayed error message, causing inconsistent user experience.

## Priority
- P2
## Severity
- Low
 
## Evidence
<a href="Images/TC-03.png" target="_blank">
Click here to view Screenshot of TC-03
</a>
<br>
<a href="Images/TC-04.png" target="_blank">
Click here to view Screenshot of TC-04
</a> 



## Suggested Fix
- Check localization configuration for error message keys
- Ensure “member not found” error uses English resource bundle when language = EN
- Verify fallback language logic is not defaulting to Vietnamese incorrectly








