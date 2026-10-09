# Lab 23 — Internal Identity Security Assessment
## Work in Progress — Planning and Initial Evidence Review

Vandelay Health is a fictional healthcare technology company headquartered in Santa Monica, California. Its Ninja Sleeper CPAP technology originated from a federal government project and was subsequently adapted for commercial use.

The Ninja Sleeper incorporates highly restricted, proprietary intellectual property. Vandelay Health uses Active Directory (AD), Microsoft Entra ID, and Okta to manage workforce identities and protect access to organizational resources.

## Business Request

In this simulated scenario, executive leadership requested a 30-day internal assessment of identity and access management (IAM) controls. Acting as a Security & Compliance Analyst, I am documenting the project plan, evidence collection, selected control examinations, and follow-up work under **SEC-2026-1023**.

The objective is to evaluate implementation and operation, identify supported deficiencies, and recommend corrective actions. The results are intended to inform leadership about identity security posture and preparation for potential future federal contracting requirements.

## What I Have Documented So Far

- A project scope covering AD, Entra ID, hybrid synchronization, and applicable Okta processes for the El Segundo warehouse.
- Planned stakeholder coordination, evidence response deadlines, and executive reporting milestones.
- An evidence request register covering account management, least privilege, and authentication.
- Preliminary examinations of existing evidence from Labs 15, 06, 08, and 02.
- Supported observations, evidence limitations, and specific follow-up requests.

This is an ongoing assessment project. Documented examinations are one part of the work; they do not establish completion of the overall assessment or full control effectiveness.

## Project Blueprint

The planned assessment period is 30 calendar days, with a preliminary CISO briefing on Day 14 and final executive presentation on Day 30. These are scenario milestones, not claims that the briefings or final delivery have occurred. Calendar dates remain to be confirmed.

The plan identifies IAM Administration, IT Infrastructure, Security Engineering, HR Operations, Compliance/GRC, and Warehouse IT as stakeholders. Evidence responses are expected within five business days, with material delays escalated to the Chief Information Security Officer (CISO).

Resource assignments, stakeholder interviews, and independent technical validation remain planned activities. Actual progress will be documented as the lab develops.

## Current Control Reviews

| Request | Control | Current progress |
|---|---|---|
| EV-001 | AC-2 — Account Management | Selected account and membership outcomes and one access review supported; authorization, timing, full access coverage, and recurring-review evidence remain open |
| EV-002 | AC-6 — Least Privilege | Selected Privileged Identity Management (PIM) lifecycle and membership evidence examined; readable artifacts, complete privileges, settings, and role rationale remain open |
| EV-003 | IA-2 — Identification and Authentication | Identity and multifactor authentication (MFA) readiness evidence examined; reviewed policy was report-only and enforcement remains unverified |

All three reviews are partially assessed. Okta evidence has not yet been examined in this report.

## How I Am Developing the Assessment

I compare documented claims with the evidence available, record exactly what each artifact supports, and identify the records needed to answer remaining questions.

My next evidence activity is a retrospective review of Lab 15: identify what the original collection captured, what follow-up already resolved, and what specific evidence is still needed. New captures will be dated and labeled as follow-up validation. They will not be presented as historical proof.

## Working Documents

- [Project Scope and Assessment Plan](Project-Scope.md)
- [Security Assessment Report — working report](Security-Assessment-Report.md)
- [Evidence Request Register](Evidence-Request-Register.md)
- [Plan of Action and Milestones (POA&M) disposition](POAM.md)

The Google Docs report and Google Sheets tracker are maintained separately. Repository copies document this published checkpoint.

## Remaining Work

- Review the existing evidence and conclusions together.
- Obtain outstanding authorization, timing, access-review, privilege, and authentication records.
- Collect applicable Okta evidence.
- Confirm assessment dates and resource availability.
- Conduct stakeholder interviews and technical validation where feasible.
- Record confirmed deficiencies and corrective actions only when supported.
- Prepare preliminary and final executive deliverables.

## Assessment Boundaries

I have documented examination of existing portfolio evidence. No completed stakeholder interviews or independent assessor tests are documented. Historical captures do not establish current tenant-wide effectiveness.

Missing evidence is an assessment limitation; it is not automatically a control failure. No confirmed unresolved deficiency has been established from the examined evidence, and no active POA&M items have been opened. This does not establish that the environment is free of weaknesses.

*This is a fictional portfolio training exercise using selected NIST SP 800-53 Revision 5 controls and an approach informed by NIST SP 800-53A Revision 5. It is not an independent compliance audit, federal authorization, or FedRAMP assessment.*

**Checkpoint:** October 9, 2026 — work in progress.
