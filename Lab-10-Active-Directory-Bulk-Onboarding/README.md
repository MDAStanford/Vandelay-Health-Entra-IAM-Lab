# Lab 10 — Integrating Employees After a Corporate Acquisition

**Vandelay Health** is a fictional healthcare technology company headquartered in Santa Monica, California and the company behind the **Ninja Sleeper** — an ultra-light, compact and virtually noiseless CPAP system designed for travelers who need to sleep comfortably in flight without disturbing fellow passengers.

The technology behind the Ninja Sleeper began as a **federal government contract project**, developed to provide military personnel in the field with a quiet and highly portable sleep-apnea solution. Vandelay Health later adapted the technology for the commercial market, incorporating as much of the original proprietary intellectual property as possible into the consumer Ninja Sleeper platform.

---

## Business Scenario

Vandelay Health has acquired a small design studio in **Toronto, Ontario, Canada**.

Unlike the employees hired directly into Vandelay's Toronto Innovation Center in earlier labs, these seven employees are joining the company through an **acquisition** and must now be incorporated into Vandelay's existing Active Directory environment.

IAM needs to bring the acquired workforce into the corporate identity structure without simply creating seven disconnected user accounts.

The acquired employees need:

- A defined organizational location in Active Directory
- Standardized identity attributes
- Appropriate departmental placement
- Consistent naming and account configuration
- Department-based security-group access
- A repeatable onboarding process
- Validation that the resulting identities and access were created correctly

Because multiple employees need to be incorporated at the same time, the acquisition also provides an opportunity to move beyond one-at-a-time account creation and use **CSV data and PowerShell to automate part of the onboarding process**.

The resulting workflow is:

**Acquisition → Organizational design → Identity source data → Bulk provisioning → Attribute configuration → Group-based access → Validation**

---

## IAM Requirements

To integrate the acquired Toronto workforce, IAM needed to:

- Establish a Toronto organizational structure in Active Directory.
- Separate Innovation Center and Operations identities using Organizational Units (OUs).
- Create seven workforce identities for the acquired employees.
- Place each identity in the appropriate OU.
- Apply standardized user attributes.
- Configure department, title, company, office, and geographic information.
- Establish manager relationships where applicable.
- Create department-based security groups.
- Assign users only to groups appropriate for their business responsibilities.
- Use structured CSV data to support repeatable bulk administration.
- Use PowerShell to reduce repetitive manual account creation.
- Validate the resulting identities, attributes, OU placement, and group memberships.

---

## Implementation

### 1. Establish the Toronto Active Directory Structure

A dedicated **Toronto** Organizational Unit was created within the `vandelay.local` Active Directory domain.

Two child OUs were created beneath Toronto:

- `IC` — Innovation Center
- `OPS` — Operations

This provides a logical directory structure for managing the acquired employees according to their organizational responsibilities.

Rather than placing the new users into a generic user container, the directory structure reflects the business organization they are joining.

---

### 2. Prepare the Acquired Workforce for Onboarding

Seven Toronto employees needed to be incorporated into Vandelay's Active Directory environment.

The acquired population consisted of:

- **6 Innovation Center employees**
- **1 Operations employee**

The Operations employee, **Shawn Rudey**, was placed within the Toronto Operations structure, while the six Innovation Center employees were placed within the Toronto IC structure.

The workforce included employees such as:

- Eric Lund
- Erik Wallace
- Jay Martin
- James Patel
- Shawn Rudey

Each identity required more than a username and password. The directory records needed enough business information to make the accounts understandable and usable for downstream identity and access administration.

---

### 3. Create the Initial Identities

Initial Toronto identities were created manually through **Active Directory Users and Computers (ADUC)**.

Manual creation provided an opportunity to validate the intended account structure, naming conventions, OU placement, and required identity information before expanding the process to the rest of the acquired workforce.

This established the expected provisioning model before introducing automation.

---

### 4. Move from Manual Provisioning to Bulk Administration

Creating each acquired employee individually through the GUI would work technically, but it would require repeating the same administrative process for every account.

A structured **CSV file** was therefore used as the identity source for bulk administration.

The CSV provided consistent workforce information that could be processed programmatically rather than re-entered manually for every employee.

PowerShell was then used to create and configure the remaining Active Directory identities.

The operating model became:

**Structured employee data → PowerShell → Active Directory identity**

This reduces repetitive administration and creates a more repeatable process for onboarding multiple employees during events such as acquisitions or organizational expansion.

---

### 5. Standardize Identity Attributes

The Toronto identities were configured with business and organizational attributes including:

- First name
- Last name
- Display name
- User Principal Name (UPN)
- Job title
- Department
- Company
- Office
- City
- State/Province
- Country
- Manager, where applicable

The accounts used the `vandelay.local` Active Directory domain and were associated with **Vandelay Worldwide** in the underlying lab configuration.

The Toronto geographic attributes were standardized as:

- **Office/City:** Toronto
- **State/Province:** Ontario
- **Country:** Canada

Consistent identity information makes the accounts more useful for administration, reporting, access decisions, automation, and future governance processes.

---

### 6. Establish Department-Based Access

Security groups were used to provide a consistent access structure for the Toronto workforce.

Relevant groups included:

