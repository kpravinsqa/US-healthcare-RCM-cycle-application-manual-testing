# Patient Registration (PAT): Test Cases

10 test cases. Execution results show Cycle 1 → Cycle 2.

## TC_RCM_PAT_001: Register insured patient

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-03 / TS_RCM_PAT_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Fill all demographics<br>2. Payer Cigna, member ID CIG1234567<br>3. Register |
| Expected result | Toast with new MRN; patient searchable by name |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_patient_registration.py::test_register_insured_patient` |

## TC_RCM_PAT_002: DOB in the future

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-03 / TS_RCM_PAT_02 |
| Priority / Type | P1 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter tomorrow's date as DOB<br>2. Register |
| Expected result | 'Date of birth cannot be in the future' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_patient_registration.py::test_registration_field_validation` |

## TC_RCM_PAT_003: DOB more than 120 years ago

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-03 / TS_RCM_PAT_02 |
| Priority / Type | P2 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter 1890-01-01<br>2. Register |
| Expected result | 'Date of birth cannot be more than 120 years ago' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_patient_registration.py::test_registration_field_validation` |

## TC_RCM_PAT_004: Phone 9 / 10 / 11 digits

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-03 / TS_RCM_PAT_02 |
| Priority / Type | P2 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. Register with 9, 10 and 11-digit phone numbers |
| Expected result | Only 10 digits accepted |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_patient_registration.py::test_registration_field_validation` |

## TC_RCM_PAT_005: Names allow apostrophe and hyphen

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-03 / TS_RCM_PAT_02 |
| Priority / Type | P2 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Register O'Brien-Smith |
| Expected result | Accepted and displayed correctly |
| Result (C1 → C2) | Fail → Pass (DEF-RCM-04) |
| Automation | Manual only |

## TC_RCM_PAT_006: ZIP must be 5 digits

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-03 / TS_RCM_PAT_02 |
| Priority / Type | P3 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter 7870 |
| Expected result | 'ZIP code must be 5 digits' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_patient_registration.py::test_registration_field_validation` |

## TC_RCM_PAT_007: Member ID disabled for Self-Pay

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-04 / TS_RCM_PAT_03 |
| Priority / Type | P2 / UI |
| Preconditions | - |
| Test data | - |
| Steps | 1. Select payer Self-Pay |
| Expected result | Member ID disabled and cleared |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_patient_registration.py::test_member_id_disabled_for_self_pay` |

## TC_RCM_PAT_008: Member ID length and characters

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-04 / TS_RCM_PAT_03 |
| Priority / Type | P2 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter AB12<br>2. Enter AET-12345 |
| Expected result | 'Member ID must be 6-15 letters or digits' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_patient_registration.py::test_registration_field_validation` |

## TC_RCM_PAT_009: Same name and DOB, different case

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-05 / TS_RCM_PAT_04 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Register 'emily CARTER' 1985-04-12 (exists as Emily Carter) |
| Expected result | 'Possible duplicate: patient MRN000100 has the same name and date of birth' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_patient_registration.py::test_duplicate_patient_detection` |

## TC_RCM_PAT_010: Search by MRN and partial name

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-05 / TS_RCM_PAT_05 |
| Priority / Type | P2 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Search MRN000101<br>2. Search 'carter' |
| Expected result | Exact MRN returns 1; name search case-insensitive |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_patient_registration.py::test_patient_search` |
