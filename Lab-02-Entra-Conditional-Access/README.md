# Lab 02 — Protecting Vandelay Health with Conditional Access and MFA

**Vandelay Health** is a fictional healthcare technology company headquartered in Santa Monica, California and the company behind the **Ninja Sleeper** — an ultra-light, compact and virtually noiseless CPAP system designed for travelers who need to sleep comfortably in flight without disturbing fellow passengers.

The technology behind the Ninja Sleeper began as a **federal government contract project**, developed to provide military personnel in the field with a quiet and highly portable sleep-apnea solution. Vandelay Health later adapted the technology for the commercial market, incorporating as much of the original proprietary intellectual property as possible into the consumer Ninja Sleeper platform.

---

## Business Scenario

Vandelay Health employees use cloud identities to access company resources, including information associated with the Ninja Sleeper and other proprietary business operations. A compromised password could therefore provide an unauthorized user with access to sensitive Vandelay resources.

IAM has been asked to strengthen workforce authentication by requiring **multifactor authentication (MFA)** rather than relying on passwords alone.

Because an incorrectly configured Conditional Access policy can also prevent legitimate users or administrators from signing in, the new control must be introduced carefully. Vandelay will first evaluate the policy in **Report-only mode**, maintain emergency administrative access outside the policy scope, and validate authentication behavior before considering enforcement.

---

## IAM Requirements

To strengthen Vandelay Health's authentication controls, IAM needed to:

- Require multifactor authentication for workforce sign-ins through Microsoft Entra Conditional Access.
- Apply the control broadly rather than configuring MFA independently for individual employees.
- Maintain emergency access through the dedicated Break Glass administrator account.
- Exclude designated administrative access from the initial policy scope to reduce lockout risk during testing.
- Deploy the Conditional Access policy in Report-only mode before enforcement.
- Register an authentication method for a test identity.
- Perform a test sign-in and review Microsoft Entra sign-in logs to validate authentication activity.

- ---

## Implementation

### 1. Confirm the Microsoft Entra Environment

The Conditional Access control was implemented in Vandelay Health's Microsoft Entra ID Premium P2 environment, building on the workforce identity foundation established in Lab 01.

![Tenant Overview](01-Tenant-Overview.png)

---

### 2. Select a Workforce Identity for Validation

John Smith was selected as the test identity for validating authentication configuration and Conditional Access behavior.

Using a defined test identity allows the policy configuration and authentication process to be evaluated before Vandelay considers broader enforcement.

![John Smith User](02-John-Smith-User.png)

---

### 3. Configure an MFA Authentication Method

Microsoft Authenticator was registered as an authentication method for the test identity.

This provides an additional authentication factor beyond the user's password and establishes the authentication capability required by the proposed Conditional Access control.

![Authentication Methods](03-Authentication-Methods.png)

---

### 4. Create the Conditional Access Policy

A Microsoft Entra Conditional Access policy was configured to require multifactor authentication for users within the policy scope.

The dedicated Break Glass identity and designated administrative account were excluded during initial testing to reduce the risk that a policy configuration error could prevent administrative access to the tenant.

Rather than immediately enforcing the control, the policy was placed in **Report-only mode**. This allows IAM to evaluate how the policy would affect sign-ins before enabling enforcement across the environment.

![Conditional Access Policy](04-Conditional-Access-Policy.png)

---

### 5. Validate Authentication Activity

A sign-in was performed using the test identity and Microsoft Entra sign-in logs were reviewed to verify the resulting authentication activity.

The sign-in evidence provides IAM with a record that can be used alongside the Report-only Conditional Access results to evaluate the proposed control before enforcement.

![Successful Sign-in Verification](05-Successful-Sign-In.png)

---

## Validation

The completed configuration was reviewed to confirm that:

- Microsoft Authenticator was registered for the test identity.
- The Conditional Access policy required multifactor authentication for identities within its scope.
- The Break Glass and designated administrative identities were excluded from the initial policy scope.
- The policy remained in Report-only mode during evaluation rather than being immediately enforced.
- Sign-in activity for the test identity was successfully recorded in Microsoft Entra sign-in logs.

The configuration demonstrates how Vandelay can introduce stronger authentication controls while evaluating policy impact and preserving emergency administrative access.

---

## IAM Controls Demonstrated

- **Multifactor authentication (MFA)** — strengthen authentication beyond a password alone.
- **Conditional Access** — apply authentication requirements through centralized identity policy.
- **Broad policy scoping** — protect workforce identities through policy rather than user-by-user configuration.
- **Emergency access protection** — preserve a path to tenant administration if normal access is disrupted.
- **Report-only deployment** — evaluate policy impact before enforcement.
- **Authentication method administration** — register and validate Microsoft Authenticator for a workforce identity.
- **Sign-in monitoring** — use Microsoft Entra sign-in logs to validate authentication activity.
- **Access validation** — verify policy configuration and authentication behavior before broader deployment.

---

## Key Takeaway

Strong authentication is important, but so is deploying it safely.

This lab demonstrates how Vandelay Health can use **Conditional Access and MFA to reduce the risk of password-based account compromise while using Report-only evaluation, administrative exclusions, emergency access, and sign-in evidence to reduce the risk of disrupting legitimate access**.

