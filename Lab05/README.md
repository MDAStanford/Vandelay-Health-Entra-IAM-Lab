# Lab 05 – Joiner & Mover Lifecycle Management: Organizational Change and Toronto Expansion

## Objective

The objective of this lab was to simulate two common identity lifecycle events in Microsoft Entra ID: an internal organizational move and the onboarding of a new office.

The lab demonstrates how identity attributes, manager relationships, group membership, business ownership, and access validation work together during Joiner-Mover-Leaver (JML) administration.

## Scenario

Vandelay Worldwide underwent two simultaneous business changes.

First, Travel was separated from Human Resources and established as its own department. Existing employees Tuba Aksoy and Suzi Tarkanian needed to be moved from HR into the new Travel organization, with their identity records, reporting relationships, and access aligned to their new responsibilities.

Tuba was promoted from Travel Coordinator to Director - Travel and became the department lead. Suzi remained a Travel Coordinator and moved under Tuba's management.

At the same time, Vandelay opened a new Innovation Center in Toronto, Ontario. Six new workforce identities were onboarded and required consistent organizational attributes, manager relationships, baseline security access, and Microsoft 365 collaboration access.

The IAM goal was to support both changes while maintaining least privilege, accurate identity data, appropriate business ownership, and traceable access assignments.

## Part 1 – Mover Event: Creating the Travel Department

Travel initially operated within Human Resources. The organizational change required existing identities to be updated rather than creating new accounts.

### Tuba Aksoy

Before the move, Tuba was configured as a Travel Coordinator in Human Resources and reported to the CHRO.

After the move, her identity was updated to reflect:

- Job title: `Director - Travel`
- Department: `Travel`
- Office location: `Santa Monica`
- Manager: `Rebecca Lewis (CHRO)`

This preserved Tuba's existing identity while aligning her attributes with her new business role.

### Suzi Tarkanian

Before the move, Suzi was a Travel Coordinator in Human Resources and reported to the HR Manager.

After the move, her identity was updated to reflect:

- Job title: `Travel Coordinator`
- Department: `Travel`
- Office location: `Santa Monica`
- Manager: `Tuba Aksoy`

The change demonstrates a typical mover workflow in which an employee's identity persists while organizational attributes, reporting relationships, and access requirements change.

### Travel Access Structure

New Travel groups were created to support the department:

- `SG-TR-Users` – security and access assignments
- `M365-TR-Team` – Microsoft 365 collaboration resources

This created a dedicated access structure for the new department rather than continuing to rely on Human Resources groups.

The mover lifecycle can be summarized as:

**Business change → identity attribute update → manager update → access reassessment → new departmental access**

## Part 2 – Joiner Event: Toronto Innovation Center

Vandelay simultaneously opened a new Innovation Center in Toronto, Ontario, Canada.

Six workforce identities were created for the new location. Each identity was configured with business context such as job title, department, office location, geographic information, manager relationship, and account status.

The Innovation Center workforce included a local leader and additional employees reporting into the new organization.

Creating the identities first established the authoritative business attributes needed to make appropriate access decisions.

## Part 3 – Toronto Access Groups

Two baseline groups were created for Innovation Center employees.

### SG-IC-Users

`SG-IC-Users` is a Microsoft Entra Security group.

**Purpose:** All Innovation Center employees. Used for Innovation Center application access and department-based security assignments.

The group provides a reusable authorization boundary for security and application access associated with the Innovation Center.

### M365-IC-Team

`M365-IC-Team` is a Microsoft 365 group.

**Purpose:** All Innovation Center employees. Used for Innovation Center collaboration, shared resources, and Microsoft 365 services.

The group supports collaboration resources separately from security authorization.

Using separate group types reinforces an important design principle:

**Security groups manage authorization; Microsoft 365 groups support collaboration.**

Appropriate business owners were assigned to the groups rather than retaining unnecessary standing ownership with the IAM administrator.

## Part 4 – Joiner Provisioning and Validation

