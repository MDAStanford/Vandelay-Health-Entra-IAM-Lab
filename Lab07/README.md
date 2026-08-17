# Lab 07 — Access Certification Data Validation & Entitlement Remediation

## Overview

This lab simulates a periodic User Access Review (UAR) / access certification workflow in Microsoft Entra ID.

The objective is to demonstrate two controls that are critical to a defensible access certification process:

1. **Identity data must be complete and accurate before certification begins.**
2. **Access that cannot be justified by business need must be remediated and verified.**

The scenario uses the Vandelay Health Toronto environment created in earlier labs.

> **Lab scope:** This is a manually simulated certification workflow using Microsoft Entra ID identity and group data. It does not represent execution of a native Entra Access Review campaign.

---

## Business Scenario

Vandelay Health is preparing for a periodic access certification. Before reviewers can make reliable access decisions, IAM must validate the identity and entitlement data being presented for review.

During pre-certification validation, two issues are identified:

- **Erik Wallace**, Senior Project Manager in the Innovation Center, has no manager populated in his identity record.
- **Daniel Cho**, a Financial Analyst, appears in the `SG-IC-Users` Innovation Center security group even though his identity attributes place him in Finance.

The first is an **identity-data quality issue** that can affect reviewer assignment and certification context. The second is an **entitlement exception** requiring investigation and remediation.

---

## Lab Objectives

- Validate identity attributes before an access certification.
- Identify incomplete reviewer/manager data.
- Correct identity data needed to support certification.
- Compare identity attributes with assigned entitlements.
- Identify and investigate an access exception.
- Remove inappropriate group access.
- Verify remediation while preserving legitimate access.
- Produce evidence supporting an auditable certification process.

---

## Environment

**Platform:** Microsoft Entra ID  
**Organization:** Vandelay Health  
**Location:** Toronto, Ontario, Canada

### Identities

| Identity | Role | Department | Manager / Review Context |
|---|---|---|---|
| Daniel Cho | Financial Analyst | Finance | James Patel (CFO) |
| Erik Wallace | Senior Project Manager | Innovation Center | Lori Van Meter after remediation |

### Relevant Groups

- `SG-FIN-Users`
- `M365-FIN-Team`
- `SG-IC-Users`

---

## Workflow

### 1. Establish Daniel Cho's Expected Access

Daniel Cho is provisioned as a **Financial Analyst** in **Finance**. His manager is **James Patel (CFO)**, and his expected assignments are `M365-FIN-Team` and `SG-FIN-Users`.

This establishes the business context against which Daniel's access can later be evaluated.

![Daniel Cho clean identity provisioning](01-daniel-cho-clean-identity-provisioning.png)

---

### 2. Perform Pre-Certification Identity-Data Validation

Before beginning the access review, identity records are checked for completeness.

Erik Wallace is correctly identified as a **Senior Project Manager** in the **Innovation Center**, but his **Manager** field is blank.

This is a data-quality exception. Manager information can be important to determining the appropriate reviewer and providing business context during an access certification.

![Pre-certification missing manager](02-pre-certification-missing-manager.png)

---

### 3. Remediate the Identity-Data Exception

Erik Wallace's manager relationship is corrected by assigning **Lori Van Meter** as his manager.

The identity record now contains the management information needed to support a reliable review.

![Manager data remediated](03-manager-data-remediated.png)

---

### 4. Identify an Entitlement Exception

The membership of `SG-IC-Users` is reviewed.

Daniel Cho appears in the Innovation Center security group even though he is a Finance employee.

This is treated as an entitlement exception requiring validation rather than automatically assuming that the access is legitimate.

![Entitlement data exception](04-entitlement-data-exception.png)

---

### 5. Validate Daniel Cho's Identity and Business Context

Daniel's identity record confirms:

- **Job title:** Financial Analyst
- **Department:** Finance
- **Office location:** Toronto
- **Manager:** James Patel (CFO)

These attributes do not provide a documented business justification for Innovation Center access.

![Identity data validation Daniel Cho](05-identity-data-validation-daniel-cho.png)

---

### 6. Remediate and Verify Inappropriate Access

Daniel Cho is removed from `SG-IC-Users`.

The group is reviewed again after remediation. Daniel is no longer present, while the five legitimate Innovation Center members remain.

This verifies that the inappropriate entitlement was removed without disrupting valid departmental access.

![Entitlement remediation verified](06-entitlement-remediation-verified.png)

---

## Findings and Remediation Summary

| Finding | Risk | Action | Result |
|---|---|---|---|
| Erik Wallace had no manager assigned | Review routing/context may be incomplete | Assigned Lori Van Meter as manager | Identity data corrected |
| Daniel Cho was in `SG-IC-Users` despite belonging to Finance | Excess/inappropriate access | Validated identity context and removed IC membership | Entitlement remediated |
| Legitimate IC users needed to retain access | Over-remediation could disrupt business access | Rechecked membership after removal | Five legitimate members remained |

---

## Control Logic Demonstrated

**Define scope → validate identity data → validate entitlement data → identify exceptions → determine business need → remediate inappropriate access → verify remediation → retain evidence**

A certification is only as reliable as the data supplied to the reviewer. Incorrect manager relationships, stale identity attributes, or inaccurate entitlement data can produce incorrect certification decisions and weak audit evidence.

---

## Governance and Audit Relevance

This exercise models activities that support periodic system access certifications and User Access Reviews in regulated environments:

- **Data completeness and accuracy** — validate identity and entitlement information before certification.
- **Least privilege** — retain access only where a valid business requirement exists.
- **Reviewer accountability** — accurate identity and manager data supports appropriate review.
- **Exception handling** — investigate questionable access rather than blindly approving it.
- **Remediation** — remove denied or unjustified access.
- **Verification** — confirm that remediation occurred correctly.
- **Evidence retention** — preserve evidence supporting the review process.

These concepts are relevant to access-control evidence used in environments subject to requirements such as **SOX, SOC 1, SOC 2, HITRUST, and PCI-DSS**.

---

## Key Takeaway

Access certification is more than asking a manager to click **Approve** or **Deny**.

A defensible certification process depends on trustworthy identity, application, and entitlement data. IAM must validate that data, route access to appropriate reviewers, investigate exceptions, remediate access that is no longer justified, verify the change, and preserve evidence.

In this lab, an incomplete manager relationship was corrected before review, an inconsistent entitlement was identified through identity-to-access comparison, and the inappropriate access was removed and verified.

---

## Skills Demonstrated

- Microsoft Entra ID
- User Access Reviews (UAR)
- Access Certification Data Validation
- Identity Data Quality
- Entitlement Validation
- Least Privilege
- Reviewer Accountability
- Access Remediation
- Remediation Verification
- Audit Evidence
- IAM Governance Documentation
