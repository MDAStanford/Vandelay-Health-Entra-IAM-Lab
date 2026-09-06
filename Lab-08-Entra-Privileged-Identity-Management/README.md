# Lab 08 — Privileged Identity Management (PIM) & Just-in-Time Access

## Overview

This lab demonstrates Microsoft Entra Privileged Identity Management (PIM) and just-in-time (JIT) privileged access during an IAM support incident. Rather than maintaining standing User Administrator privileges, the IAM administrator was configured as **eligible** for the role and activated it only when elevated access was required.

The temporary role activation was used to investigate and remediate an access provisioning issue affecting a newly onboarded employee at Vandelay World Wide's Toronto Innovation Center.

**Workflow:** `Incident → Investigate → Activate JIT Privilege → Remediate → Verify → Privilege Expires → Audit`

## Business Scenario

A newly onboarded Toronto Innovation Center employee, **Eric Lund**, could sign in successfully but could not access the Innovation Center's Microsoft 365 collaboration resources.

**Incident:** `INC-2026-0817 — Toronto Innovation Center User Access Provisioning Issue`

The IAM administrator did not maintain standing User Administrator access. Microsoft Entra PIM was used to activate the role temporarily for the incident.

## Initial State

Eric Lund had been provisioned with the Innovation Center security group:

- `SG-IC-Users`

However, his expected Microsoft 365 collaboration entitlement was missing:

- `M365-IC-Team`

This represented a partial onboarding/provisioning failure rather than an authentication issue.

## Privileged Access Model

The IAM administrator was made **eligible** for the Microsoft Entra **User Administrator** role through PIM. Eligibility alone did not make the role active.

When elevated permissions were required, the administrator activated User Administrator for **one hour** with the incident-specific justification:

> INC-2026-0817 — Temporary User Administrator access required to remediate Toronto Innovation Center user account provisioning issue.

The activation was time-bound and recorded in PIM audit history.

## Investigation

Eric Lund's group memberships were reviewed before any change was made. The account showed `SG-IC-Users`, but `M365-IC-Team` was absent.

This established the root cause as a missing entitlement rather than a broader identity or account problem.

## Remediation

Eric Lund was added to `M365-IC-Team`.

After remediation, his group memberships showed both required Innovation Center groups:

- `SG-IC-Users`
- `M365-IC-Team`

The change was limited to the missing entitlement.

## Verification and Privilege Expiration

Post-remediation validation confirmed that Eric had both required group memberships. The one-hour User Administrator activation then expired, returning the administrator to an **eligible but non-active** state.

This demonstrates an important PIM distinction:

**Permanent eligibility does not equal permanent privilege.**

## Audit Evidence

Microsoft Entra PIM recorded the privileged-access lifecycle, including:

1. User Administrator eligibility request/completion
2. PIM activation request
3. Successful User Administrator activation
4. Automatic removal when the PIM activation expired

The audit trail provides evidence that privileged access was granted through a controlled, time-bound process rather than through a permanent active role assignment.

## Security Principles Demonstrated

- **Least privilege:** use the specific administrative role needed for the task rather than broader standing access.
- **Just-in-time access:** activate privileged access only when a legitimate business need occurs.
- **Time-bound privilege:** administrative access has a defined expiration.
- **Traceability:** privileged activation is tied to a documented incident and business justification.
- **Access validation:** inspect current identity and entitlement state before making a change.
- **Auditability:** retain evidence of eligibility, activation, remediation, expiration, and privileged-access history.

## Evidence

### 01 — User Administrator Eligible Baseline

No eligible User Administrator assignment existed before configuration.

![User Administrator eligible baseline](./01-User-Administrator-Eligible-Baseline.webp)

### 02 — User Administrator Eligible Assignment

The IAM administrator was made permanently **eligible**, not permanently active, for User Administrator.

![User Administrator eligible assignment](./02-User-Administrator-Eligible-Assignment.webp)

### 03 — PIM User Administrator Activated

User Administrator was activated temporarily through PIM for the incident.

![PIM User Administrator activated](./03-PIM-User-Administrator-Activated.webp)

### 04 — Eric Lund Before Remediation

Eric's group membership showed `SG-IC-Users`, while the expected Microsoft 365 collaboration group was absent.

![Eric Lund group membership before remediation](./04-Eric-Lund-Group-Membership-Before-Remediation.webp)

### 07 — Eric Lund Remediated

Post-remediation validation confirmed both `M365-IC-Team` and `SG-IC-Users` memberships.

![Eric Lund group membership remediated](./07-Eric-Lund-Group-Membership-Remediated.webp)

### 08 — User Administrator Returned to Eligible State

After the activation window ended, User Administrator was no longer active and was again available only through PIM activation.

![User Administrator returned to eligible state](./08-PIM-User-Administrator-Deactivated.webp)

### 09 — PIM Audit History

PIM audit history documented eligibility, activation, and automatic expiration/removal of the role.

![PIM User Administrator audit history](./09-PIM-User-Administrator-Audit-History.webp)

## Key Takeaways

A mature privileged-access process separates **eligibility** from **active privilege**. The administrator did not need User Administrator continuously; PIM allowed the role to be activated for a specific operational requirement, used within a defined window, and automatically removed afterward.

The incident also demonstrates the value of validating existing identity data before making changes. Investigation identified a single missing entitlement, so remediation was limited to that access rather than broadly reprovisioning the user.

## Technologies

- Microsoft Entra ID
- Microsoft Entra Privileged Identity Management (PIM)
- Microsoft Entra ID Governance
- Microsoft 365 Groups
- Entra Security Groups

## Skills Demonstrated

- Identity and Access Management (IAM)
- Privileged Access Management (PAM)
- Privileged Identity Management (PIM)
- Just-in-Time (JIT) Access
- Least Privilege
- Role-Based Access Control (RBAC)
- Identity Lifecycle Support
- Access Provisioning and Remediation
- Incident-Based Administration
- Access Validation
- Audit Evidence Review
- Microsoft Entra ID Administration
