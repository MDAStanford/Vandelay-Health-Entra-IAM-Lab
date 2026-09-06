# Lab 10 — Integrating Employees After a Corporate Acquisition

**Vandelay Health** is a fictional healthcare technology company headquartered in Santa Monica, California and the company behind the **Ninja Sleeper** — an ultra-light, compact and virtually noiseless CPAP system designed for travelers who need to sleep comfortably in flight without disturbing fellow passengers.

The technology behind the Ninja Sleeper began as a **federal government contract project**, developed to provide military personnel in the field with a quiet and highly portable sleep-apnea solution. Vandelay Health later adapted the technology for the commercial market, incorporating as much of the original proprietary intellectual property as possible into the consumer Ninja Sleeper platform.

---

## Business Scenario

Vandelay Health has acquired a small design studio in **Toronto, Canada**, bringing seven employees into the company's Active Directory environment.

IAM needs to incorporate the acquired workforce efficiently while maintaining consistent identity data and ensuring that access reflects each employee's actual department.

Rather than creating and configuring every account manually, the onboarding process uses **structured CSV data and PowerShell** for bulk administration, followed by Active Directory validation and remediation of incorrect group assignments.

The workflow is:

**Acquisition → Bulk provisioning → Identity attributes → Department-based access → Validation → Remediation**

---

## IAM Requirements

IAM needed to:

- Establish a dedicated Toronto structure in Active Directory.
- Provision seven acquired employee identities.
- Standardize business and geographic identity attributes.
- Use CSV and PowerShell to reduce repetitive administration.
- Create department-based Toronto security groups.
- Assign employees according to their business roles.
- Identify and correct inaccurate group membership.
- Validate the final identity and access configuration.

---

## Implementation

### 1. Provision the Toronto Workforce

A dedicated Toronto Organizational Unit was established in `vandelay.local` with separate containers for users, groups, and computers.

Seven acquired employees were provisioned into the Toronto Users OU:

- Eric Lund
- Erik Wallace
- Jay Martin
- Lisa Brock
- Lori Van Meter
- Paul Merson
- Shawn Rudey

![Toronto Bulk Users](screenshots/01-Toronto-Bulk-Users-ADUC.png)

---

### 2. Standardize Identity Attributes

A structured CSV file was used to populate workforce attributes including title, department, company, office, city, province, and country.

PowerShell imported the data and updated the corresponding Active Directory user objects.

The resulting attributes were then queried to verify that the bulk operation succeeded.

![Bulk AD Attribute Update and PowerShell Verification](screenshots/02-Bulk-AD-Attribute-Update-PowerShell-Verification.png)

The same information was independently reviewed in Active Directory Users and Computers.

For example, Eric Lund was configured as a **Systems Analyst** in **Information Technology**.

![ADUC Attribute Verification](screenshots/03-ADUC-Attribute-Verification.png)

---

### 3. Create Department-Based Security Groups

Global Security Groups were created in the Toronto Groups OU for the departments represented by the acquired workforce:

- `SG-TOR-Finance`
- `SG-TOR-HR`
- `SG-TOR-IT`
- `SG-TOR-Operations`

![Toronto Security Groups](screenshots/04-Toronto-Security-Groups-ADUC.png)

This separates the employee's directory location from the access structure associated with the employee's business function.

---

### 4. Assign Access from Employee Attributes

PowerShell was used to assign Toronto employees to security groups according to their department.

The resulting memberships were queried to verify the initial access state.

![Toronto Group Membership Verification](screenshots/05-Toronto-Group-Membership-Verification.png)

The Toronto user population was also reviewed in ADUC to confirm that all seven acquired identities remained present within the expected organizational structure.

![Toronto Users OU](screenshots/06-toronto-users-ou.png)

---

### 5. Identify and Remediate an Access Exception

Validation identified an incorrect access state in `SG-TOR-Operations`.

The group contained:

- Shawn Rudey
- Jay Martin
- Paul Merson

Jay Martin and Paul Merson did not require Operations membership and were removed with PowerShell.

The group was then queried again, confirming that only Shawn Rudey remained.

![Toronto Operations Membership Validation](screenshots/08-toronto-operations-membership-validation.png)

This demonstrates an important part of bulk onboarding: **automation must still be validated**. A successful script execution does not necessarily mean that every resulting access assignment is correct.

---

### 6. Verify Final Group Membership

Final membership was reviewed directly in Active Directory Users and Computers.

The Innovation Center access population contained the six expected employees:

![Innovation Center Group Membership](screenshots/09-sg-tor-ic-users-membership.png)

Toronto Operations contained only Shawn Rudey:

![Operations Group Membership](screenshots/10-sg-tor-operations-membership.png)

The final validation confirmed that inappropriate Operations access had been removed while legitimate access remained intact.

---

## Validation

The completed acquisition onboarding confirmed that:

- Seven acquired employees were incorporated into Active Directory.
- A dedicated Toronto OU structure was established.
- Identity attributes were populated through CSV-driven PowerShell administration.
- User attributes were verified through both PowerShell and ADUC.
- Department-based Toronto security groups were created.
- Group membership was assigned and reviewed.
- Incorrect Operations access was identified and remediated.
- Final access was independently validated in ADUC.

The completed process can be summarized as:

**Employee data → Identity provisioning → Standardized attributes → Group-based access → Validation → Remediation → Final verification**

---

## IAM Controls Demonstrated

- **Active Directory Domain Services (AD DS)**
- **Organizational Unit design**
- **Acquisition onboarding**
- **Bulk identity provisioning**
- **CSV-driven identity administration**
- **PowerShell automation**
- **Identity attribute management**
- **Department-based security groups**
- **Group membership administration**
- **Least privilege**
- **Access remediation**
- **Post-provisioning validation**

---

## Key Takeaway

Bulk onboarding is not complete when the accounts have been created.

IAM must ensure that the resulting identities contain accurate business data, receive appropriate access, and do not retain access that their roles do not justify.

In this lab, Vandelay Health moved an acquired workforce from **structured employee data to provisioned Active Directory identities, department-based access, validation, remediation, and final verification**.
