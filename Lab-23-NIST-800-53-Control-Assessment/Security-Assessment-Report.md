# VANDELAY HEALTH

## Security Assessment Report (SAR) — Working Draft v0.3

**Project:** SEC-2026-1023  
**Prepared by:** Security & Compliance Analyst  
**Assessment Framework:** NIST SP 800-53 Revision 5  
**Assessment Procedures:** NIST SP 800-53A Revision 5  
**Status:** Preliminary — Assessment in Progress  
**Assessment Type:** Simulated Internal Security Control Assessment  
**Updated:** October 9, 2026

---

### 1. Executive Summary

Vandelay Health has initiated an internal security assessment of its identity and access management (IAM) environment in response to a simulated executive request.

The assessment focuses on account management, employee access, authentication, privileged access, and identity governance across Active Directory, Microsoft Entra ID, and selected Okta processes.

The objective is to examine implementation evidence, identify supported security weaknesses, and recommend corrective actions.

The initial AC-2 examination now includes October 8 follow-up evidence from Lab 15. This supports selected provisioning, group-management, identity-attribute correction, account disablement, and cloud-validation outcomes. Authorization, termination timeliness, complete entitlement coverage, and periodic account reviews remain insufficiently evidenced. No final compliance determination has been made.

### 2. Assessment Scope

**Systems in scope:**

- Microsoft Active Directory
- Microsoft Entra ID
- Microsoft Entra Connect synchronization
- Okta identity services supporting the El Segundo warehouse, where applicable

**Assessment focus:**

- Account provisioning and termination
- Least-privilege access
- Authentication and multifactor authentication
- Privileged access management
- Periodic access reviews

**Out of scope:**

- Network penetration testing
- Application source-code testing
- Medical device safety testing
- Formal FedRAMP authorization

### 3. Assessment Methodology

Selected controls will be assessed using applicable NIST SP 800-53A methods:

- **Examine:** Review configuration records, screenshots, policies, and identity lifecycle documentation.
- **Interview:** Identify questions for responsible system and process owners. Proposed questions are not completed interviews.
- **Test:** Validate control operation where the lab environment permits. Historical screenshots are examination evidence, not independent assessor testing.

Evidence will be evaluated for relevance, completeness, and reliability. Missing documentation is an evidence limitation rather than automatically a control failure. Assessment conclusions will distinguish verified states, documented scenarios, and untested outcomes.

### 4. Control Assessment Results

#### 4.1 AC-2 — Account Management

**Assessment objective:** Determine whether account provisioning, modification, disabling, and termination are supported by documented authorization, access changes, and validation.

**Assessment method:** Examine existing lab documentation and screenshots. No independent assessor test or process-owner interview was performed.

**Evidence source:** [Lab 15 — Ticket-Driven Identity Lifecycle Operations](../Lab-15-Ticket-Driven-Identity-Lifecycle/README.md).

**Evidence reviewed:**

| Evidence | Visible result | Assessment use |
|---|---|---|
| Lab15-02 — original Joe AD account output | Enabled account and Toronto attributes; original department Information Technology | Supports existence and enabled state; identifies attribute subsequently corrected |
| Lab15-04 — Paul pre-termination output | Account enabled and member of SG-TOR-IC-Users | Establishes the documented pre-change account state |
| Lab15-05 — Paul AD offboarding output | Enabled = False; group-removal command | Establishes AD disablement; command alone does not prove membership removal |
| Lab15-07 — Joe AD Member Of | SG-TOR-IC-Users and Domain Users | Confirms specified IC membership on October 8 |
| Lab15-08 — Paul AD Member Of | Domain Users; SG-TOR-IC-Users absent | Confirms specified IC membership removed on October 8 |
| Lab15-09 — Joe saved AD organization properties | Department Innovation Center | Confirms correction of the initial department attribute |
| Lab15-10 — Paul named Entra properties | Account enabled: No; on-premises sync enabled: Yes | Confirms disabled synchronized cloud identity on October 8 |
| Lab15-11 — delta synchronization command | Start-ADSyncSyncCycle -PolicyType Delta returns Success | Confirms acceptance of the sync request, not completion of every export |
| Lab15-12 — Joe named Entra properties | Enabled: Yes; on-premises sync enabled: Yes; department Innovation Ce…; last sync October 8, 2026 at 6:11 PM | Supports synchronized identity and arrival of the corrected department value |

