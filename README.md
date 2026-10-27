# Healthcare RCM — Manual Testing

![Type](https://img.shields.io/badge/testing-manual-blue) ![Cases](https://img.shields.io/badge/test%20cases-44-success) ![Defects](https://img.shields.io/badge/defects-7-orange) ![Domain](https://img.shields.io/badge/domain-US%20Healthcare%20RCM-informational)

Complete manual-testing artefact set for **HeartBeats MD (Provider Revenue Cycle Management)** (US Healthcare / Revenue Cycle Management): test plan, scenarios, detailed test cases,
requirement traceability, defect reports and a test summary report, structured the way I deliver them on real projects.

> **Confidentiality note:** this is a portfolio re-creation. Requirements, test data and defects are rewritten in generic
> terms from my project experience; **no confidential client documents, data or screenshots are included.**

**Automation companion:** [playwright-python-healthcare-rcm](https://github.com/kpravinsqa/playwright-python-healthcare-rcm). Test cases marked with an automated test name are implemented there.

## Contents

| Artefact | Link |
|---|---|
| Master test plan | [docs/01_Test_Plan.md](docs/01_Test_Plan.md) |
| Test scenarios (19) | [docs/02_Test_Scenarios.md](docs/02_Test_Scenarios.md) |
| Requirement traceability matrix | [docs/03_RTM.md](docs/03_RTM.md) |
| Test cases by module | [AUTH](test-cases/AUTH_Login_and_Access_Control.md) · [PAT](test-cases/PAT_Patient_Registration.md) · [PRV](test-cases/PRV_Provider_and_NPI.md) · [ENC](test-cases/ENC_Encounters_and_Coding.md) · [DASH](test-cases/DASH_Provider_Dashboard.md) · [CLM](test-cases/CLM_Claims_and_Payments.md) |
| Excel workbook (dashboard, cases, RTM, defects) | [test-cases/RCM_Test_Cases.xlsx](test-cases/RCM_Test_Cases.xlsx) |
| Defect report (7) | [defects/Defect_Report.md](defects/Defect_Report.md) |
| Test summary report | [reports/Test_Summary_Report.md](reports/Test_Summary_Report.md) |
| Checklists | [HIPAA-aware Test Data Checklist](checklists/hipaa_test_data_checklist.md) · [Claim Lifecycle Checklist](checklists/claim_lifecycle_checklist.md) |

## Coverage

| Module | Code | Test cases |
|---|---|---|
| Login & Access Control | AUTH | 7 |
| Patient Registration | PAT | 10 |
| Provider & NPI | PRV | 6 |
| Encounters & Coding | ENC | 8 |
| Provider Dashboard | DASH | 4 |
| Claims & Payments | CLM | 9 |
| **Total** | | **44** |

## Highlights

- 44 test cases across 6 modules and 13 requirements, with full RTM
- Healthcare-specific rules: **NPI Luhn check digit**, ICD-10-CM formats, CPT fee schedule, **timely filing 365/366**
- Persona and RBAC testing (Admin, Front Desk, Provider) at menu, URL and API level
- Real bug patterns: **encounter info missing from provider dashboard**, **NPI boundary-value cluster**
- HIPAA-aware approach: synthetic data only, PHI rules for defects and screenshots

## Test design techniques used

Equivalence partitioning · boundary value analysis · decision tables · state transition · error guessing · exploratory testing

## Author

**Pravin Khedkar**, QA Lead / SDET · [@kpravinsqa](https://github.com/kpravinsqa)
