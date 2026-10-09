# Lab 23 — Evidence Request Register

**As of:** October 9, 2026  
**Purpose:** Track evidence received and follow-up needed for the scoped assessment. This repository register consolidates the assessment; it does not change a separately maintained spreadsheet.

Original request, receipt, due, and follow-up dates not independently established are left unspecified. Examination of historical screenshots on October 9 is not their original receipt date.

| REQUEST ID | NIST CONTROL | DEPARTMENT | EVIDENCE REQUESTED | DATE REQUESTED | DUE DATE | DATE RECEIVED | STATUS | EVIDENCE RECEIVED | EVIDENCE LINK | NEXT ACTION | FOLLOW-UP DUE | ASSESSOR NOTES |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| AC-02 | AC-2 Account Management | IAM / IT; HR for authorization | HR approvals; account-management policy; termination SLA and ticket history; entitlement inventory; recurring review requirements and results | Not established | Not set | Not established | Partially received — additional evidence required | Lab 15 account/group/cloud validation; Lab 06 one-time review decisions, audit history, and final direct-member list | [Lab 15](../Lab-15-Ticket-Driven-Identity-Lifecycle/README.md); [Lab 06](../Lab-06-Entra-Access-Reviews/README.md) | Obtain remaining authorization, timing, complete access and recurring-review evidence; detailed per-user review decisions and applied-result logs | Not set | Group/cloud gaps resolved. One review supported; recurring program and complete AC-2 effectiveness remain unverified. |
| AC-06 | AC-6 Least Privilege | IAM / IT | Readable PIM artifacts; role settings; complete active/eligible privilege inventory; task-to-role rationale; approvals and privileged-access reviews | October 9, 2026 | Not set | Not established | Partially received — additional evidence required | Lab 08 readable membership views, eligible-role view and PIM audit history; supplemental Lab 06 membership reduction | [Lab 08](../Lab-08-Entra-Privileged-Identity-Management/README.md); [Lab 06](../Lab-06-Entra-Access-Reviews/README.md) | Recover authentic readable PIM artifacts and obtain settings, inventory, narrowest-role rationale and review records | Not set | Five Lab 08 images unreadable; selected activation/removal events and membership outcomes supported. Complete effective privileges not established. |
| IA-02 | IA-2 Identification and Authentication | IAM / IT | Current policy export; named exclusions; authentication and policy-evaluation details; approved MFA enforcement requirements and rollout plan | October 9, 2026 | Not set | Not established | Partially received — additional evidence required | Lab 02 tenant/user views, Authenticator registration, report-only MFA policy and successful single-factor sign-in | [Lab 02](../Lab-02-Entra-Conditional-Access/README.md) | Establish required enforcement state and examine current settings and representative detailed sign-in outcomes | Not set | Readiness supported; MFA enforcement not demonstrated. Applicable enhancements and full scope remain to be selected. |

No request is closed. Outstanding evidence does not automatically establish a control failure or justify a POA&M item.

## Consolidated Collection List

1. **Documents:** HR approvals and ticket history; approved termination timeframe; account and privilege policies; business entitlement approvals; recurring review schedule and completed review records.
2. **PIM:** Authentic readable originals for Lab08-01, 02, 03, 05 and 06; current role settings; full role inventory; task-to-role rationale; detailed audit records.
3. **MFA:** Current full policy settings and named exclusions; approved rollout/enforcement requirements; detailed representative sign-ins and policy results.
4. **Access review:** Named user decisions and justification; persisted reviewer settings; applied-result and membership-removal records; Lisa's account state if retained-enabled status is to be substantiated.

Historical records cannot be recreated by a new screenshot. New captures must be labeled as follow-up validation, with their actual date.
