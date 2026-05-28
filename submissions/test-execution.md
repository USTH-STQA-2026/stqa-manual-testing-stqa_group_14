# Test Execution — Test Execution Results

> **Instructions**: Run each TC on the system https://stqa.rbc.vn, record actual results.
> Conclusion: **Pass** (correct result), **Fail** (incorrect result → create bug report), **Blocked** (cannot execute due to other blocking issue), **Not Run** (not yet run).

| Information | |
|---|---|
| **Group** | STQA-14 |
| **Execution Date** | 24/05/2026 |
| **Browser** | Chrome |
| **Operating System** | Windows 10 |

---

## Detailed Results

| Test Case ID | Function Group | Expected Result (Summary) | Actual Result | Conclusion | Evidence | Bug |
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
|-------|---------------|---------------------------|-----------------|---------|-----------|----|
| TC-01 | Members | Create valid member | System rejected, displays "Email invalid" | Fail | | BUG-07 |
| TC-02 | Members | Reject email missing "." | System rejected, displays "Email invalid" | PASS | | |
| TC-03 | Members | Reject email missing "@" | Created Successfully | Fail | | BUG-07 |
| TC-04 | Members | Reject duplicate email | System rejected (email exists) | Pass | | |
| TC-05 | Members | Member does not see "Add member" tab | Tab not displayed / not accessible | Pass | | |
| TC-06 | Members | Create member with a@b.co successfully | System rejected (email invalid) | Fail | | BUG-07 |
| TC-07 | Borrow/Return | Display BR001–BR005 (Librarian) | Display all tickets | Pass | | |
| TC-08 | Borrow/Return | Member sees only BR001 & BR004 | Only see BR001 & BR004 | Pass | | |
| TC-09 | Borrow/Return | Member cannot view other ticket | MEM003 tickets displayed | Fail | | BUG-08 |
| TC-10 | Borrow/Return | View BR001 details completely | Display all information | Pass | | |
| TC-11 | Borrow/Return | BR002 displays "Returned" | Displays "Returned" | Pass | | |
| TC-12 | Borrow/Return | Check Overdue marks BR001 | BR001 changes to "Overdue" if expired | Pass | | |
| TC-13 | Borrow/Return | BR002 still "Returned" after check | BR002 still displays "Returned" | Pass | | |
| TC-14 | Members | Reject email with multiple @ or .. | System rejected (email invalid) | Pass | | |
| TC-15 | Members | Reject blank username | System rejected (Username blank) | Pass | | |

---

## Summary of Results

| Metric | Value |
|--------|--------|
| Total test cases | 15 |
| Pass | 11 |
| Fail | 4 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass Rate** | 73.3% |

### Results by Function Group

| Function Group | Total TC | Pass | Fail | Pass Rate |
|------|---------|------|------|------------|
|------|---------|------|------|------------|
| Members | 8 | 5 | 3 | 62.5% |
| Borrow/Return | 7 | 6 | 1 | 85.7% |
