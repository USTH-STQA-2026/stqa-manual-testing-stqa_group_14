# Test Observation Report

| Attribute | Details |
|-----------|---------|
| **Report ID** | OBS-01 |
| **Related TC** | TC-03 ,TC-04|
| **Related REQ** | REQ-01 |
| **Type** | Failure |
| **Severity** | Low |
| **Reported By** | La Thi Bao Tram |
| **Date Reported** | 25/05/2026 |
| **Status** | Open |

## Title
- TC-03: Error message is displayed in Vietnamese instead of English when logging in with a non-existing email
- TC-04: Error message is displayed in Vietnamese instead of English when logging in with incorrect password
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
- TC-03:System displays the Vietnamese message: 'Không tìm thấy thành viên'
- TC-04:System displays the Vietnamese message: 'Mật khẩu không đúng'

## Impact
English users may not understand the displayed error message, causing inconsistent user experience.

## Severity explanation:
The issue does not prevent users from logging in or accessing system functions.
However, it affects usability and language consistency when the application is used in English mode.
=>Therefore, the severity is classified as Low
## Priority
- P2

## Evidence

<p><strong>TC-03 Screenshot</strong></p>
<a href="Images/REQ-01-02/TC-03.png" target="_blank">
    <img src="Images/REQ-01-02/TC-03.png" alt="TC-03 Screenshot" width="700">
</a>

<br><br>

<p><strong>TC-04 Screenshot</strong></p>
<a href="Images/REQ-01-02/TC-04.png" target="_blank">
    <img src="Images/REQ-01-02/TC-04.png" alt="TC-04 Screenshot" width="700">
</a>

## Suggested Fix
- Check localization configuration for error message keys
- Ensure “member not found” error uses English resource bundle when language = EN
- Verify fallback language logic is not defaulting to Vietnamese incorrectly

# OBSERVATION-02
| Attribute | Details |
|-----------|---------|
| **Report ID** | OBS-02 |
| **Related TC** | TC-06 ,TC-07|
| **Related REQ** | REQ-01 |
| **Type** | Requirement Ambiguity |
| **Severity** | Low |
| **Reported By** | La Thi Bao Tram |
| **Date Reported** | 25/05/2026 |
| **Status** | Open |
## Title
The SRS specifies behavior only when both email and password fields are empty.
However, the SRS does not define expected behavior for:
- empty email only
- empty password only

Therefore, expected results cannot be determined confidently.

## Environment
- Browser: Chrome Version 148
- Operating System: Windows 10
- Application: Library Management System
- UI Language: English

## Preconditions:
- Application is running
- User is on the login screen

## Steps to reproduce:

- TC-06
1.Open the login page
2.Leave the email field empty
3.Enter password: 'password123'
4.Click the Login button

- TC-07:
1.Open the login page
2.Enter email: 'ba.nguyen@email.com'
3.Leave the password field empty
4.Click the Login button

## Expected Result
- The SRS does not specify the expected behavior when only one field is empty.
=>Therefore, the expected result cannot be determined


## Actual Result
- TC-06: System displays the message "Please enter your email and password"
- TC-07: System displays the message "Please enter your email and password"

## Testing Impact
- Test verdict is marked as: Inconclusive. Because the specification is too vague to determine a Pass or Fail result.
## Severity explanation:
The ambiguity does not prevent the system from functioning. However, it affects the ability to evaluate test results consistently and may lead to misunderstandings during development and testing.
=>Therefore, the severity is classified as Low.
## Priority:
- P3
## Evidence

<p><strong>TC-06 Screenshot</strong></p>
<a href="Images/REQ-01-02/TC-06.png" target="_blank">
    <img src="Images/REQ-01-02/TC-06.png" alt="TC-06 Screenshot" width="700">
</a>

<br><br>

<p><strong>TC-07 Screenshot</strong></p>
<a href="Images/REQ-01-02/TC-07.png" target="_blank">
    <img src="Images/REQ-01-02/TC-07.png" alt="TC-07 Screenshot" width="700">
</a>

## Suggested Fix
- Expected validation message when email is empty
- Expected validation message when password is empty

# OBSERVATION-03
| Attribute | Details |
|-----------|---------|
| **Report ID** | OBS-03 |
| **Related TC** | TC-08 ,TC-09|
| **Related REQ** | REQ-01 |
| **Type** | Requirement Gap |
| **Severity** | Low |
| **Reported By** | La Thi Bao Tram |
| **Date Reported** | 25/05/2026 |
| **Status** | Open |

## Title
The SRS describes login functionality but does not specify behavior for invalid email format validation.
Missing specifications include:
- email without @
- email without . in domain

## Environment
- Browser: Chrome Version 148
- Operating System: Windows 10
- Application: Library Management System
- UI Language: English
## Preconditions:
- Application is running
- User is on the login screen

## Steps to reproduce:
### TC-08
1. Open the login page
2. Enter email: user@gmail
3. Enter password: password123
4. Click Login

### TC-09
1. Open the login page
2. Enter email: abc.com
3. Enter password: password123
4. Click Login

## Expected Result
The SRS does not specify the expected behavior for invalid email formats
=>Therefore, the expected result cannot be determined

## Actual Result
- TC-08: System displays the message "Member not found"
- TC-09: System displays the message "Member not found"


## Testing Impact
The test verdict is marked as Inconclusive because the SRS does not define the expected behavior for invalid email formats.

## Risk
- Different developers may implement inconsistent validation behavior.

## Severity explanation:
The issue does not affect system operation directly. However, it prevents objective verification of login validation behavior and may lead to inconsistent implementations.
=>Therefore, the severity is classified as Low
## Priority:
- P3
## Evidence:

<p><strong>TC-08 Screenshot</strong></p>
<a href="Images/REQ-01-02/TC-08.png" target="_blank">
    <img src="Images/REQ-01-02/TC-08.png" alt="TC-08 Screenshot" width="700">
</a>

<br><br>

<p><strong>TC-09 Screenshot</strong></p>
<a href="Images/REQ-01-02/TC-09.png" target="_blank">
    <img src="Images/REQ-01-02/TC-09.png" alt="TC-09 Screenshot" width="700">
</a>

## Suggested Fix
- Specify whether email format validation is required
- Define expected validation messages for invalid email formats
- Clarify whether format validation should occur before account lookup






