# Lab 09 — Identity Attributes & Dynamic Groups

## Overview

This lab demonstrates attribute-driven identity administration in Microsoft Entra ID. Identity records were standardized through bulk operations across the Vandelay Health tenant, establishing location attributes for Santa Monica and Toronto users. Dynamic security groups were then configured using city-based membership rules, allowing Entra ID to calculate group membership automatically from authoritative user attributes rather than relying on manual member assignment.

## Objectives

- Standardize identity attributes across the tenant using bulk administration
- Validate location attributes at the individual-user level
- Create dynamic security groups driven by identity attributes
- Validate positive and negative dynamic membership conditions
- Demonstrate automated group membership based on authoritative identity data

## Environment

| Component | Configuration |
|---|---|
| Platform | Microsoft Entra ID |
| Organization | Vandelay Health / Vandelay Worldwide (fictional) |
| Total workforce identities | 50 |
| Santa Monica identities | 42 |
| Toronto identities | 8 |
| Group type | Security |
| Membership type | Dynamic User |

## 1. Bulk Identity Attribute Standardization

Location attributes were standardized across the tenant using Microsoft Entra bulk administration. The Santa Monica population and Toronto population were updated as separate identity sets.

The completed operations confirmed successful updates for 42 Santa Monica users and 8 Toronto users.

![Bulk Identity Attribute Update Success](screenshots/01-bulk-identity-attribute-update-success.png)

## 2. Validate Toronto Identity Attributes

An individual Toronto identity was reviewed after the bulk operation to verify that the expected attributes were present. The record shows Toronto as the city and office location, Ontario as the province, Canada as the country/region, Vandelay Health as the company, and Innovation Center as the department.

![Toronto Identity Attributes Validated](screenshots/02-toronto-identity-attributes-validated.png)

## 3. Configure and Validate Dynamic Membership

A dynamic security-group rule was created using the `city` user attribute:

```text
(user.city -eq "Santa Monica")
```

The rule was tested against identities from both locations. A Santa Monica identity evaluated as **In group**, while a Toronto identity evaluated as **Not in group**, confirming both the positive and negative membership conditions before deployment.

![Dynamic City Rule Validation](screenshots/03-dynamic-city-rule-validation.png)

## 4. Verify Automated Group Membership

The dynamic security group `SG-SM-Users-Dynamic` automatically populated with 42 members after the rule was deployed. No manual member assignment was required.

![Santa Monica Dynamic Group Members](screenshots/04-santa-monica-dynamic-group-members.png)

A corresponding Toronto dynamic security group was also created and validated using:

```text
(user.city -eq "Toronto")
```

The Toronto rule successfully matched all 8 Toronto identities.

## Results

- Standardized location attributes across all 50 workforce identities
- Confirmed successful bulk updates for 42 Santa Monica and 8 Toronto identities
- Validated identity attributes after the bulk operation
- Created location-driven dynamic security groups
- Verified positive and negative rule evaluation
- Automatically populated `SG-SM-Users-Dynamic` with 42 qualifying identities
- Created and validated a corresponding Toronto dynamic group for 8 identities

## Skills Demonstrated

- Microsoft Entra ID Administration
- Identity Attribute Management
- Bulk User Administration
- Dynamic Security Groups
- Attribute-Based Group Membership
- Identity Data Validation
- Access Automation
- Identity Governance
- Security Group Administration
- Policy and Rule Validation

## Key Takeaway

Dynamic groups connect identity data to access administration. By standardizing authoritative user attributes and using those attributes in membership rules, Entra ID can automatically maintain security-group membership as the workforce changes, reducing manual administration and improving consistency.
