# Lab 23 — Internal Identity Security Assessment
**Work in progress | Project SEC-2026-1023**

Vandelay Health is a fictional healthcare technology company based in Santa Monica, California. Its Ninja Sleeper CPAP technology began as a federal government project and was later adapted for commercial use.

The Ninja Sleeper contains highly restricted, proprietary intellectual property. I use this business scenario throughout my portfolio to explore how Active Directory (AD), Microsoft Entra ID, and Okta can manage employee identities and protect access to company resources.

## Why I Started This Assessment

In this lab’s scenario, I received a ticket from executive leadership asking for a 30-day review of the company’s identity and access management (IAM) controls.

My job as the Security & Compliance Analyst is to answer three practical questions: Are the controls in place? Do they work as intended? Can I show enough evidence to support my answers?

Leadership wants to understand the company’s identity security posture and prepare for possible future federal contracting requirements. I am using selected National Institute of Standards and Technology (NIST) SP 800-53 Revision 5 controls to organise the review, with SP 800-53A Revision 5 guiding how I examine the evidence.

## How I Planned the Work

I documented the scope before moving into the technical review. It covers AD, Entra ID, their synchronization, and Okta’s support for the El Segundo warehouse.

I also documented which departments the assessment would need to involve: IAM Administration, IT Infrastructure, Security Engineering, HR Operations, Compliance/GRC, and Warehouse IT. My plan gives department owners five business days to respond to evidence requests. Material delays would go to the Chief Information Security Officer (CISO).

The scenario calls for a preliminary CISO briefing on Day 14 and a final executive presentation on Day 30. I have included those milestones in the plan. I still need to confirm calendar dates, resource assignments, and appointments for interviews and testing.

This lab is a running project. I will add completed work as I go.

## What I Have Done So Far

I have prepared the project scope, created an evidence tracker, and developed a working Security Assessment Report (SAR).

I have also documented an initial review of screenshots and records from my earlier labs. I am checking what those records actually show and where I need more information. My tracker records what I requested, which department is responsible, what I received, and what I still need.

I started with three control reviews:

| Evidence request | Control | Question I am working through |
|---|---|---|
| EV-001 | AC-2 — Account Management | When someone joins, changes roles, or leaves, are their account and access handled appropriately? |
| EV-002 | AC-6 — Least Privilege | Does someone have only the permissions they need, and is temporary administrator access properly managed? |
| EV-003 | IA-2 — Identification and Authentication | How does someone prove their identity, and is required multifactor authentication actually enforced? |

These are three parts of one assessment. Each contributes to the same report.

## What the Evidence Has Shown Me

For account management, I used Joe Cantoni’s onboarding and Paul Merson’s offboarding from Lab 15. Follow-up screenshots support Joe’s specified group membership, Paul’s removal from the specified group, and Paul’s disabled account in Entra ID. They also document the correction of Joe’s department.

That gives me evidence of particular account states and changes. I still need the original approvals and timestamps to establish who authorised the work and whether it was completed within the required timeframe. I also need to check the full range of access that should have been removed.

Lab 06 gives me an example of a completed access review. I still need more detail linking individual decisions to the resulting access changes, and records showing how reviews would operate on a recurring basis.

For least privilege, Lab 08 contains readable Privileged Identity Management (PIM) records showing eligibility, activation, and removal of an expired activation. Some images were unreadable during the documented review. I need readable evidence and more detail about role settings, approvals, and why the chosen role was appropriate for the task.

For authentication, Lab 02 shows Microsoft Authenticator registration and a Conditional Access policy requiring multifactor authentication (MFA). The policy was in report-only mode, and the captured successful sign-in used single-factor authentication. Those records do not demonstrate MFA enforcement. My next task is to establish what enforcement was required and examine the relevant settings and sign-in details.

I have not yet examined Okta evidence for this assessment.

## What I Am Doing Next

I will start by reviewing Lab 15’s evidence collection. I want to identify what I captured originally, what the October follow-up already resolved, and which questions still need a specific record or screenshot.

If I take new screenshots, I will record the actual date and explain what they demonstrate. A screenshot taken today can show today’s account state; it cannot establish when an earlier termination was completed.

I will then work through the remaining privilege and authentication evidence, collect applicable Okta records, and develop the planned interviews and technical checks.

## My Working Documents

I keep the project’s purpose and scope in the [Project Scope and Assessment Plan](Project-Scope.md).

I record my observations and the limits of the evidence in the [Security Assessment Report](Security-Assessment-Report.md).

I track requests and follow-up in the [Evidence Request Register](Evidence-Request-Register.md). I also maintain the working report in Google Docs and the tracker in Google Sheets; these repository copies show the published checkpoint.

I have prepared a [Plan of Action and Milestones (POA&M) disposition](POAM.md). If the assessment establishes an unresolved security deficiency, I will use the POA&M to document the corrective action, owner, deadline, and evidence needed to confirm the fix.

## Where the Project Stands

The assessment is still in progress. So far, I have documented planning and examination of existing evidence. I have not completed stakeholder interviews or independent assessment tests.

I have not established a confirmed unresolved security deficiency from the evidence reviewed so far. Several questions remain open. When a record is missing, I document the gap and request what I need before reaching a conclusion.

This is a simulated portfolio assessment. It does not establish company-wide compliance or represent a federal authorization or FedRAMP assessment.

**Last updated: October 9, 2026**
