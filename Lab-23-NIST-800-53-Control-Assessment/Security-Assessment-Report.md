# VANDELAY HEALTH

## Security Assessment Report (SAR) — Working Draft v0.5

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

The initial AC-2 examination now includes October 8 follow-up evidence from Lab 15. This supports selected provisioning, group-management, identity-attribute correction, account disablement, and cloud-validation outcomes. Authorization, termination timeliness, complete entitlement coverage, and periodic account reviews remain insufficiently evidenced. The AC-6 examination supports selected PIM lifecycle events and a targeted group-membership change, with limitations concerning unreadable artifacts, complete privilege inventory, activation settings, and least-role rationale. The IA-2 review confirms Authenticator registration and a report-only MFA policy; the captured successful sign-in is single-factor, so MFA enforcement is not demonstrated. No final compliance determination has been made.

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

**Assessment objective:** Examine whether privileged access is limited to operational need and whether the selected incident demonstrates targeted entitlement changes.

**Assessment method:** Examine Lab 08 documentation and readable repository screenshots. No independent activation test or process-owner interview was performed.

**Evidence source:** [Lab 08 — Privileged Identity Management](../Lab-08-Entra-Privileged-Identity-Management/README.md).

| Evidence | Visible result | Assessment use |
|---|---|---|
| Lab08-04 — Eric group membership before remediation | Eric's named group view lists SG-IC-Users | Supports the visible pre-change membership |
| Lab08-07 — Eric group membership after remediation | Eric's named group view lists SG-IC-Users and M365-IC-Team | Supports addition of the identified collaboration membership |
| Lab08-08 — PIM My roles | User Administrator appears under Eligible assignments | Supports eligibility at capture time; does not alone prove absence from Active assignments or absence of other active roles |
| Lab08-09 — PIM audit history | Successful eligibility and activation events and a removal event labeled for an expired PIM activation | Supports the recorded eligibility, activation, and expiration-removal lifecycle |

**Evidence reliability limitation:** Repository image files Lab08-01, Lab08-02, Lab08-03, Lab08-05, and Lab08-06 could not be decoded for visual examination. Independently downloaded bytes matched their repository Git blob hashes, so the unreadability was not resolved by downloading again. Those files are not used as visual support for conclusions. Their filenames and README captions are not substitutes for readable evidence.

**Assessment observations:**

The readable evidence supports selected least-privilege practices: PIM eligibility and activation events, removal of an expired activation, and a before-and-after group-membership change addressing a specific collaboration entitlement.

The README describes a one-hour activation and incident-specific justification. The readable artifacts do not independently establish the exact activation duration, the full justification text, required approval, or multifactor authentication settings. These remain documented claims requiring supporting evidence.

The User Administrator role has broader permissions than a single group-membership change. Its temporary use demonstrates time-limited privilege; it does not by itself establish that the narrowest suitable role or scope was chosen. The selected screenshots also do not establish the administrator's complete effective privileges, the business approval for Eric's access, or successful access to the underlying application.

**Remaining evidence requests:**

- Readable original eligibility, activation, and role-settings evidence, including duration, justification, approval, and authentication requirements.
- Complete active and eligible administrative-role inventory, including inherited or group-based assignments and relevant role scopes.
- Documented task-to-role rationale and comparison with narrower roles or delegated group ownership.
- Approved business access baseline and authorization for Eric's collaboration entitlement.
- Privileged-access review records and evidence of review or removal of unnecessary assignments.
- Detailed audit records linking the activated administrator to the membership change.

**Assessment determination:**

**Partially assessed — selected PIM lifecycle and targeted membership outcomes supported; additional evidence required to establish complete AC-6 effectiveness.**

No conclusion is made for all AC-6 requirements or enhancements.

**POA&M determination:** No confirmed unresolved access-control deficiency established. Record unreadable artifacts and unverified control settings as evidence limitations. Replace unreadable screenshots with authentic readable evidence before relying on them.


#### 4.3 IA-2 — Identification and Authentication

**Assessment objective:** Examine identification and authentication evidence, with a limited focus on workforce MFA configuration and demonstrated enforcement. Applicable IA-2 enhancements and organization-defined requirements have not yet been selected or fully assessed.

**Assessment method:** Examine Lab 02 documentation and all five repository screenshots. No independent sign-in test was performed.

**Evidence source:** [Lab 02 — Conditional Access and MFA](../Lab-02-Entra-Conditional-Access/README.md).

