# Encounters & Coding (ENC): Test Cases

8 test cases. Execution results show Cycle 1 → Cycle 2.

## TC_RCM_ENC_001: Multi-line encounter total

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-09 / TS_RCM_ENC_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Add 99214 x1, 93000 x1, 36415 x2 |
| Expected result | Total $244.00 (175 + 45 + 24) |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_encounters_dashboard.py::test_create_encounter_with_multiple_lines` |

## TC_RCM_ENC_002: Units change recalculates total

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-09 / TS_RCM_ENC_01 |
| Priority / Type | P2 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Select 99213 x1<br>2. Change units to 3 |
| Expected result | Total updates $120.00 → $360.00 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_encounters_dashboard.py::test_total_charge_recalculates_live` |

## TC_RCM_ENC_003: Units 0 and 100 rejected

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-09 / TS_RCM_ENC_01 |
| Priority / Type | P2 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. Save with units 0<br>2. Save with units 100 |
| Expected result | 'Units must be between 1 and 99' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/api/test_rcm_api.py::test_encounter_line_validation` |

## TC_RCM_ENC_004: DOS in the future

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-08 / TS_RCM_ENC_02 |
| Priority / Type | P1 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Set DOS tomorrow<br>2. Save |
| Expected result | 'Date of service cannot be in the future' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_encounters_dashboard.py::test_date_of_service_rules` |

## TC_RCM_ENC_005: DOS before patient DOB

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-08 / TS_RCM_ENC_02 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. DOS 1980-01-01 for patient born 1985 |
| Expected result | 'Date of service cannot be before the patient's date of birth' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_encounters_dashboard.py::test_date_of_service_rules` |

## TC_RCM_ENC_006: Valid ICD-10 formats incl. 7-character and lowercase

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-08 / TS_RCM_ENC_03 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter I10, E11.9, S72.001A, j06.9 |
| Expected result | All accepted; lowercase normalised |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_encounters_dashboard.py::test_icd10_format_validation` |

## TC_RCM_ENC_007: Invalid ICD-10 format

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-08 / TS_RCM_ENC_03 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter 12345<br>2. Enter E11.12345 |
| Expected result | '… is not a valid ICD-10-CM code' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_encounters_dashboard.py::test_icd10_format_validation` |

## TC_RCM_ENC_008: Diagnosis and procedure mandatory

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-08 / TS_RCM_ENC_02 |
| Priority / Type | P1 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Save with no dx<br>2. Add dx and save with no CPT |
| Expected result | Both errors shown in order |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_encounters_dashboard.py::test_encounter_requires_diagnosis_and_procedure` |
