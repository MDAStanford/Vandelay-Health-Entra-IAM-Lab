# Lab 23 — NIST SP 800-53 Security Control Assessment & POA&M

## Overview

Vandelay Health is a fictional healthcare technology company headquartered in Santa Monica, California. Its Ninja Sleeper CPAP technology originated from a federal government project and was subsequently adapted for commercial use.

The Ninja Sleeper incorporates highly restricted, proprietary intellectual property. Vandelay Health uses Active Directory, Microsoft Entra ID, and Okta to manage workforce identities and protect access to organizational resources.

In this lab, I acted as a Security & Compliance Analyst and examined evidence from my existing IAM labs. I used selected NIST SP 800-53 Revision 5 control objectives and an examination approach informed by NIST SP 800-53A Revision 5 to evaluate what the evidence supported and identify where additional evidence was needed.

## Assessment Objective

My objective was to assess selected account management, least-privilege, and authentication activities without treating incomplete evidence as proof of a control failure.

I mapped screenshots and documentation from Labs 15, 08, 02, and 06 to three controls:

- **AC-2 — Account Management**
- **AC-6 — Least Privilege**
- **IA-2 — Identification and Authentication**

## Status

**I completed the scoped evidence examination on October 9, 2026.**

I documented all three controls as **partially assessed** because the available evidence did not establish complete control effectiveness. I left follow-up evidence requests open and made no overall compliance determination.

## What I Did

I reviewed account provisioning and termination evidence from Lab 15, privileged-access evidence from Lab 08, authentication evidence from Lab 02, and access-review evidence from Lab 06.

For each control, I separated visible configuration and observed outcomes from narrative claims. I recorded the evidence limitations, identified the follow-up needed, and documented my assessment conclusions in the Security Assessment Report.

I also maintained an evidence request register and a Plan of Action and Milestones (POA&M) disposition. I did not open active POA&M items because my examination established no confirmed unresolved access-control deficiency.

## Assessment Results

| Control | What I could support | What I still needed to establish |
|---|---|---|
| AC-2 — Account Management | Selected Active Directory account and group outcomes, Microsoft Entra ID account states, Joe's department correction, and one access review with decisions, audit records, and final membership | Authorization, original timing, complete access coverage, recurring review operation, and detailed review-result traceability |
| AC-6 — Least Privilege | Privileged Identity Management (PIM) activation/removal audit events and targeted membership changes | Readable versions of five Lab 08 images, exact role settings, effective privilege inventory, approvals, and the rationale for the narrowest suitable role |
| IA-2 — Identification and Authentication | A named user, registered Microsoft Authenticator, and a report-only multifactor authentication (MFA) policy | MFA enforcement, named exclusions, and full coverage; the displayed successful sign-in used single-factor authentication |

## Deliverables

I documented the examination and remaining follow-up in these files:

- [Scoped Security Assessment Report v1.0](Security-Assessment-Report.md)
- [Evidence Request Register and consolidated collection list](Evidence-Request-Register.md)
- [POA&M disposition](POAM.md)

## Assessment Boundaries

I examined existing screenshots and documentation. I performed no independent tests or completed interviews, and I did not treat historical captures as proof of current tenant-wide configuration.

I limited this examination to selected objectives for AC-2, AC-6, and IA-2. I did not assess Okta, a federal baseline, or a complete set of control enhancements.

## What I Practiced

Through this lab, I practiced mapping controls to evidence, evaluating screenshot reliability and completeness, documenting scoped assessment conclusions, and tracking follow-up requests.

I also practiced distinguishing evidence gaps from confirmed deficiencies and explaining why an incomplete assessment does not automatically justify a POA&M item.

## Key Takeaway

I learned to make each assessment conclusion traceable to the available evidence. When the evidence supported only part of a control, I documented that limit and requested the specific records needed to complete the assessment.

---

*This is a fictional portfolio training exercise, not an independent compliance audit, federal authorization, or FedRAMP assessment.*