| Evidence | Visible result | Assessment use |
|---|---|---|
| Lab02-01 — tenant overview | Tenant display name Vandelay World Wide; Microsoft Entra ID P2 license | Establishes the lab tenant context; fictional business narrative uses Vandelay Health |
| Lab02-02 — John Smith overview | Named member identity, enabled account, MFA-capable status | Supports account identification and authentication capability, not MFA enforcement |
| Lab02-03 — authentication methods | Microsoft Authenticator listed as usable; notification default method | Confirms registered method for the test identity |
| Lab02-04 — Conditional Access policy | Report-only; all users; all resources; two users excluded; Require multifactor authentication; one client-app category included | Confirms proposed MFA configuration and non-enforcing state at capture time |
| Lab02-05 — named sign-in details | John Smith; Success; Single-factor authentication; August 7, 2026 | Confirms successful sign-in; does not establish MFA completion or policy enforcement |

**Assessment observations:**

The evidence demonstrates a named workforce identity, Authenticator registration, and a Conditional Access policy configured with an MFA requirement in report-only mode. The policy screenshot explicitly states that it is evaluated but not enforced.

The successful sign-in is marked single-factor authentication. It cannot be used as evidence that this sign-in completed MFA or that the report-only policy enforced an MFA requirement. The Authentication Details, Conditional Access, and Report-only tabs are visible but their contents are not captured.

The policy summary identifies two excluded users but does not name them. Lab 02 describes these as a break-glass identity and a designated administrator; their identities, approvals, and compensating protections require additional evidence. The included client-app category is not identified in the summary.

Report-only deployment is consistent with Lab 02's documented staged evaluation objective. This is not, by itself, a confirmed control failure. Whether enforcement is required at the assessed stage must be established from the selected control requirements, approved rollout plan, and other applicable authentication controls. The August screenshots do not establish current tenant configuration.

**Remaining evidence requests:**

- Current full policy export or detailed screenshots covering state, users, exclusions, resources, conditions, client apps, and grant controls.
- Named excluded identities, exception authorization, and emergency-access protection and monitoring requirements.
- Authentication Details and policy-evaluation results for representative sign-ins.
- If enforcement is required, an enabled MFA policy and representative sign-in results demonstrating MFA satisfaction and handling of attempts that do not satisfy the requirement.
- Approved rollout plan, enforcement criteria and target date, authentication requirements, applicable IA-2 enhancements, and coverage of privileged and non-privileged users.
- Inventory of other controls that could enforce MFA, and evidence of their actual scope and operation.

**Assessment determination:**

**Partially assessed — identity and MFA readiness configuration supported; MFA enforcement not demonstrated by the reviewed evidence.**

No conclusion is made that the complete IA-2 control or its MFA-related enhancements are satisfied.

**POA&M determination:** No confirmed unresolved control deficiency established from the staged lab evidence alone. If required MFA coverage is subsequently confirmed absent, assess the resulting deficiency and open a POA&M item with supported scope and risk.

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

AC6-OBS-001: Five Lab 08 image artifacts were unreadable during examination. Obtain readable originals.

AC6-OBS-002: Exact activation duration, justification, approval, and authentication requirements are not independently established by readable evidence.

AC6-OBS-003: Complete effective privilege inventory, narrowest-role rationale, entitlement approval, and privileged-access reviews remain unverified.

These AC-6 observations are evidence limitations, not confirmed access-control failures.

IA2-OBS-001: MFA readiness is documented, but the reviewed policy is report-only and the captured sign-in is single-factor. Establish required enforcement state and examine current policies and detailed sign-in results.

IA2-OBS-002: Excluded identities, exception approvals, client-app scope, and complete authentication coverage are not established by the policy summary.

These IA-2 observations require additional evidence and are not, on their own, confirmed control failures.

### 6. Remediation Planning

Confirmed unresolved deficiencies will be entered into a POA&M with documented risk, responsible owner, corrective action, target completion date, and validation requirements.

No POA&M items have been opened at this stage. The resolved department discrepancy remains documented in the observation record.

### 7. Next Assessment Activities

- Complete the evidence request register for the remaining AC-2 limitations.
- Resolve the AC-6 evidence limitations and review relevant privilege inventory and settings.
- Review authentication, privileged access, and identity governance controls.
- Validate observations and identify any confirmed deficiencies.
- Develop corrective-action recommendations and POA&M items where warranted.
- Prepare the final assessment report and executive summary.

---

**Document status:** Working Draft v0.5 — Simulated Internal Assessment.

This report is a portfolio exercise using NIST SP 800-53 and NIST SP 800-53A assessment principles. It does not represent a formal federal security authorization or independent FedRAMP assessment.
