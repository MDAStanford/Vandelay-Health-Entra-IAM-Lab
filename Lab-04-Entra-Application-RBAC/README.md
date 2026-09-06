# Lab 04 — Giving Users the Right Level of Application Access

**Vandelay Health** is a fictional healthcare technology company headquartered in Santa Monica, California and the company behind the **Ninja Sleeper** — an ultra-light, compact and virtually noiseless CPAP system designed for travelers who need to sleep comfortably in flight without disturbing fellow passengers.

The technology behind the Ninja Sleeper began as a **federal government contract project**, developed to provide military personnel in the field with a quiet and highly portable sleep-apnea solution. Vandelay Health later adapted the technology for the commercial market, incorporating as much of the original proprietary intellectual property as possible into the consumer Ninja Sleeper platform.

---

## Business Scenario

As Vandelay Health introduces internal applications to support its growing business, simply determining whether an employee can access an application is not always sufficient. Different users may require different levels of authorization based on their responsibilities.

Jarvis Miller, an executive assistant, needs access to a custom internal Vandelay application to support his business responsibilities. His work requires him to view information in the application, but he does not need administrative or elevated capabilities.

IAM therefore needs to provide Jarvis with **read-only application access without granting unnecessary privilege**.

---

## IAM Requirements

To provide Jarvis with appropriate access while maintaining least privilege, IAM needed to:

- Register the internal application in Microsoft Entra ID.
- Understand the relationship between the App Registration and its Enterprise Application.
- Define a specific read-only application role.
- Assign Jarvis only the role required for his business responsibilities.
- Avoid granting broader application or administrative privilege.
- Validate the resulting assignment from both the application and user perspectives.

---

## Implementation

### 1. Register the Internal Application

The custom `Lab04-IAM-App` application was registered in Microsoft Entra ID as a single-tenant application.

The App Registration establishes the application's identity and configuration within Microsoft Entra ID, including its unique application and object identifiers.

![Application Registration Overview](screenshot%201%20-%20application%20registration%20overview.png)

---

### 2. Define a Read-Only Application Role

A custom application role named `Lab Reader` was created for users who require access to the application without elevated capabilities.

Creating a defined role allows Vandelay to grant access according to the user's business responsibilities rather than providing unnecessarily broad permissions.

![Application Role Configuration](screenshot%202%20-%20application%20role%20configuration.png)

---

### 3. Identify the Enterprise Application

The corresponding Enterprise Application created in the Vandelay tenant was reviewed.

The **App Registration** represents the application's identity and configuration definition, while the **Enterprise Application** represents the service principal through which the application is managed within the tenant.

![Enterprise Application Service Principal](screenshot%203%20-%20enterprise%20application%20service%20principal.png)

---

### 4. Assign the Appropriate Application Role

Jarvis Miller was assigned to the Enterprise Application using the `Lab Reader` role.

This gives Jarvis the application access required for his responsibilities while limiting his authorization to the defined read-only role.

![User Application Role Assignment](screenshot%204%20-%20user%20application%20role%20assignment.png)

---

### 5. Validate the Access Assignment

The role assignment was validated from both sides of the identity relationship.

Within the Enterprise Application, Jarvis appeared as an assigned user with the `Lab Reader` role.

Jarvis's Microsoft Entra identity was then independently reviewed to confirm that `Lab04-IAM-App` appeared among his assigned applications with the same role.

![User Application Access Verification](screenshot%205%20-%20user%20application%20access%20verification.png)

---

## Validation

The completed configuration was reviewed to confirm that:

- `Lab04-IAM-App` was registered in Microsoft Entra ID.
- A corresponding Enterprise Application/service principal existed in the tenant.
- The `Lab Reader` application role was defined.
- Jarvis Miller was assigned the `Lab Reader` role.
- Jarvis did not require broader administrative privilege to perform his intended function.
- The assignment could be independently verified from both the application and user perspectives.

---

## IAM Controls Demonstrated

- **Application identity management** — represent a custom application within Microsoft Entra ID.
- **Service principal administration** — manage the application's tenant-specific Enterprise Application.
- **Application RBAC** — define different authorization levels through application roles.
- **Least privilege** — provide only the level of application access required by the user's responsibilities.
- **Role assignment** — connect a workforce identity to a defined application role.
- **Separation of access and privilege** — application access does not require administrative authority.
- **Access validation** — independently verify an entitlement from both the resource and identity perspectives.

---

## Key Takeaway

Giving someone access to an application does not mean giving them unrestricted authority within it.

This lab demonstrates how Vandelay Health can use **Microsoft Entra application roles and role-based access control to give an employee the specific level of application access required for the job while avoiding unnecessary privilege**.
