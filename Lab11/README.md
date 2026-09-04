# Vandelay Health — Geographic Access Control with Microsoft Entra Conditional Access

## Project Overview

This lab simulates an enterprise geographic access-control requirement for Vandelay Health, a fictional consumer medical-device company headquartered in Santa Monica, California.

Vandelay Health's primary competitor, Newman GmbH, is located in Switzerland. As part of the company's efforts to reduce the risk of unauthorized access, intellectual-property theft, and digital piracy, Vandelay established Switzerland as a restricted sign-in geography.

Rather than attempting to manage geographic restrictions individually at the user level, Vandelay implemented a centralized Microsoft Entra Conditional Access policy designed to prevent company identities from accessing corporate resources when sign-in activity originates from Switzerland.

The project demonstrates a practical Conditional Access workflow:

Business risk → geographic restriction → named location → organization-wide policy → access control → staged deployment → validation

> **Note:** Vandelay Health, Newman GmbH, and the business scenario in this project are fictional. The environment was created solely as a hands-on identity and access management lab.

---

## Business Scenario

Vandelay Health operates in a competitive consumer medical-device market in which product designs, intellectual property, and other proprietary information represent valuable corporate assets.

The company's primary competitor, Newman GmbH, operates from Switzerland. As part of a broader effort to mitigate the risk of digital piracy and unauthorized access to proprietary information, Vandelay's security team established Switzerland as a restricted sign-in geography.

The security requirement was:

**Vandelay corporate identities should not be permitted to access company resources when sign-in activity originates from Switzerland.**

The implementation needed to:

- Define Switzerland as a named geographic location in Microsoft Entra ID.
- Apply the restriction across Vandelay's user population.
- Protect all resources covered by Conditional Access.
- Block access when the geographic condition is met.
- Protect administrative access from accidental lockout during testing.
- Validate the policy before enabling production enforcement.

Vandelay therefore implemented the requirement through a centralized Microsoft Entra Conditional Access policy rather than making access changes to individual identities.

---

## Environment

- Microsoft Entra ID
- Microsoft Entra Conditional Access
- Microsoft Entra Named Locations
- Microsoft 365 test tenant
- Fictional Vandelay Health identity environment

---

## Implementation

### 1. Defined Switzerland as a Named Location

A named geographic location was created in Microsoft Entra Conditional Access:

**Switzerland - Blocked Location**

Switzerland was selected as the country associated with the location.

This named location provides the geographic condition used by the Conditional Access policy.

---

### 2. Created the Conditional Access Policy

A Conditional Access policy was created:

**Lab 11 - Block Sign-ins from Switzerland**

The policy translates Vandelay's geographic security requirement into a centralized identity access control.

---

### 3. Applied the Policy Across the Organization

The Conditional Access policy was configured with:

- **Users:** All users
- **Target resources:** All resources
- **Network/location:** Switzerland - Blocked Location
- **Grant control:** Block access

Using **All users** allows the geographic restriction to apply across Vandelay's user population without requiring individual account modifications.

New and existing users covered by the policy can therefore be governed by the same centralized access rule.

---

### 4. Added an Administrative Safety Exclusion

The lab administrator account was explicitly excluded from the Conditional Access policy.

This provides a safeguard against accidental administrative lockout while the organization-wide policy is being tested and validated.

The exclusion demonstrates an important operational consideration when deploying Conditional Access controls: security policies must protect corporate resources without eliminating the organization's ability to administer or recover the identity environment.

The resulting user assignment is:

**All users → Exclude designated administrator account**

---

### 5. Configured Geographic Access Enforcement

The policy evaluates the network/location associated with the sign-in attempt.

When a covered Vandelay identity attempts to access corporate resources from the named Switzerland location, the policy is designed to apply:

**Block access**

The policy does not specifically identify or block Newman GmbH. Instead, Vandelay has chosen Switzerland as a restricted geographic location based on its business-risk assessment.

The resulting control logic is:

