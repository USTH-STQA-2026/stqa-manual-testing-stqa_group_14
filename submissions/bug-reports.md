# BUG-01

| Attribute | Details |
|-----------|---------|
| **Bug ID** | BUG-01 |
| **Related TC** | TC-03 |
| **Related REQ** | REQ-01 |
| **Severity** | Low |
| **Reported By** | Testing Team |
| **Date Reported** | 23/05/2026 |
| **Status** | Open |

## Title
Error message is displayed in Vietnamese instead of English when logging in with a non-existing email

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
1. Open the login page
2. Enter email: 'khongtontai@gmail.com'
3. Enter password: 'password123'
4. Click the **Login** button

## Expected Result
System displays the error message:
'Member not found'(English Message)

## Actual Result
System displays the Vietnamese message:
'Không tìm thấy thành viên'

## Impact
English users may not understand the displayed error message, causing inconsistent user experience.

## Priority
- P2
## Severity
- Low
 
## Evidence
<a href="Images/TC-03.png" target="_blank">
Click here to view Screenshot
</a>

## Suggested Fix
- Check localization configuration for error message keys
- Ensure “member not found” error uses English resource bundle when language = EN
- Verify fallback language logic is not defaulting to Vietnamese incorrectly

# BUG-02

| Attribute | Details |
|-----------|---------|
| **Bug ID** | BUG-02 |
| **Related TC** | TC-04 |
| **Related REQ** | REQ-01 |
| **Severity** | Low |
| **Reported By** | Testing Team |
| **Date Reported** | 23/05/2026 |
| **Status** | Open |

## Title
Error message is displayed in Vietnamese instead of English when logging in with incorrect password

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
1. Open the login page
2. Enter email: 'ba.nguyen@email.com'
3. Enter password: 'wrongpassword123'
4. Click the **Login** button

## Expected Result
System displays the error message:
'Incorrect password'(English Message)

## Actual Result
System displays the Vietnamese message:
'Mật khẩu không đúng'

## Impact
English users may not understand the displayed error message, causing inconsistent user experience.

## Priority
- P2
## Severity
- Low
 
## Evidence
<a href="Images/TC-04.png" target="_blank">
Click here to view Screenshot
</a>
## Suggested Fix
- Check localization configuration for error message keys
- Ensure “Incorrect password” error uses English resource bundle when language = EN
- Verify fallback language logic is not defaulting to Vietnamese incorrectly




