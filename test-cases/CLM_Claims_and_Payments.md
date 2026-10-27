# Claims & Payments (CLM): Test Cases

9 test cases. Execution results show Cycle 1 → Cycle 2.

## TC_RCM_CLM_001: Create and submit claim

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-11 / TS_RCM_CLM_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Create claim from open encounter<br>2. Submit |
| Expected result | Claim CLM-xxxxxxx DRAFT → SUBMITTED; billed = encounter charge |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_claims.py::test_create_and_submit_claim` |

## TC_RCM_CLM_002: Second claim for same encounter

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-11 / TS_RCM_CLM_01 |
| Priority / Type | P1 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Create claim twice for one encounter |
| Expected result | 409 'A claim already exists for this encounter' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/api/test_rcm_api.py::test_claim_cannot_be_created_twice` |

## TC_RCM_CLM_003: Self-pay claim rejected

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-12 / TS_RCM_CLM_02 |
| Priority / Type | P1 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Create claim for Self-Pay patient<br>2. Submit |
| Expected result | Status REJECTED with scrub message |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_claims.py::test_self_pay_claim_is_rejected_by_scrubber` |

## TC_RCM_CLM_004: Timely filing day 365 vs 366

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-12 / TS_RCM_CLM_02 |
| Priority / Type | P1 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. Submit claims with DOS 365 and 366 days ago |
| Expected result | 365 SUBMITTED; 366 REJECTED 'Timely filing limit exceeded' |
| Result (C1 → C2) | Fail → Pass (DEF-RCM-05) |
| Automation | `tests/ui/test_claims.py::test_timely_filing_boundary` |

## TC_RCM_CLM_005: Partial then full payment

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-13 / TS_RCM_CLM_03 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Claim $175<br>2. Post paid 100 + adj 25<br>3. Post paid 50 |
| Expected result | PARTIALLY_PAID balance $50 → PAID balance $0 |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_claims.py::test_partial_then_full_payment` |

## TC_RCM_CLM_006: Overpayment blocked

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-13 / TS_RCM_CLM_03 |
| Priority / Type | P1 / Boundary |
| Preconditions | - |
| Test data | - |
| Steps | 1. Claim $120<br>2. Post 120.01 |
| Expected result | 'Paid + adjustment cannot exceed the outstanding balance' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_claims.py::test_overpayment_is_blocked` |

## TC_RCM_CLM_007: Payment on DRAFT claim

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-13 / TS_RCM_CLM_03 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Post payment to a DRAFT claim via API |
| Expected result | 409 'Payments can only be posted to submitted claims' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/api/test_rcm_api.py::test_payment_on_draft_claim_rejected` |

## TC_RCM_CLM_008: Negative paid / adjustment amounts

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-13 / TS_RCM_CLM_03 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Post -1<br>2. Post adjustment -5 |
| Expected result | Validation error on the field |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/api/test_rcm_api.py::test_payment_amount_validation` |

## TC_RCM_CLM_009: Claim list export to CSV for billing team

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-11 / TS_RCM_CLM_04 |
| Priority / Type | P3 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Click Export on Claims |
| Expected result | CSV with all visible columns |
| Result (C1 → C2) | Blocked → Pass |
| Automation | Manual only |
