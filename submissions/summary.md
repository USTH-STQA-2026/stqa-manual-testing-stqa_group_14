# Test Summary — Testing Summary Report

> **Instructions**: This is a **Quality Assurance** activity — you evaluate the overall quality of the software, not just list bugs.

---

## 1. Group Information

| Item | Information |
|-----|----------|
| **Group** | STQA-14 |
| **Class** | `<!-- Ex: SE001.P11 -->` |
| **Report Date** | `<!-- DD/MM/YYYY -->` |
| **System Under Test** | https://stqa.rbc.vn — v1.0 |

---

## 2. Overall Result Summary

| Metric | Value |
|--------|--------|
| Total test cases | 15 |
| Pass | 11 |
| Fail | 4 |
| Blocked | 0 |
| Not Run | 0 |
| **Pass Rate** | 73.3% |
| **Bugs Found** | 2 |

### Distribution by Function Group

| Function Group | TC | Pass | Fail | Bug | Assessment |
|---------------|-----|------|------|-----|----------|
| Members | 8 | 5 | 3 | BUG-07 | Need fix: email validation causing false rejection |
| Borrow/Return | 7 | 6 | 1 | BUG-08 | Need fix: access control/search filtering by member |

### Bug Distribution by Severity

| Severity | Count | Bug IDs |
|--------|---------|---------|
| High | 2 | BUG-07, BUG-08 |
| Medium | 0 | |
| Low | 0 | |

---

## 3. Design Techniques Used

| Technique | Applied to Which REQs? | Number of TCs | How It Was Applied |
|----------|---------------------|---------------|------------------------|
| EP (Equivalence Partitioning) | REQ-07, REQ-08 | 12 | Group discrete data (valid/invalid emails, roles) |
| BVA (Boundary Value Analysis) | REQ-07 | 3 | Applied for email length/format validation and phone number |

---

## 4. Software Quality Analysis

### 4.1. Strengths
`- Core workflows mostly functional: adding members and borrow/return flows operate correctly for the majority of cases.`

`- IDM analysis applied: tests cover valid/invalid partitions and boundary values for member inputs.`

### 4.2. Weaknesses
`- Two high-severity issues found:`
`  - BUG-07: Email validation currently rejects a valid email during member creation (blocks registrations) and accept invalid email into database.`
`  - BUG-08: Members can view other members' borrow tickets (data privacy / access control breach).`

---

## 5. Bug Fix Priority Recommendation

> 💡 This is the **Quality Assurance** section: you not only find bugs but also **recommend fix priorities** and assess impact.
> Clearly state priority criteria: based on **severity** (technical severity) and/or **priority** (business priority).

| Order | Bug | Severity | Reason for Priority |
|--------|-----|--------|---------------|
| 1 | BUG-08 | High | Data privacy breach — immediate security/privacy risk |
| 2 | BUG-07 | High | Blocks core functionality (member registration) — business impact |

**Short-term Fix Suggestions:**
- BUG-08: Enforce access control checks at server/data layer, add unit/integration tests for search API.
- BUG-07: Review/adjust email regex/validator in backend, add test cases for edge-case and international emails.

---

## 6. Conclusion

The system is **not ready for release**. Two critical issues (privacy + registration) must be fixed and retested before release.

---

## 7. Lessons Learned (Optional)

`- Thiết kế IDM trước khi viết TC giúp phát hiện các kịch bản biên và trường hợp xấu.
`- Cần bổ sung test tự động (unit & integration) cho validation và phân quyền truy xuất dữ liệu.

---

## 8. AI Tool Usage Declaration (Optional)

> If the group used AI tools (ChatGPT, Copilot, Gemini...), please document below. Honest disclosure **does not affect your score** — this is a professional transparency skill.

| AI Tool | Used For Which Section | How You Verified/Edited It |
|------------|-------------------|------------------------------|
| | | |
| AI Tool | Used For Which Section | How You Verified/Edited It |
|------------|-------------------|------------------------------|
| GitHub Copilot | Bug fixes, documentation spelling corrections | Manually reviewed and edited before saving |
| Claude AI | Test case suggestions | Asked for suggestions on missing test scenarios |