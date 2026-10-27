# Test Plan: Healthcare RCM — Manual Testing

| Item | Detail |
|---|---|
| Project | HeartBeats MD (Provider Revenue Cycle Management) |
| Domain | US Healthcare / Revenue Cycle Management |
| Document | Master Test Plan (IEEE 829 aligned) |
| Prepared by | Pravin Khedkar, QA Lead |
| Version | 1.2 |

> Portfolio re-creation. Requirements, data and defects are rewritten in generic terms; no confidential client
> information is included.

## 1. Introduction
The application supports a US cardiology and family-medicine practice through the revenue cycle: patient registration and insurance capture, provider onboarding (NPI), encounter documentation with CPT/ICD-10 codes, the provider dashboard, claim creation and scrubbing, submission and payment posting. This release added the provider dashboard and the claim scrubber. Testing was done with synthetic, PHI-free data under HIPAA-aware practices.

## 2. Objectives
- Verify demographic, insurance and NPI validation rules prevent bad data entering the revenue cycle
- Verify encounter charges are calculated from the fee schedule and appear on the provider dashboard
- Verify claim scrubbing (self-pay, timely filing) and payment posting balances are correct
- Verify role-based access control for Admin, Front Desk and Provider personas

## 3. Scope
### 3.1 In scope
- **Login & Access Control** (AUTH): 7 test cases
- **Patient Registration** (PAT): 10 test cases
- **Provider & NPI** (PRV): 6 test cases
- **Encounters & Coding** (ENC): 8 test cases
- **Provider Dashboard** (DASH): 4 test cases
- **Claims & Payments** (CLM): 9 test cases


### 3.2 Out of scope
- EDI 837/835 clearing-house connectivity (vendor certified)
- EHR clinical notes module
- Patient portal and online payments
- Performance and penetration testing (separate engagements)

## 4. Test approach
- Persona-based testing: Front Desk, Provider and Billing Admin journeys end to end
- Healthcare code validation with reference values: NPI Luhn check (80840 prefix), ICD-10-CM format, CPT fee schedule
- Synthetic data only; PHI handling rules followed (no real patient data in screenshots or defects)
- API verification of business rules before UI testing; automated smoke and regression in Playwright

**Test design techniques:** equivalence partitioning, boundary value analysis, decision tables, state transition,
error guessing, and exploratory charters for high-risk areas.

**Test types:** Boundary, Functional, Negative, Security, UI.

## 5. Test environment
| Environment | Purpose | Details |
|---|---|---|
| QA | Functional and regression | https://qa.rcm.example (synthetic patients) |
| UAT | Billing team acceptance | Masked production-like configuration |
| Browsers | Compatibility | Chrome, Edge (practice standard) |

**Tools:** JIRA / Zephyr, Postman, SQL Server Management Studio, Python + Playwright, Excel

## 6. Entry criteria
- Build deployed to QA with release notes
- Smoke suite passed
- Test data loaded and verified
- Requirements signed off and test cases peer-reviewed

## 7. Exit criteria
- 100% of P1 and 95% of all planned test cases executed
- No open Critical / High defects
- All Medium defects triaged with an agreed fix version
- Regression suite green, Test Summary Report signed off

## 8. Suspension and resumption
- Suspend when the smoke suite fails, the environment is unavailable for more than 4 hours, or a Critical defect blocks more than 30% of cases.
- Resume after the fix is deployed and the smoke suite passes again.

## 9. Defect management
Defects are logged in JIRA with severity (Critical / High / Medium / Low) and priority (P1 to P4), triaged daily with
Dev and PO, and retested and regression-tested before closure. See [Defect Report](../defects/Defect_Report.md).

## 10. Risks and mitigation
| Risk | Impact | Mitigation |
|---|---|---|
| Invalid NPI or member ID reaching claims | Claim denials, delayed revenue | Strict BVA on NPI/member ID; API-level negative tests |
| Encounters missing from provider dashboard | Providers cannot review or sign; revenue leakage | Dedicated dashboard reconciliation scenarios |
| Timely-filing rule mis-implemented | Lost revenue for late claims | Day 365 vs 366 boundary cases |
| Use of real PHI in testing | HIPAA breach | Synthetic data factory; screenshot review before sharing |

## 11. Deliverables
- Test plan (this document), [Test Scenarios](02_Test_Scenarios.md), [Test Cases](../test-cases/), [RTM](03_RTM.md)
- [Defect Report](../defects/Defect_Report.md), [Test Summary Report](../reports/Test_Summary_Report.md)
- Excel workbook: [`test-cases/RCM_Test_Cases.xlsx`](../test-cases/RCM_Test_Cases.xlsx)

## 12. Roles and responsibilities
| Role | Responsibility |
|---|---|
| QA Lead | Test strategy, planning, estimation, reporting, sign-off |
| QA Engineer | Test design, execution, defect logging, regression |
| Automation (SDET) | Smoke and regression automation, CI integration |
| Developer | Defect fixes, unit tests, root-cause analysis |
| Product Owner | Requirement clarification, UAT acceptance |

## 13. Schedule
| Phase | Duration |
|---|---|
| Requirement analysis and test planning | 1 week |
| Test design and review | 1.5 weeks |
| Cycle 1: functional execution | 2 weeks |
| Defect fixing and Cycle 2: regression | 1 week |
| UAT support and sign-off | 0.5 week |
