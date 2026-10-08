# Lab 23 — NIST SP 800-53 Security Control Assessment & POA&M

## Overview

Vandelay Health is a fictional healthcare technology company headquartered in Santa Monica, California. Its Ninja Sleeper CPAP technology originated from a federal government project and was subsequently adapted for commercial use.

The Ninja Sleeper incorporates highly restricted, proprietary intellectual property. Vandelay Health uses Active Directory, Microsoft Entra ID, and Okta to manage workforce identities and protect access to organizational resources.

## Assessment Objective

Evaluate selected security controls against NIST SP 800-53 Revision 5 using evidence collected from the Vandelay Health identity environment.

Document control effectiveness, evidence limitations, potential deficiencies, remediation recommendations, and Plans of Action and Milestones (POA&Ms).

## Control 1 — AC-2: Account Management

**Evidence source:** Lab 15 — Ticket-Driven Identity Lifecycle Operations

**Assessment method:** Examine existing documentation and screenshots.

### Evidence Reviewed

- New employee account creation and validation
- Role-based security group assignment
- Employee account disablement
- Security group access removal
- Entra Connect synchronization
- Microsoft Entra ID account validation

### Assessment Results

The available evidence supports execution of selected account provisioning and termination procedures.

However, the existing documentation does not independently establish HR authorization timestamps, termination SLA compliance, or periodic account review effectiveness.

**Assessment determination:** Partially assessed — insufficient evidence to conclude that the complete AC-2 control is satisfied.

### Observations

**AC2-OBS-001:** Termination timeliness cannot be independently verified from the available evidence.

**AC2-OBS-002:** Periodic account review effectiveness was not established by the reviewed Lab 15 artifacts.

These are evidence limitations, not confirmed security control failures.

## Next Assessment

AC-6 — Least Privilege

**Status:** Not yet assessed.

---

*This project is a portfolio-based security control assessment performed in a fictional training environment. It is not an independent compliance audit or formal authorization assessment.*
