# Lab 09 — Automating Access with Identity Attributes and Dynamic Groups

**Vandelay Health** is a fictional healthcare technology company headquartered in Santa Monica, California and the company behind the **Ninja Sleeper** — an ultra-light, compact and virtually noiseless CPAP system designed for travelers who need to sleep comfortably in flight without disturbing fellow passengers.

The technology behind the Ninja Sleeper began as a **federal government contract project**, developed to provide military personnel in the field with a quiet and highly portable sleep-apnea solution. Vandelay Health later adapted the technology for the commercial market, incorporating as much of the original proprietary intellectual property as possible into the consumer Ninja Sleeper platform.

---

## Business Scenario

Vandelay Health's identity environment was originally centered on its Santa Monica headquarters, where manually maintained group membership was manageable.

The expansion of the Toronto Innovation Center changed that.

Vandelay now has **50 workforce identities across two locations**:

- **42 employees in Santa Monica**
- **8 employees in Toronto**

As the company grows, IAM does not want location-based group membership to depend on an administrator remembering to add and remove individual employees from the correct groups every time someone is hired, transferred, or changes location.

The goal is to make **identity data itself drive group membership**.

Before automating that process, however, IAM needs confidence that the underlying location attributes are accurate and consistently populated. A dynamic rule will faithfully act on whatever data it receives — including bad data.

This is particularly important following the data-quality issues identified during Vandelay's access-certification work. Automating access from incomplete or inaccurate identity attributes could turn a single data error into an incorrect group assignment.

IAM therefore establishes a two-stage control:

1. **Standardize and validate the workforce identity data.**
2. **Use validated attributes to automate location-based group membership.**

The resulting model is:

**Business event → Identity attribute → Dynamic membership rule → Automatic group membership**

Under this model, a newly created or updated identity can qualify automatically for the appropriate location group based on its authoritative `city` attribute rather than requiring a separate manual group-assignment step.

---

## IAM Requirements

To implement attribute-driven group administration, IAM needed to:

- Standardize location attributes across the existing workforce.
- Update multiple identities efficiently through bulk administration.
- Maintain accurate Santa Monica and Toronto identity populations.
- Validate the resulting attributes at the individual-user level.
- Create dynamic security groups using authoritative identity attributes.
- Test dynamic membership rules before relying on them.
- Validate both matching and non-matching identities.
- Automatically populate groups without manually assigning individual members.
- Confirm that calculated membership matched the expected workforce populations.
- Establish a scalable model in which future identity changes can automatically affect group membership.

---

## Implementation

### 1. Standardize Workforce Identity Attributes

Location attributes were standardized across the Vandelay Health tenant using Microsoft Entra bulk administration.

The Santa Monica and Toronto populations were processed as separate identity sets.

The completed operations confirmed successful updates for:

- **42 Santa Monica identities**
- **8 Toronto identities**
- **50 total workforce identities**

This established consistent location data that could subsequently be used for automated membership decisions.

![Bulk Identity Attribute Update Success](screenshots/01-bulk-identity-attribute-update-success.png)

---

### 2. Validate the Updated Identity Data

After the bulk operation, an individual Toronto identity was reviewed to confirm that the expected organizational and geographic information had been populated correctly.

The identity showed:

- **City:** Toronto
- **Office location:** Toronto
- **State/Province:** Ontario
- **Country/Region:** Canada
- **Company:** Vandelay Health
- **Department:** Innovation Center

This validation step is important because a dynamic group can only make reliable membership decisions when the identity attributes driving its rule are accurate.

The bulk operation established consistency across the workforce, while the individual inspection provided evidence that the resulting identity data was populated as intended.

![Toronto Identity Attributes Validated](screenshots/02-toronto-identity-attributes-validated.png)

---

### 3. Create the Santa Monica Dynamic Membership Rule

A dynamic security-group rule was created using the Microsoft Entra `city` user attribute:

```text
(user.city -eq "Santa Monica")