- `SG-IC-Users`
- `SG-TR-Users`

Users were assigned according to their organizational requirements rather than receiving arbitrary individual access.

This creates a basic role- and organization-oriented access model:

**Employee responsibility → Department/organizational placement → Security-group membership**

Group-based administration also makes access easier to understand and maintain than individually assigning permissions directly to each employee.

---

### 7. Validate the Provisioned Identities

After provisioning, the Toronto users were reviewed in **Active Directory Users and Computers**.

Validation confirmed that:

- All seven acquired employees were present.
- Users were placed within the intended Toronto organizational structure.
- Innovation Center and Operations users were separated appropriately.
- Identity attributes were populated.
- Geographic information reflected the Toronto location.
- Department and title information were present.
- Manager relationships were configured where applicable.

The resulting directory state provided evidence that the acquisition population had been incorporated into the Vandelay Active Directory environment as intended.

---

### 8. Validate Group Membership

Group memberships were reviewed after provisioning to confirm that the new identities received the expected access structure.

The validation confirmed that the Toronto identities were associated with the appropriate security groups based on their organizational requirements.

Reviewing the resulting membership is an important final step because successful account creation alone does not prove that the employee received the correct access.

The onboarding process therefore ends with validation rather than provisioning:

**Create identity → Configure identity → Assign access → Verify identity and access**

---

## Why This Matters Operationally

Corporate acquisitions create a different IAM problem from ordinary one-at-a-time hiring.

IAM may suddenly receive an entire population of employees who need to be incorporated into the organization's directory while preserving consistent naming, attributes, organizational structure, and access.

A purely manual process can work for a small number of accounts, but it becomes increasingly repetitive and susceptible to inconsistent data entry as the population grows.

This lab demonstrates a progression from:

**Manual account creation**

to:

**Structured source data + PowerShell automation**

The important control is not simply that PowerShell can create Active Directory users. The larger objective is to establish a **repeatable identity-provisioning process based on structured workforce information**.

That same principle scales beyond seven employees. The size of the input population can change while the basic workflow remains:

**Receive authoritative workforce data → Process identities consistently → Apply organizational attributes → Assign appropriate access → Validate the result**

---

## Validation

The completed acquisition-onboarding process confirmed that:

- A Toronto organizational structure existed in Active Directory.
- Separate `IC` and `OPS` OUs were established.
- Seven acquired employees were provisioned.
- Six employees were associated with the Innovation Center population.
- One employee was associated with Operations.
- Initial account creation was validated manually.
- Structured CSV data was used for bulk identity administration.
- PowerShell was used to automate repetitive provisioning work.
- Business and geographic attributes were populated.
- Department and organizational information were represented in Active Directory.
- Manager relationships were configured where applicable.
- Department-based security groups were used for access administration.
- User identities and group memberships were reviewed after provisioning.

The end-to-end process can be summarized as:

**Acquisition → Design directory structure → Prepare identity data → Provision accounts → Populate attributes → Assign group access → Validate**

---

## IAM Controls Demonstrated

- **Active Directory Domain Services (AD DS)** — administer workforce identities in an on-premises directory environment.
- **Organizational Units (OUs)** — organize identities according to business and administrative structure.
- **Acquisition onboarding** — incorporate a population of employees joining through a corporate transaction.
- **Identity provisioning** — create workforce identities based on defined business requirements.
- **Bulk user administration** — process multiple identities through a structured onboarding workflow.
- **CSV-based identity administration** — use structured source data to support consistent provisioning.
- **PowerShell automation** — reduce repetitive manual account administration.
- **Identity attribute management** — maintain organizational, geographic, and workforce information.
- **Manager relationships** — represent organizational reporting relationships within the directory.
- **Security-group administration** — provide group-based access rather than relying on individual permission assignment.
- **Organizational access alignment** — associate group membership with employee business responsibilities.
- **Post-provisioning validation** — verify identity configuration and access after account creation.
- **Repeatable onboarding** — establish a process that can be reused for future workforce populations.

---

## Relationship to Earlier Labs

This lab extends Vandelay Health's identity environment into **Active Directory** while introducing a different workforce event from the company's earlier Toronto expansion.

Earlier labs demonstrated the creation and administration of cloud identities in Microsoft Entra ID, including direct onboarding into Vandelay's Toronto Innovation Center.

This lab addresses a separate business event:

**Vandelay acquires an existing Toronto workforce and must integrate those employees into its corporate Active Directory environment.**

It also advances the portfolio's automation story.

Earlier labs demonstrated individual identity administration, lifecycle changes, governance, and attribute-driven automation. Here, structured CSV data and PowerShell are used to make the **provisioning process itself more repeatable**.

---

## Key Takeaway

An acquisition is not simply a request to **create seven user accounts**.

IAM needs to translate an incoming workforce population into the organization's existing identity structure: where employees belong, how their identities should be represented, what attributes should describe them, what access they require, and how the completed work will be validated.

This lab demonstrates how Vandelay Health can combine **Active Directory organizational design, structured identity data, security groups, CSV-based administration, and PowerShell automation** to integrate an acquired workforce consistently.

The result is a repeatable IAM workflow:

**Business event → Workforce data → Identity provisioning → Organizational placement → Access assignment → Validation**
