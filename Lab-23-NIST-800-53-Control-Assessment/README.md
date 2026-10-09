# Lab 23 — NIST SP 800-53 Security Control Assessment & POA&M

## Overview

Vandelay Health is a fictional healthcare technology company headquartered in Santa Monica, California. Its Ninja Sleeper CPAP technology originated from a federal government project and was subsequently adapted for commercial use.

The Ninja Sleeper incorporates highly restricted, proprietary intellectual property. Vandelay Health uses Active Directory, Microsoft Entra ID, and Okta to manage workforce identities and protect access to organizational resources.

## Assessment Objective

Examine existing IAM portfolio evidence against selected NIST SP 800-53 Revision 5 control objectives, using an examination approach informed by NIST SP 800-53A Revision 5.

## Status

**Scoped evidence examination complete — October 9, 2026.**

The report examines selected AC-2, AC-6, and IA-2 objectives using Labs 15, 08, 02, and 06. All three controls remain **partially assessed**. Follow-up evidence is open; no overall compliance determination is made.

## Deliverables

- [Scoped Security Assessment Report v1.0](Security-Assessment-Report.md)
- [Evidence Request Register and consolidated collection list](Evidence-Request-Register.md)
- [POA&M disposition](POAM.md)

## Assessment Results

| Control | Supported evidence | Remaining limitations |
|---|---|---|
| AC-2 — Account Management | Selected AD/group/Entra outcomes; corrected department; one access review with decisions, audit records and final membership | Authorization, original timing, complete access coverage, recurring review operation, detailed review-result traceability |
| AC-6 — Least Privilege | PIM activation/removal audit events; targeted membership changes | Five unreadable Lab 08 images, exact settings, effective privilege inventory, approval and narrowest-role rationale |
| IA-2 — Identification and Authentication | Named user, registered Authenticator, report-only MFA configuration | MFA enforcement not demonstrated; sign-in shown is single-factor; exclusions and full coverage not independently established |

## Assessment Boundaries

- Examined existing screenshots and documentation; performed no independent tests or completed interviews.
- Distinguished configuration, observed outcomes, narrative claims, and evidence limitations.
- Historical captures do not establish current tenant-wide configuration.
- Okta and other unexamined objectives remain outside this completed examination.
- No federal baseline or complete set of control enhancements was assessed.
- No confirmed unresolved access-control deficiency was established; therefore no active POA&M items were created.

## What I Practiced

- Control-to-evidence mapping
- Screenshot and documentation examination
- Evidence reliability and completeness evaluation
- Scoped assessment determinations
- Separation of evidence gaps from confirmed deficiencies
- Follow-up request tracking and POA&M disposition
- Assessment reporting with explicit limits

---

*This is a fictional portfolio training exercise, not an independent compliance audit, federal authorization, or FedRAMP assessment.*
