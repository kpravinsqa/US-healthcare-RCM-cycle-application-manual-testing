# Test Summary Report: Healthcare RCM — Manual Testing

**Release:** R5.0 (Provider Dashboard & Claims) · **Prepared by:** Pravin Khedkar, QA Lead · **Recommendation: GO**

## 1. Execution summary

| Metric | Cycle 1 | Cycle 2 (regression) |
|---|---:|---:|
| Planned | 44 | 44 |
| Executed | 43 | 44 |
| Passed | 37 | 43 |
| Failed | 6 | 1 |
| Blocked | 1 | 0 |
| Pass rate | 84.1% | 97.7% |

## 2. Module-wise results

| Module | Cases | C1 Pass | C1 Fail | C1 Blocked | C2 Pass | C2 Pass % |
|---|---|---|---|---|---|---|
| Login & Access Control | 7 | 6 | 1 | 0 | 6 | 86% |
| Patient Registration | 10 | 9 | 1 | 0 | 10 | 100% |
| Provider & NPI | 6 | 4 | 2 | 0 | 6 | 100% |
| Encounters & Coding | 8 | 8 | 0 | 0 | 8 | 100% |
| Provider Dashboard | 4 | 3 | 1 | 0 | 4 | 100% |
| Claims & Payments | 9 | 7 | 1 | 1 | 9 | 100% |

## 3. Defect summary

| Severity | Count |
|---|---:|
| Critical | 0 |
| High | 3 |
| Medium | 3 |
| Low | 1 |
| **Total** | **7** |

Status: Closed: 6, Open: 1.
Defect density: **1.2 defects per module**; defect detection in Cycle 1: **6 failing cases**.

## 4. Automation coverage
40 of 44 test cases (91%) are automated in [playwright-python-healthcare-rcm](https://github.com/kpravinsqa/playwright-python-healthcare-rcm); the rest are manual or exploratory by design.

## 5. Open issues and risks
- **DEF-RCM-06** (Medium/P2, Open): Session does not expire after 15 minutes idle

## 6. Recommendation
Exit criteria met except DEF-RCM-06 (Medium, session timeout), which is accepted by the PO as a known issue for R5.0 with a fix committed for R5.1. QA recommends GO.
