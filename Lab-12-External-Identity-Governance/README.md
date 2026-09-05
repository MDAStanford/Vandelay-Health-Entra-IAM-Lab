# Lab 12 — Microsoft Entra External Identity Governance

## Technologies

- Microsoft Entra ID
- Microsoft Entra B2B Collaboration
- Microsoft Entra Identity Governance
- Microsoft Entra Access Reviews
- Microsoft 365
- Entra Security Groups

## IAM / Security Concepts

- External identity lifecycle
- B2B guest access
- Least privilege
- Group-based authorization
- Resource ownership
- Access certification
- Recurring access reviews
- Automated access remediation
- Separation of authentication and authorization

---

## Project Overview

This lab simulates the onboarding and governance of an external consultant who requires access to a sensitive product-development project at Vandelay Health.

Vandelay Health is developing the **Ninja Sleeper II**, the next generation of its lightweight, ultra-quiet CPAP device designed for frequent travelers. The new product is intended to be twice as quiet as the original Ninja Sleeper.

The project is being developed by Vandelay Health's Toronto Innovation Center (IC), with participation from selected company leadership.

To support the project, Vandelay Health engaged **Dr. Jameela Jamil**, an external medical industrial designer based in Edmonton, Alberta. Because Dr. Jamil is a consultant rather than a Vandelay Health employee, IAM needed to provide the collaboration access required for the engagement without creating an internal employee identity or granting broad access to Vandelay resources.

The resulting workflow demonstrates:

**External identity → B2B authentication → scoped authorization → access certification → lifecycle governance**

> **Note:** Vandelay Health, Ninja Sleeper, Jamil Industrial Design, the employees, and the business scenario used in this project are fictional. The environment was created solely as a hands-on identity and access management lab.

---

## Business Scenario

Dr. Jamil was retained by Vandelay Health to collaborate with the Toronto Innovation Center on the Ninja Sleeper II development project.

Her engagement created several IAM requirements:

- She must remain an external identity rather than receive a Vandelay employee account.
- She must be able to authenticate to Vandelay's Microsoft 365 environment.
- Successful authentication must not automatically provide access to company resources.
- Project access must be explicitly authorized.
- She must not inherit general Toronto Innovation Center access merely because she works with that team.
- An internal business owner must remain accountable for her continued access.
- Her access must be periodically reviewed and removable when the engagement no longer requires it.

The design therefore separates **identity establishment** from **resource authorization**.

---

## External Identity Onboarding

Dr. Jamil was invited to the Vandelay tenant using Microsoft Entra B2B collaboration.

Her Entra identity was configured as an external **Guest** rather than an internal Member account.

Relevant identity attributes included:

- **Name:** Dr. Jameela Jamil
- **Company:** Jamil Industrial Design
- **Job Title:** Medical Industrial Designer
- **Department:** Innovation Center
- **Employee Type:** Consultant/Contractor
- **Office Location:** Edmonton
- **Sponsor:** Lori Van Meter
- **User Type:** Guest

Lori Van Meter serves as the internal sponsor responsible for the business relationship and the consultant's continued need for access.

![External B2B invitation](01-jamil-b2b-invitation.png)

---

## B2B Invitation Redemption

Dr. Jamil received and redeemed the external collaboration invitation using her existing external identity.

During redemption, Microsoft presented the organizational consent requirements associated with accessing the Vandelay tenant.

![External user consent](02-jamil-b2b-consent.png)

After successful authentication and invitation redemption, Dr. Jamil reached the Microsoft 365 My Apps environment.

Importantly, no applications or resources were automatically available to her.

![Guest redemption completed](03-jamil-guest-redemption-complete.png)

This demonstrates an important IAM principle:

> **Authentication does not equal authorization.**

Dr. Jamil had successfully established a trusted external identity with Vandelay, but she still had no project access until that access was explicitly granted.

---

## Least-Privilege Project Access

Rather than adding Dr. Jamil to the existing Toronto Innovation Center employee group, a dedicated security group was created for Ninja Sleeper II:

**SG-NS2-Project**

The group was configured with assigned membership and no Entra administrative roles.

Its purpose is to provide an explicit authorization boundary for employees and approved external collaborators who require access to Ninja Sleeper II resources.

![NS2 project security group](04-ns2-project-security-group.png)

The completed group contained 11 authorized project participants and one resource owner.

![NS2 project group overview](05-ns2-project-group-overview.png)

Membership included the Toronto Innovation Center project team, selected Vandelay leadership, and Dr. Jamil.

Dr. Jamil appears as a **Guest**, while Vandelay employees appear as **Members**.

![NS2 project membership](06-ns2-project-membership.png)

This structure avoids granting the consultant broad organizational or Toronto IC access solely because she collaborates with that team.

Instead:

**Access is based on project need.**

---

## External Access Governance

Providing access was only the first part of the control.

Because Dr. Jamil is an external consultant, Vandelay also needs a mechanism to periodically verify that the business relationship remains active and that continued access is justified.

A Microsoft Entra Access Review was therefore created:

**Ninja Sleeper II External Access Review**

The review targets:

- **Resource:** SG-NS2-Project
- **Scope:** Guest users only
- **Reviewer:** Resource owner
- **Recurrence:** Quarterly
- **Review window:** 14 days
- **Justification:** Required
- **Notifications and reminders:** Enabled

![External access review created](07-ns2-external-access-review-created.png)

Because Lori Van Meter owns the NS2 project group, the resource-owner model assigns responsibility for external access certification to the business owner rather than permanently tying the review to an IAM administrator.

The active review identified one guest identity requiring certification.

![Active external access review](08-ns2-access-review-active.png)

---

## Access Certification and Remediation

The Access Review evaluates whether Dr. Jamil should continue to retain membership in the Ninja Sleeper II project group.

Entra provides the reviewer with decision-support information, but the business owner remains responsible for determining whether a legitimate business requirement still exists.

The active review identified Dr. Jamil as the external identity awaiting certification and generated a recommended action for the reviewer.

![Jamil access review pending](09-ns2-jamil-review-pending.png)

The review was also configured so that a denied access decision can remove the guest user's membership from the project group.

This creates a governance lifecycle in which external access is not simply granted and forgotten.

Instead, access can be:

**Granted → reviewed → justified → retained or removed**

---

## Security Design

The lab demonstrates several controls that reduce the risk associated with external collaboration.

### External identity instead of employee identity

The consultant authenticates using an external identity through Entra B2B rather than receiving an internal Vandelay employee account.

### No access by default

Successful B2B authentication does not automatically provide access to Vandelay applications or project resources.

### Project-based authorization

Access is granted through the dedicated `SG-NS2-Project` security group rather than through broad Toronto IC membership.

### Business ownership

Lori Van Meter serves as the resource owner and is accountable for determining whether external access remains appropriate.

### Recurring certification

Guest membership is reviewed quarterly rather than remaining indefinitely without validation.

### Remediation capability

A denied review decision can remove the guest's project-group membership, allowing the access certification process to affect the actual authorization state.

---

## IAM Workflow

```text
External Consultant
        ↓
Entra B2B Invitation
        ↓
External Identity Verification
        ↓
Guest Identity Created / Redeemed
        ↓
Microsoft 365 Authentication
        ↓
No Default Resource Access
        ↓
SG-NS2-Project Authorization
        ↓
Guest-Only Access Review
        ↓
Resource Owner Certification
        ↓
Retain or Remove Access