**Assessment observations:**

The reviewed evidence supports selected account-management activities: an enabled new-hire AD account, specified security-group membership, correction of an identity attribute, AD account disablement, removal of the specified IC membership, and the corresponding enabled/disabled cloud account states.

The October 8 follow-up evidence resolves the previously recorded gaps concerning Joe's completed group membership, Paul's specified group removal, and explicit Entra account-state validation. The delta request and Joe's updated cloud properties support synchronization of Joe's corrected attribute. They do not establish the original termination synchronization time.

Joe's initial department was Information Technology rather than the requested Innovation Center. This discrepancy was corrected and verified in AD and Entra during the follow-up review. It is recorded as a resolved lab data discrepancy; this single example does not establish an organization-wide AC-2 control failure.

The fictional scenario describes HR-driven requests, but independent authorization records and timestamps were not available for examination.

**Remaining evidence limitations:**

- Original HR authorization and approval records, including timestamps.
- Defined termination service-level agreement (SLA) and original receipt, execution, and completion timestamps.
- A complete entitlement inventory and validation across applicable systems and applications.
- Documented account-management policy, assigned responsibilities, approval requirements, and review frequency.
- Completed periodic account reviews and resulting corrective actions.

October 8 screenshots establish states at the time of review. They do not prove the original ticket was completed within a required timeframe, that all application access or existing sessions were revoked, or that periodic reviews operated effectively.

**Assessment determination:**

**Partially assessed — selected account-management outcomes supported; additional evidence required for a complete AC-2 determination.**

This is a limited examination of two simulated lifecycle cases, not a determination that every AC-2 requirement or enhancement is satisfied.

**Recommended follow-up:**

Request the authorization records, account-management policy and responsibilities, defined termination timeframe and supporting ticket history, complete entitlement inventory, and completed periodic-review records. Identify any untested session or application-access termination requirements before concluding that corporate access was fully terminated.

**POA&M determination:**

No confirmed unresolved security control deficiency has been established from this evidence set. Track outstanding evidence requests separately from the Plan of Action and Milestones (POA&M). Retain the corrected department discrepancy as a resolved observation.

#### 4.2 AC-6 — Least Privilege

**Status:** Not yet assessed. No determination made.

### 5. Preliminary Findings

Selected AC-2 account-management outcomes are supported by the reviewed evidence.

| Observation | Status | Disposition |
|---|---|---|
| AC2-OBS-001 — Original termination timeliness not independently established | Open evidence limitation | Request defined SLA and original ticket/action timestamps |
| AC2-OBS-002 — Periodic account review effectiveness not established | Open evidence limitation | Request review schedule, completed reviews, and corrective-action evidence |
| AC2-OBS-003 — Authorization and account-management requirements not independently established | Open evidence limitation | Request approvals, policy, responsibilities, and review requirements |
| AC2-OBS-004 — Complete entitlement and session termination not assessed | Open assessment limitation | Identify applicable systems, entitlements, sessions, and required validation |
| AC2-OBS-005 — Joe department differed from scenario requirement | Resolved lab data discrepancy | Corrected to Innovation Center; follow-up AD and Entra evidence retained |

Earlier missing group and cloud-state validation is resolved by Lab15-07, Lab15-08, Lab15-10, and Lab15-12.

No confirmed unresolved security control deficiencies have been established at this stage. Evidence limitations remain separate from verified security weaknesses.

### 6. Remediation Planning

Confirmed unresolved deficiencies will be entered into a POA&M with documented risk, responsible owner, corrective action, target completion date, and validation requirements.

No POA&M items have been opened at this stage. The resolved department discrepancy remains documented in the observation record.

### 7. Next Assessment Activities

- Complete the evidence request register for the remaining AC-2 limitations.
- Assess AC-6 — Least Privilege using relevant portfolio evidence.
- Review authentication, privileged access, and identity governance controls.
- Validate observations and identify any confirmed deficiencies.
- Develop corrective-action recommendations and POA&M items where warranted.
- Prepare the final assessment report and executive summary.

---

**Document status:** Working Draft v0.3 — Simulated Internal Assessment.

This report is a portfolio exercise using NIST SP 800-53 and NIST SP 800-53A assessment principles. It does not represent a formal federal security authorization or independent FedRAMP assessment.
