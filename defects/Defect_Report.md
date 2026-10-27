# Defect Report: Healthcare RCM — Manual Testing

Defects are re-created from real bug patterns found on the project, rewritten without client details.

| ID | Title | Module | Severity | Priority | Status |
|---|---|---|---|---|---|
| DEF-RCM-01 | Encounter information missing from provider dashboard after save | Provider Dashboard | High | P1 | Closed |
| DEF-RCM-02 | NPI field accepts 11 digits (boundary not enforced) | Provider & NPI | Medium | P2 | Closed |
| DEF-RCM-03 | NPI check digit not validated: invalid NPIs accepted | Provider & NPI | High | P1 | Closed |
| DEF-RCM-04 | Patient last name with apostrophe rejected | Patient Registration | Medium | P2 | Closed |
| DEF-RCM-05 | Claim with DOS exactly 365 days old rejected for timely filing | Claims & Payments | High | P1 | Closed |
| DEF-RCM-06 | Session does not expire after 15 minutes idle | Login & Access Control | Medium | P2 | Open |
| DEF-RCM-07 | CPT dropdown not sorted numerically | Encounters & Coding | Low | P3 | Closed |

## DEF-RCM-01: Encounter information missing from provider dashboard after save

| Field | Value |
|---|---|
| Module | Provider Dashboard |
| Severity / Priority | High / P1 |
| Status | Closed |
| Environment | https://qa.rcm.example (synthetic patients) |
| Linked test case(s) | TC_RCM_DASH_001 |
| Steps to reproduce | 1. Create encounter for Dr. Smith with dx R07.9 and CPT 99214 + 93000<br>2. Log in as dr_smith<br>3. Open dashboard |
| Expected result | Encounter row shows patient, dx, CPT and charge; KPIs include it |
| Actual result | Row shown with blank diagnosis and CPT columns; total charges KPI excluded the encounter |
| Root cause / notes | Dashboard query joined on encounter lines before commit; fixed by reading after transaction commit |

## DEF-RCM-02: NPI field accepts 11 digits (boundary not enforced)

| Field | Value |
|---|---|
| Module | Provider & NPI |
| Severity / Priority | Medium / P2 |
| Status | Closed |
| Environment | https://qa.rcm.example (synthetic patients) |
| Linked test case(s) | TC_RCM_PRV_002 |
| Steps to reproduce | 1. Enter NPI 12345678931<br>2. Add provider |
| Expected result | 'NPI must be exactly 10 digits' |
| Actual result | Provider saved; 11th digit silently truncated |
| Root cause / notes | maxlength used instead of server-side length validation |

## DEF-RCM-03: NPI check digit not validated: invalid NPIs accepted

| Field | Value |
|---|---|
| Module | Provider & NPI |
| Severity / Priority | High / P1 |
| Status | Closed |
| Environment | https://qa.rcm.example (synthetic patients) |
| Linked test case(s) | TC_RCM_PRV_003 |
| Steps to reproduce | 1. Enter NPI 1234567890<br>2. Add provider |
| Expected result | 'NPI check digit is invalid' |
| Actual result | Provider saved; claims later denied by payer |
| Root cause / notes | Luhn check omitted the 80840 prefix |

## DEF-RCM-04: Patient last name with apostrophe rejected

| Field | Value |
|---|---|
| Module | Patient Registration |
| Severity / Priority | Medium / P2 |
| Status | Closed |
| Environment | https://qa.rcm.example (synthetic patients) |
| Linked test case(s) | TC_RCM_PAT_005 |
| Steps to reproduce | 1. Register last name O'Brien-Smith |
| Expected result | Accepted |
| Actual result | 'Last name may contain letters only' |
| Root cause / notes | Regex did not allow ' and - |

## DEF-RCM-05: Claim with DOS exactly 365 days old rejected for timely filing

| Field | Value |
|---|---|
| Module | Claims & Payments |
| Severity / Priority | High / P1 |
| Status | Closed |
| Environment | https://qa.rcm.example (synthetic patients) |
| Linked test case(s) | TC_RCM_CLM_004 |
| Steps to reproduce | 1. Create encounter with DOS today-365<br>2. Create and submit claim |
| Expected result | Claim SUBMITTED (limit is inclusive) |
| Actual result | REJECTED 'Timely filing limit exceeded' |
| Root cause / notes | Off-by-one: >= used instead of > |

## DEF-RCM-06: Session does not expire after 15 minutes idle

| Field | Value |
|---|---|
| Module | Login & Access Control |
| Severity / Priority | Medium / P2 |
| Status | Open |
| Environment | https://qa.rcm.example (synthetic patients) |
| Linked test case(s) | TC_RCM_AUTH_007 |
| Steps to reproduce | 1. Log in<br>2. Stay idle 16 minutes<br>3. Click Claims |
| Expected result | Redirect to login with session-expired message |
| Actual result | Page loads normally; session still valid |
| Root cause / notes | Token TTL configured as 8 hours in QA; fix scheduled for R5.1 |

## DEF-RCM-07: CPT dropdown not sorted numerically

| Field | Value |
|---|---|
| Module | Encounters & Coding |
| Severity / Priority | Low / P3 |
| Status | Closed |
| Environment | https://qa.rcm.example (synthetic patients) |
| Linked test case(s) | - |
| Steps to reproduce | 1. Open New encounter<br>2. Expand CPT dropdown |
| Expected result | CPT codes in ascending order |
| Actual result | Displayed in insertion order |
| Root cause / notes | UI sort added |
