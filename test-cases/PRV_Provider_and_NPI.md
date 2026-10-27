# Provider & NPI (PRV): Test Cases

6 test cases. Execution results show Cycle 1 → Cycle 2.

## TC_RCM_PRV_001: Valid NPI passes check digit

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-06 / TS_RCM_PRV_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter 1234567893<br>2. Tab out |
| Expected result | '✔ Valid NPI' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_providers_npi.py::test_npi_inline_validation_boundaries` |

## TC_RCM_PRV_002: NPI 9 and 11 digits (BVA)

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-06 / TS_RCM_PRV_01 |
| Priority / Type | P1 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter 123456789<br>2. Enter 12345678931 |
| Expected result | 'NPI must be exactly 10 digits' |
| Result (C1 → C2) | Fail → Pass (DEF-RCM-02) |
| Automation | `tests/ui/test_providers_npi.py::test_npi_inline_validation_boundaries` |

## TC_RCM_PRV_003: NPI with invalid check digit

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-06 / TS_RCM_PRV_01 |
| Priority / Type | P1 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter 1234567890 |
| Expected result | 'NPI check digit is invalid' |
| Result (C1 → C2) | Fail → Pass (DEF-RCM-03) |
| Automation | `tests/ui/test_providers_npi.py::test_npi_inline_validation_boundaries` |

## TC_RCM_PRV_004: NPI with letters

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-06 / TS_RCM_PRV_01 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter 12345ABCDE |
| Expected result | 'NPI must contain digits only' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_providers_npi.py::test_npi_inline_validation_boundaries` |

## TC_RCM_PRV_005: Add provider with valid NPI

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-06 / TS_RCM_PRV_02 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Enter Anita Desai, NPI 1456789019, Pediatrics<br>2. Add |
| Expected result | Provider listed with specialty |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_providers_npi.py::test_add_provider_with_valid_npi` |

## TC_RCM_PRV_006: Duplicate NPI rejected

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-07 / TS_RCM_PRV_02 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Add provider with NPI 1234567893 (exists) |
| Expected result | 'A provider with this NPI already exists' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_providers_npi.py::test_duplicate_npi_rejected` |
