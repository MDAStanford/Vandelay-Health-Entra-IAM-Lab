# Microsoft Entra ID Enterprise Application & SAML SSO Lab

## Overview

This lab demonstrates the configuration and management of an enterprise application in Microsoft Entra ID. The objective was to explore how Entra ID can provide centralized application access, SAML-based single sign-on (SSO), identity claims, and group-based access assignment.

The lab uses a fictional enterprise application, **Vandelay Expense Management**, to simulate an organization's expense management system.

## Objectives

* Configure an Enterprise Application in Microsoft Entra ID
* Require explicit assignment before users can access the application
* Assign individual users to an enterprise application
* Configure SAML-based Single Sign-On
* Configure SAML attributes and claims
* Map a user's department attribute into a SAML claim
* Assign application access through a Microsoft Entra group
* Demonstrate how group membership can support scalable application access management

---

## 1. Enterprise Application and User Assignment

The **Vandelay Expense Management** enterprise application was configured in Microsoft Entra ID.

A test user was assigned to the application through **Users and groups**, demonstrating direct application access assignment.

![Enterprise Application User Assignment](screenshots/01-enterprise-app-user-assignment.png)

Direct assignment can be useful when access must be granted to a specific identity, although group-based assignment is generally more scalable for larger environments.

---

## 2. Require Explicit Assignment

The application's **Assignment required?** setting was configured as **Yes**.

![Assignment Required](screenshots/02-assignment-required.png)

This restricts application access to identities that have been explicitly assigned to the enterprise application rather than allowing any user in the tenant to access it.

From an IAM perspective, this supports controlled access and the principle of least privilege.

---

## 3. Configure SAML Single Sign-On

The enterprise application was configured to use **SAML-based Single Sign-On**.

The basic SAML configuration included an:

* Identifier (Entity ID)
* Reply URL / Assertion Consumer Service (ACS) URL
* Token signing certificate

![SAML Configuration](screenshots/03-saml-configuration.png)

In this configuration, Microsoft Entra ID acts as the **Identity Provider (IdP)** and provides authentication information to the application using SAML assertions.

---

## 4. Configure SAML Attributes and Claims

SAML claims determine what identity information Entra ID sends to the application after authentication.

The application was configured with standard identity claims including:

* User Principal Name
* Email address
* Given name
* Surname

A custom **department** claim was also configured and mapped to:

`user.department`

![SAML Department Claim](screenshots/04-saml-department-claim.png)

This demonstrates how directory attributes can be included in SAML assertions and made available to an application.

---

## 5. Validate the User Attribute

The test user's Entra ID profile contains a populated **Department** attribute.

![User Department Attribute](screenshots/05-user-department-attribute.png)

Because the SAML department claim references `user.department`, the value stored in the user's Entra ID identity record can be supplied to the application as part of the SAML assertion.

This demonstrates the relationship between **identity attributes stored in the directory and claims delivered to an application**.

---

## 6. Implement Group-Based Application Assignment

Rather than managing application access exclusively through individual user assignments, the **M365-FIN-Team** group was assigned to Vandelay Expense Management.

![Group-Based Application Assignment](screenshots/06-group-based-app-assignment.png)

Group-based assignment provides a more scalable method of managing access because application access can be tied to group membership.

Users who require the application can be managed through the appropriate access group instead of individually at the application level.

---

## 7. Validate Group Membership

The Finance group contains multiple test identities representing members of the organization's Finance team.

![Finance Group Members](screenshots/07-finance-group-members.png)

This demonstrates the relationship:

**User Identity → Group Membership → Enterprise Application Assignment**

This approach supports centralized access administration and can reduce the administrative overhead associated with managing application assignments individually.

---

## IAM Concepts Demonstrated

This lab provided hands-on experience with several core identity and access management concepts:

* Enterprise application management
* Federated authentication
* SAML 2.0 Single Sign-On
* Identity Provider (IdP) configuration
* SAML assertions and claims
* Identity attribute mapping
* User-based application assignment
* Group-based application assignment
* Least-privilege access
* Centralized access management

## Security and Governance Takeaways

The lab demonstrates how authentication and authorization are related but distinct functions.

**SAML SSO** provides a federated mechanism for authenticating a user to an application, while **application assignments and group membership** determine which identities are authorized to access that application.

Using group-based application assignment provides a more scalable access-management model than maintaining large numbers of individual assignments. Identity attributes can also be passed to applications through SAML claims, allowing applications to consume identity information maintained centrally in Entra ID.

Together, these capabilities demonstrate how Microsoft Entra ID can act as a centralized identity provider and access-management layer for enterprise applications.

---

## Environment

* Microsoft Entra ID
* Microsoft Entra admin center
* Enterprise Applications
* SAML 2.0
* Microsoft Entra users and groups

> **Note:** Vandelay Expense Management and the identities shown in this lab are part of a lab environment and are used solely for demonstration purposes.
