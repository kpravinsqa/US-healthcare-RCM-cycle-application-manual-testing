# Requirement Traceability Matrix: Healthcare RCM — Manual Testing

Requirement coverage: **13/13 (100%)**

| Req ID | Module | Requirement | Scenarios | Test cases | Automated | Status |
|---|---|---|---|---|---|---|
| REQ-01 | Login & Access Control | Role-based login lands each persona on its home page | TS_RCM_AUTH_01, TS_RCM_AUTH_02 | TC_RCM_AUTH_001, TC_RCM_AUTH_002, TC_RCM_AUTH_003 | 3/3 | Covered |
| REQ-02 | Login & Access Control | Modules are restricted by role in the menu, by direct URL and in the API | TS_RCM_AUTH_03 | TC_RCM_AUTH_004, TC_RCM_AUTH_005, TC_RCM_AUTH_006, TC_RCM_AUTH_007 | 3/4 | Covered, open defect |
| REQ-03 | Patient Registration | Register patients with validated demographics (name, DOB, phone, ZIP, email) | TS_RCM_PAT_01, TS_RCM_PAT_02 | TC_RCM_PAT_001, TC_RCM_PAT_002, TC_RCM_PAT_003, TC_RCM_PAT_004, TC_RCM_PAT_005, TC_RCM_PAT_006 | 5/6 | Covered |
| REQ-04 | Patient Registration | Insurance capture: payer required; member ID 6-15 alphanumerics unless Self-Pay | TS_RCM_PAT_03 | TC_RCM_PAT_007, TC_RCM_PAT_008 | 2/2 | Covered |
| REQ-05 | Patient Registration | Duplicate detection on name + date of birth; MRN auto-generated | TS_RCM_PAT_04, TS_RCM_PAT_05 | TC_RCM_PAT_009, TC_RCM_PAT_010 | 2/2 | Covered |
| REQ-06 | Provider & NPI | NPI must be 10 digits and pass the CMS Luhn check digit | TS_RCM_PRV_01, TS_RCM_PRV_02 | TC_RCM_PRV_001, TC_RCM_PRV_002, TC_RCM_PRV_003, TC_RCM_PRV_004, TC_RCM_PRV_005 | 5/5 | Covered |
| REQ-07 | Provider & NPI | NPI is unique across providers | TS_RCM_PRV_02 | TC_RCM_PRV_006 | 1/1 | Covered |
| REQ-08 | Encounters & Coding | Encounter requires patient, provider, valid DOS, at least one ICD-10 and one CPT line | TS_RCM_ENC_02, TS_RCM_ENC_03 | TC_RCM_ENC_004, TC_RCM_ENC_005, TC_RCM_ENC_006, TC_RCM_ENC_007, TC_RCM_ENC_008 | 5/5 | Covered |
| REQ-09 | Encounters & Coding | Charges are calculated from the fee schedule x units | TS_RCM_ENC_01 | TC_RCM_ENC_001, TC_RCM_ENC_002, TC_RCM_ENC_003 | 3/3 | Covered |
| REQ-10 | Provider Dashboard | Providers see their own encounters with dx, CPT, charge and status; KPIs reconcile | TS_RCM_DASH_01, TS_RCM_DASH_02 | TC_RCM_DASH_001, TC_RCM_DASH_002, TC_RCM_DASH_003, TC_RCM_DASH_004 | 3/4 | Covered |
| REQ-11 | Claims & Payments | Create a claim from an open encounter; one claim per encounter | TS_RCM_CLM_01, TS_RCM_CLM_04 | TC_RCM_CLM_001, TC_RCM_CLM_002, TC_RCM_CLM_009 | 2/3 | Covered |
| REQ-12 | Claims & Payments | Claim scrubber rejects self-pay and claims older than 365 days from DOS | TS_RCM_CLM_02 | TC_RCM_CLM_003, TC_RCM_CLM_004 | 2/2 | Covered |
| REQ-13 | Claims & Payments | Payment posting: paid + adjustment cannot exceed balance; status PAID / PARTIALLY_PAID | TS_RCM_CLM_03 | TC_RCM_CLM_005, TC_RCM_CLM_006, TC_RCM_CLM_007, TC_RCM_CLM_008 | 4/4 | Covered |
