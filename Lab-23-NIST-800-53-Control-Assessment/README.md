# Lab 23 — NIST SP 800-53 Security Control Assessment & POA&M

## Overview

Vandelay Health is a fictional healthcare technology company headquartered in Santa Monica, California. Its Ninja Sleeper CPAP technology originated from a federal government project and was subsequently adapted for commercial use.

The Ninja Sleeper incorporates highly restricted, proprietary intellectual property. Vandelay Health uses Active Directory, Microsoft Entra ID, and Okta to manage workforce identities and protect access to organizational resources.

## Assessment Objective

Evaluate selected security controls against NIST SP 800-53 Revision 5 using evidence collected from the Vandelay Health identity environment.

Document control effectiveness, evidence limitations, potential deficiencies, remediation recommendations, and Plans of Action and Milestones (POA&Ms).

## Assessment Report

[Security Assessment Report — Working Draft v0.4](Security-Assessment-Report.md)

Updated October 9, 2026 with the October 8 Lab 15 follow-up evidence. The report includes the evidence mapping, assessment limitations, observation statuses, and next activities.

## Control 1 — AC-2: Account Management

**Evidence source:** Lab 15 — Ticket-Driven Identity Lifecycle Operations

**Assessment method:** Examine existing documentation and screenshots.

### Evidence Reviewed

- New employee account creation and validation
- Role-based security group assignment
- Employee account disablement
- Security group access removal
- Entra Connect synchronization
- Microsoft Entra ID account validation

### Assessment Results

The available evidence supports selected account provisioning and termination outcomes: Joe's enabled AD account, IC group membership, corrected department and synchronized Entra identity; Paul's disabled AD account, specified IC group removal and disabled Entra identity.

Follow-up screenshots captured October 8 establish these states at the time of review. The delta synchronization command confirms request acceptance; Joe's updated Entra properties support arrival of the department correction.

However, the reviewed documentation does not independently establish original HR approvals and timestamps, termination SLA compliance, complete entitlement and session termination, documented account-management requirements, or periodic account review effectiveness.

**Assessment determination:** Partially assessed — insufficient evidence to conclude that the complete AC-2 control is satisfied.

### Observations

**AC2-OBS-001:** Termination timeliness cannot be independently verified from the available evidence.

**AC2-OBS-002:** Periodic account review effectiveness was not established by the reviewed Lab 15 artifacts.

Additional authorization, policy, and entitlement-coverage limitations are detailed in the report. Joe's initial department discrepancy was corrected and recorded as a resolved lab data observation.

These open items are evidence or assessment limitations, not confirmed security control failures. No POA&M items have been opened.

## Control 2 — AC-6: Least Privilege

**Evidence source:** Lab 08 — Privileged Identity Management.

**Assessment method:** Examine documentation and readable screenshots.

Readable group views support Eric's targeted membership change. PIM audit history supports eligibility, activation, and expired-activation removal events. The eligible-role view alone does not prove absence of active privilege.

Five repository images could not be decoded; their downloaded bytes matched the repository blob hashes. Exact activation duration, justification, approval/MFA settings, complete privileges, and narrowest-role rationale remain insufficiently evidenced.

**Assessment determination:** Partially assessed — selected outcomes supported; additional evidence required.

No confirmed unresolved access-control deficiency has been established. Detailed evidence requests and observations appear in the report.

## Next Assessment

Authentication and multifactor authentication controls.

---

*This project is a portfolio-based security control assessment performed in a fictional training environment. It is not an independent compliance audit or formal authorization assessment.*
