# TEST SUMMARY  

## 1. Team Information

| Item | Information |
| :---- | :---- |
| Team | Team 14 |
| Class | ICT-1 |
| Report Date | 23/05/2026 |
| System under Test | https://stqa.rbc.vn - v1.0 |

---

## 2. Overall Results

| Metric | Value |
| :---- | :---- |
| Total Test Cases | 16 |
| Passed | 10 |
| Failed | 2 |
| Inconclusive | 4 |
| Blocked | 0 |
| Not Run | 0 |
| Pass Rate | 62.5% |
| Total Failures | 1 |
| Requirement Ambiguities | 1 |
| Requirement Gaps | 1 |

---

## 2.1) Results by Functional Group

| Functional Group | TC | Pass | Fail | Inconclusive | Observation | Evaluation |
| :---- | :---: | :---: | :---: | :---: | :---: | :---- |
| Login | 9 | 3 | 2 | 4 | 1 | Need Improvement (language inconsistency) |
| View Book List | 7 | 7 | 0 | 0 | 0 | Stable |

---

## 2.2) Test Observation Severity

| Severity | Count | Report IDs |
| :---- | :---: | :---- |
| High | 0 | N/A |
| Medium | 0 | N/A |
| Low | 1 | OBS-01 |

---

## 3. Test Design Techniques Used

| Technique | Applied to REQ | Number of TCs | Explanation |
| :---- | :---- | :---: | :---- |
| Equivalence Partitioning (EP) | REQ-01, REQ-02 | 16 | Input is divided into valid and invalid classes such as valid/invalid email, correct/incorrect password, user roles, and book status conditions. |


---

## 4. Software Quality Analysis  

### 4.1) Strengths
- Role-based access (LIBRARIAN/MEMBER) is correctly implemented.
- Book list displays complete and accurate information.
- Real-time book status updates function properly.

### 4.2) Weaknesses
- Error messages are not consistently localized (English/Vietnamese mismatch).
- Some requirements in the SRS are ambiguous or incomplete.
- Email format validation behavior is not clearly specified.

---

## 5. Priority of Reported Issues

| Priority Order | Report ID | Type | Severity | Reason |
| :---: | :---- | :---- | :---- | :---- |
| 1 | OBS-01 | Failure | Low | Affects English UI consistency and user experience. |
| 2 | RA-01 | Requirement Ambiguity | Low | SRS does not define behavior for partially empty fields. |
| 3 | RG-01 | Requirement Gap | Low | SRS does not define invalid email format validation. |

---

## 6. Conclusion
- Core functionality (login and book list management) works correctly in normal scenarios.
- Some test cases could not be fully evaluated because the SRS contains ambiguities and missing specifications.
- The system requires clarification of requirements and improvement of localization consistency before production release.

---

## 7. AI Usage Declaration
| AI Tool | Used For | Verification & Edit |
| :---- | :---- | :---- |
| ChatGPT | Reviewing test cases and report structure | Outputs were reviewed and verified manually |
| Gemini | Concept explanation and understanding | Concepts were applied to testing logic |
| Claude | Formatting review and documentation guidance | Final outputs were checked manually |