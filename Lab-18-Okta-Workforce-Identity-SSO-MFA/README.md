# Vandelay Health — Lab 18: Okta Workforce Identity — SSO, MFA & Group-Based Access

## Project Overview

Vandelay Health is a fictional healthcare technology company whose flagship product, the Ninja Sleeper, originated from a federal government contract requiring a silent sleeping solution for military personnel operating in the field. Vandelay Health subsequently adapted the technology for commercial use while retaining as much of the original proprietary design and intellectual property as possible.

As Vandelay expands, it has acquired the third-party logistics provider (3PL) that supports warehouse operations. The acquired company already uses Okta Workforce Identity, while Vandelay's core identity environment uses Microsoft Entra ID and Active Directory. Rather than disrupting warehouse operations with an immediate platform migration, the IAM team must inherit, secure, and administer the existing Okta environment.

---

## Business Scenario

The acquired 3PL workforce requires continued access to a warehouse operations application while Vandelay establishes consistent identity and access controls.

The IAM implementation must:

- Create and organize the acquired 3PL workforce in Okta.
- Use business-role groups to manage application access.
- Configure a SAML 2.0 application integration for the warehouse portal.
- Require multi-factor authentication for application access.
- Validate first-time user onboarding and Okta Verify enrollment.
- Confirm that authorized users receive the application through group membership.
- Review Okta System Log events to validate authentication, policy evaluation, and application SSO activity.

---

## Environment

- Okta Workforce Identity
- Okta Integrator Free Plan
- Okta Universal Directory
- Okta Groups
- SAML 2.0
- Okta Authentication Policies
- Okta Verify
- Okta System Log

---

## 3PL Workforce

Eight acquired 3PL identities were created in Okta:

- Bob Gillespie — Warehouse Manager
- Ian Brown — Assistant Manager 1
- John Squire — Assistant Manager 2
- Will Lee — Inventory Manager
- Chris Elliott — Assistant Inventory Manager
- Bud Melman — Shipping & Receiving Manager
- Emily Wyatt — Foreperson
- Nick Chapman — Assistant Foreperson

The users were organized into four business-role groups:

- `3PL-Warehouse-Management`
- `3PL-Inventory`
- `3PL-Shipping-Receiving`
- `3PL-Warehouse-Operations`

This established a group-based access model rather than assigning application access individually.

---

## SAML Application Integration

A SAML 2.0 application integration was created:

**3PL Warehouse Operations Portal**

The lab configured the core SAML relationship between Okta as the Identity Provider (IdP) and the simulated warehouse application as the Service Provider (SP).

Configuration included:

- Single Sign-On / Assertion Consumer Service URL
- Audience URI / SP Entity ID
- EmailAddress Name ID format
- Okta username as the application username
- Signed SAML response and assertion
- RSA-SHA256 signature algorithm
- SHA256 digest algorithm

The SAML assertion was previewed during configuration to verify the identity information Okta would send to the service provider.

The application uses a simulated service-provider endpoint for lab purposes. The lab therefore validates Okta's SAML configuration and SSO initiation, but does **not** claim end-to-end authentication into a production third-party application.

---

## Group-Based Application Access

The 3PL Warehouse Operations Portal was assigned through the acquired workforce's business-role groups.

Bob Gillespie, for example, received the application through:

**Bob Gillespie → 3PL-Warehouse-Management → 3PL Warehouse Operations Portal**

This demonstrates scalable authorization through group membership rather than direct per-user application assignment.

---

## MFA Authentication Policy

A dedicated application sign-in policy was created:

**3PL Warehouse Operations MFA**

The policy was associated with the 3PL Warehouse Operations Portal and configured to require:

**Any 2 factor types**

The policy supports factors including password and Okta Verify.

This separates application assignment from authentication requirements:

**Group membership determines whether the user receives the application.**

**The authentication policy determines how strongly the user must authenticate to access it.**

---

## User-Side Validation

Bob Gillespie was used as the validation identity.

His first sign-in demonstrated the onboarding sequence:

1. Sign in using the assigned Okta username.
2. Replace the administrator-issued one-time password.
3. Enroll Okta Verify as a security method.
4. Complete authentication.
5. Reach the Okta Dashboard.
6. Confirm the 3PL Warehouse Operations Portal is available through group-based assignment.
7. Initiate the application's SAML SSO flow.

The test confirmed that the identity, group assignment, application assignment, and MFA requirements worked together from the user's perspective.

---

## System Log Validation

Okta System Log events were reviewed after the user-side test.

The log recorded Bob Gillespie's activity, including:

- User login to Okta — **SUCCESS**
- Verify user identity — **SUCCESS**
- Password and Okta Verify authentication methods
- Evaluation of sign-on policy — **ALLOW**
- User single sign on to the 3PL Warehouse Operations Portal — **SUCCESS**

This provided auditable evidence that the configured authentication and application-access controls were evaluated during the test.

---

## IAM Concepts Demonstrated

- Workforce identity administration
- User and group management
- Group-based application assignment
- SAML 2.0 federation concepts
- Identity Provider (IdP) and Service Provider (SP) roles
- Assertion Consumer Service (ACS) and Audience URI / Entity ID
- Multi-factor authentication
- Okta Verify enrollment
- Application sign-in policies
- First-login password lifecycle
- User-side access validation
- Okta System Log investigation
- Authentication and SSO event validation

---

## Evidence

- **Lab18-01** — SAML application configuration / assertion validation
- **Lab18-02** — MFA policy associated with 3PL Warehouse Operations Portal
- **Lab18-03** — Group-based application assignments
- **Lab18-04** — MFA two-factor rule
- **Lab18-05** — Bob Gillespie group-based application access
- **Lab18-06** — Bob Gillespie Okta Verify enrollment requirement
- **Lab18-07** — Bob Gillespie Okta Dashboard with assigned 3PL application
- **Lab18-08** — Bob Gillespie MFA and SSO System Log validation

No passwords, QR enrollment codes, recovery secrets, or authentication secrets are included in the repository evidence.

---

## Outcome

Vandelay Health successfully inherited and secured the acquired 3PL workforce's Okta environment by establishing role-based groups, group-based application access, a SAML 2.0 application integration, and application-specific MFA requirements.

The implementation was validated from both the administrator and user perspectives. Bob Gillespie completed first-login password setup, enrolled Okta Verify, authenticated successfully, received the warehouse portal through group membership, and initiated SAML SSO. Okta System Log events provided audit evidence of successful authentication, policy evaluation, and application SSO activity.

This lab demonstrates practical Okta Workforce Identity administration while extending the Vandelay Health IAM portfolio beyond Microsoft Entra ID and Active Directory.