**Covered Vandelay identity  
→ Sign-in originates from Switzerland  
→ Corporate resource requested  
→ Block access**

---

### 6. Deployed the Policy in Report-Only Mode

Rather than immediately enabling the policy for production enforcement, the Conditional Access policy was configured in:

**Report-only**

Report-only mode allows Vandelay to evaluate how the policy would affect sign-in activity before enforcing the restriction.

This provides an opportunity to identify unintended consequences, confirm the scope of the policy, and validate exclusions before users are denied access.

The deployment approach is:

**Configure → Observe → Validate → Enforce**

This staged approach reduces the risk of introducing an organization-wide access policy without first understanding its operational impact.

---

## Result

Vandelay Health successfully configured an organization-wide Microsoft Entra Conditional Access control designed to prevent covered corporate identities from accessing company resources when sign-in activity originates from Switzerland.

The completed configuration demonstrates:

- Centralized Conditional Access administration
- Geographic access restrictions
- Organization-wide user targeting
- Named location configuration
- All-resource protection
- Administrative lockout safeguards
- Block-access controls
- Report-only testing
- Risk-aware security deployment
- Translation of a business-security requirement into an identity control

The policy remains intentionally in **Report-only mode**.

As a result, Microsoft Entra can evaluate how the Conditional Access policy would affect applicable sign-ins without currently enforcing the access denial.

Following successful validation, the policy could be moved from:

**Report-only → On**

to enforce the geographic restriction.

---

## Security and IAM Concepts Demonstrated

This lab demonstrates several concepts used in enterprise Identity and Access Management:

- Conditional Access
- Geographic access controls
- Named locations
- Policy-based access management
- Identity security governance
- Organization-wide identity controls
- Administrative account protection
- Access-policy scoping
- Security exception management
- Access-control testing and validation
- Risk-based security decisions
- Staged security-control deployment

---

## Business and Security Rationale

Conditional Access provides a mechanism for translating organizational security requirements into centrally managed identity controls.

In this scenario, Vandelay identified a business risk associated with sign-in activity originating from Switzerland because its primary competitor, Newman GmbH, operates there.

The IAM response was not to modify dozens of individual user accounts. Instead, the organization created a single centralized Conditional Access policy capable of governing the applicable user population and corporate resources.

This illustrates the relationship between:

**Business risk → Security requirement → IAM policy → Technical control**

The lab also demonstrates that implementing a security control involves more than simply enabling a blocking rule.

The administrator exclusion and Report-only deployment provide safeguards intended to reduce operational risk while the control is validated.

---

## Screenshots

The project screenshots document the creation, configuration, and validation of the geographic Conditional Access control.

### Screenshot 01
Creation and configuration of the Switzerland named location.

### Screenshot 02
Switzerland selected as the geographic location associated with the access restriction.

### Screenshot 03
Conditional Access policy configuration and assignment.

### Screenshot 04
Policy scope and access-control configuration.

### Screenshot 05
Completed **Lab 11 - Block Sign-ins from Switzerland** policy showing:

- Report-only status
- All-user scope
- All-resource scope
- Geographic condition
- Block-access control

### Screenshot 06
Administrator account exclusion demonstrating protection against accidental tenant lockout.

### Screenshot 07
Network assignment showing:

**Switzerland - Blocked Location**

as the named location included in the Conditional Access policy.

---

## Key Takeaway

Microsoft Entra Conditional Access allows identity teams to translate business and security requirements into centralized, scalable access controls.

In this scenario, Vandelay Health identified a geographic security risk associated with Switzerland and implemented an organization-wide Conditional Access policy designed to prevent covered identities from accessing corporate resources from that location.

Rather than immediately enforcing an untested restriction, the policy was deployed in Report-only mode with an administrative safety exclusion.

The completed workflow demonstrates:

**Identify risk → Define scope → Configure control → Protect administration → Test impact → Validate → Enforce**

This approach combines identity security with operational risk management and provides a repeatable model for deploying enterprise Conditional Access controls.
