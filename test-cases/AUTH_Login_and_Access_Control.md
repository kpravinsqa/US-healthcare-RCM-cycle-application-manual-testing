# Login & Access Control (AUTH): Test Cases

7 test cases. Execution results show Cycle 1 → Cycle 2.

## TC_RCM_AUTH_001: Billing Admin login

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-01 / TS_RCM_AUTH_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | billing_admin / Health@123 |
| Steps | 1. Log in as billing_admin |
| Expected result | Lands on Patients; all 5 modules in menu |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_login_and_roles.py::test_each_role_lands_on_its_home_page` |

## TC_RCM_AUTH_002: Provider login lands on dashboard

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-01 / TS_RCM_AUTH_01 |
| Priority / Type | P1 / Functional |
| Preconditions | - |
| Test data | - |
| Steps | 1. Log in as dr_smith |
| Expected result | Provider Dashboard shown for Dr. John Smith |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_login_and_roles.py::test_each_role_lands_on_its_home_page` |

## TC_RCM_AUTH_003: Username is case-sensitive

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-01 / TS_RCM_AUTH_02 |
| Priority / Type | P2 / Negative |
| Preconditions | - |
| Test data | - |
| Steps | 1. Log in as BILLING_ADMIN |
| Expected result | Error 'Invalid username or password' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_login_and_roles.py::test_invalid_login` |

## TC_RCM_AUTH_004: Front Desk menu hides billing modules

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-02 / TS_RCM_AUTH_03 |
| Priority / Type | P1 / Security |
| Preconditions | - |
| Test data | - |
| Steps | 1. Log in as front_desk |
| Expected result | Only Patients and Encounters visible |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_login_and_roles.py::test_front_desk_menu_hides_billing_modules` |

## TC_RCM_AUTH_005: Front Desk direct URL to Claims

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-02 / TS_RCM_AUTH_03 |
| Priority / Type | P1 / Security |
| Preconditions | - |
| Test data | - |
| Steps | 1. Log in as front_desk<br>2. Open /claims.html |
| Expected result | 'Access denied' page; no claim data |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/ui/test_login_and_roles.py::test_front_desk_direct_url_to_claims_is_denied` |

## TC_RCM_AUTH_006: Front Desk calls Claims API

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-02 / TS_RCM_AUTH_03 |
| Priority / Type | P1 / Security |
| Preconditions | - |
| Test data | - |
| Steps | 1. Use front_desk token on GET /api/claims |
| Expected result | 403 'You do not have permission to access this module' |
| Result (C1 → C2) | Pass → Pass |
| Automation | `tests/api/test_rcm_api.py::test_front_desk_cannot_call_claims_api` |

## TC_RCM_AUTH_007: Session timeout after 15 minutes idle

| Field | Value |
|---|---|
| Requirement / Scenario | REQ-02 / TS_RCM_AUTH_03 |
| Priority / Type | P2 / Security |
| Preconditions | - |
| Test data | - |
| Steps | 1. Log in<br>2. Stay idle 15 minutes<br>3. Click any menu |
| Expected result | Redirected to login with session-expired message |
| Result (C1 → C2) | Fail → Fail (DEF-RCM-06) |
| Automation | Manual only |
