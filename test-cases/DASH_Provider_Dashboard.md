# Provider Dashboard (DASH): Test Cases

4 test cases. Execution results show Cycle 1 → Cycle 2.

## TC_RCM_DASH_001: New encounter visible with full details

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-10 / TS_RCM_DASH_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Create encounter for Dr. Smith (R07.9<br>2. 99214, 93000)<br>3. Log in as dr_smith |
| Expected result | Row shows patient, dx R07.9, CPT '99214, 93000', charge $220.00; KPIs updated |
| Result (C1 → C2) | Fail → Pass (DEF-RCM-01) |
| Automation | `tests/ui/test_encounters_dashboard.py::test_new_encounter_appears_on_provider_dashboard` |

## TC_RCM_DASH_002: Provider sees only own encounters

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-10 / TS_RCM_DASH_01 |
| Priority / Type | P1 / Security |
| Preconditions | - |
| Test data | - |
| Steps | 1. Create encounter for Dr. Rao<br>2. Log in as dr_smith |
| Expected result | Empty state; KPI encounters = 0 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_encounters_dashboard.py::test_provider_sees_only_own_encounters` |

## TC_RCM_DASH_003: KPI reconciliation open vs billed

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-10 / TS_RCM_DASH_02 |
| Priority / Type | P2 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Create 2 encounters<br>2. Bill one |
| Expected result | Encounters 2, Open 1, Billed 1, charges = sum |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/api/test_rcm_api.py::test_dashboard_summary_matches_encounters` |

## TC_RCM_DASH_004: Units shown on CPT column

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-10 / TS_RCM_DASH_01 |
| Priority / Type | P3 / UI |
| Preconditions | - |
| Test data | - |
| Steps | 1. Create encounter with 36415 x2 |
| Expected result | CPT column shows '36415×2' |
| Result (C1 → C2) | Pass → Pass |
| Automation | Manual only |