The Toronto employees were provisioned into the Innovation Center baseline access structure.

For a standard Innovation Center employee, the baseline assignment was:

**Innovation Center employee → `SG-IC-Users` + `M365-IC-Team`**

Jay Martin, Senior Innovation Designer, was selected as the representative joiner for post-provisioning validation.

His identity record was reviewed to confirm that the business attributes reflected his role and location, including:

- Job title: `Senior Innovation Designer`
- Department: `Innovation Center`
- Office location: `Toronto`
- Employee type: `Employee`
- Manager: `Lori Van Meter`
- Account enabled: `Yes`

Jay's group memberships were then reviewed independently. His account showed membership in:

- `SG-IC-Users`
- `M365-IC-Team`

No unrelated group memberships were present.

This connected the employee's business identity to the access actually provisioned and demonstrated that access changes should be verified rather than assumed successful.

The joiner lifecycle can be summarized as:

**Joiner request → identity creation → attribute assignment → manager relationship → baseline access provisioning → access validation**

## Governance and IAM Takeaways

This lab demonstrates that JML administration is more than creating or editing user accounts. Effective lifecycle management requires maintaining the relationship between identity data, business role, access, ownership, and validation.

The Travel restructuring illustrates why mover events require access reassessment. Without this control, employees can accumulate permissions from previous roles and create access sprawl over time.

The Toronto expansion illustrates how a repeatable joiner process can establish consistent identity attributes and baseline access for a new workforce population.

Key principles demonstrated include:

- **Least privilege** – users receive access appropriate to their current responsibilities.
- **Lifecycle governance** – access and identity attributes change when the business role changes.
- **Business ownership** – access structures are owned by appropriate business stakeholders.
- **Separation of purpose** – Security groups and Microsoft 365 groups serve different functions.
- **Identity data quality** – accurate attributes and manager relationships support reliable access decisions.
- **Access validation** – resulting assignments are reviewed after provisioning.

## Skills Demonstrated

- Microsoft Entra ID administration
- Joiner-Mover-Leaver (JML) lifecycle management
- User provisioning and identity maintenance
- Organizational attribute management
- Manager hierarchy configuration
- Security group administration
- Microsoft 365 group administration
- Access provisioning
- Access validation
- Least privilege
- Identity governance
- Business ownership and accountability

## Screenshots

### 1. Tuba Aksoy – Before Mover Event

![Tuba Aksoy before mover event](01-tuba-before-mover.png)

### 2. Tuba Aksoy – After Mover Event

![Tuba Aksoy after mover event](02-tuba-after-mover.png)

### 3. Suzi Tarkanian – Before Mover Event

![Suzi Tarkanian before mover event](03-suzi-before-mover.png)

### 4. Suzi Tarkanian – After Mover Event

![Suzi Tarkanian after mover event](04-suzi-after-mover.png)

### 5. Travel Groups Created

![Travel groups created](05-travel-groups-created.png)

### 6. Toronto Operations Manager Created

![Toronto operations manager created](06-toronto-operations-manager-created.png)

### 7. Toronto Innovation Center Users Created

![Toronto Innovation Center users created](07-toronto-innovation-center-users-created.png)

### 8. Innovation Center Security Group

![SG-IC-Users security group](08-sg-ic-users-security-group.png)

### 9. Innovation Center Microsoft 365 Group

![M365-IC-Team group](09-m365-ic-team-group.png)

### 10. Toronto Joiner Identity Validation

![Jay Martin properties](10-toronto-joiner-jay-martin-properties.png)

### 11. Toronto Joiner Group Membership Validation

![Jay Martin group memberships](11-toronto-joiner-jay-martin-group-memberships.png)

---

> **Lab Environment Notice:** Vandelay Worldwide, Vandelay Health, and all employees, organizational structures, employee data, access assignments, and business scenarios represented in this lab are fictional and were created solely for hands-on IAM training and portfolio demonstration.
