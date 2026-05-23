# TEST SUMMARY  
## 1.Team Information

| Item | Information |
| :---- | :---- |
| Team | Team 14 |
| Class | ICT-1 |
| Report date | 23/05/2026 |
| System under Test | https://stqa.rbc.vn \- v1.0 |

## 2.Overall Results

| Metric | Value |
| :---- | :---- |
| Total Test Case | 15 |
| Passed | 9 |
| Failed | 2 |
| Inconcusive | 4 |
| Blocked | 0 |
| Not Run | 0 |
| Pass Rate | 60% |
| Total Bugs Found | 2 |

### 2.1)RESULT BY FUNCTIONAL GROUP

| Functional Group | TC | Pass | Fail | Inconclusice | Bug | Evaluation |
| :---- | :---- | :---- | :---- | :---- | :---- |
| Login | 9 | 3 | 2 | 4 | 2 | Need Improvement (language inconsisted) |
| View Book list | 6 | 6 | 0 | 0 | Stable |

### 2.2)BUG BY SEVERITY

| Severity | Count | Bug IDs |
| :---- | :---- | :---- |
| High | 0 |  |
| Medium | 0 |  |
| Low | 2 | BUG-01,BUG-02 |

## 3.TEST DESIGN TECHNIQUE USED

| Technique | Applied to REQ | Number of TCs | Explanation |
| :---- | :---- | :---- | :---- |
| Equivalence  Partitioning | REQ-01 REQ-02 | 15 | Input is divided into valid and invalid classes such as valid/invalid email, correct/incorrect password, User roles and book status conditions |

## 4.SOFTWARE QUALITY ANALYSIS  
### 4.1)STRENGTH   
\-Role-based access(LIBRARIAN/MEMBER) is correctly implemented  
\-Book list displays complete and accurate information  
\-Real-time book status updates function properly

### 4.2)Weakness  
\-Error messages are not consistent localized(English vs Vietnamese mismatch)

## 5.BUG FIX PRIORITY 

| PRIORITY ORDER | BUG | SEVERITY | REASON FOR PRIORITY |
| :---- | :---- | :---- | :---- |
| 1 | BUG-01 | Low | Affect English UI consistency and user-experience |
| 2 | BUG-02 | Low | Affect English UI consistency and user-experience |

## 6.CONCLUSION:  
\=\>System is not fully ready for production release
\=\>Core functionality (login, book list) works correctly

## 8.AI USAGE DECLARATION

| AI tool | Used for | Verification & Edit |
| :---- | :---- | :---- |
| ChatGPT | Check Test Cases |  |
| Gemini | Explaination& Understanding the concept| |
| Claude | Step-by-step guidance & Review | |

