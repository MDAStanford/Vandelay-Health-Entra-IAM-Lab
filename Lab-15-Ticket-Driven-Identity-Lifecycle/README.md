# Lab 15 — Ticket-Driven Identity Lifecycle Operations

<mark>**FICTIONAL COMPANY — Vandelay Health is a fictional healthcare technology company that produces the Ninja Sleeper, a commercialized version of technology originally developed for the U.S. military to address sleep apnea in field environments.**</mark>

![Vandelay Health — Lab 15: Ticket-Driven Identity Lifecycle](Lab15-Cover-Paul-Offboarding-v2.png)

---

## Business Requests

**Simulated HR tickets:** [IAM-2026-015A — Joe Cantoni onboarding](IAM-2026-015A-Joe-Onboarding-Ticket.md) · [IAM-2026-015B — Paul Merson offboarding](IAM-2026-015B-Paul-Offboarding-Ticket.md)

This lab simulates two HR-driven identity lifecycle tickets: onboarding Joe Cantoni and terminating Paul Merson's access across **Active Directory (AD)** and **Microsoft Entra ID**, using the hybrid environment established in Lab 14.

The original account-administration evidence is supplemented by follow-up validation captured on **October 8, 2026**. During that review, Joe's department attribute was corrected from Information Technology to Innovation Center and the updated value was verified in Entra ID.

---

## Ticket 1 — New Hire Onboarding

**Employee:** Joe Cantoni  
**Location:** Toronto, Ontario  
**Department:** Innovation Center  
**Request:** Provision a corporate identity and standard IC access.

I reviewed an existing Toronto IC user to identify the organizational unit (OU), identity attributes, and standard security-group access. I created Joe's AD identity in the Toronto Users OU and assigned `SG-TOR-IC-Users`.

### Validation

![Joe Cantoni original AD account validation](Lab15-02-Joe-Cantoni-Group-Membership-Validation-CLEAN.png)

The original PowerShell output shows Joe's AD account enabled and its Toronto attributes. It also shows the initial Information Technology department value, which was corrected during the follow-up review.

![Joe Cantoni AD group membership](Lab15-07-Joe-AD-Group-Membership.png)

The October 8 Member Of view confirms membership in `SG-TOR-IC-Users` and Domain Users.

![Joe Cantoni saved department correction](Lab15-09-Joe-AD-Department-Correction.png)

The saved AD properties show **Innovation Center** as Joe's department.

![Entra Connect delta synchronization request](Lab15-11-Delta-Sync-Request.png)

`Start-ADSyncSyncCycle -PolicyType Delta` returned `Success`, confirming that the synchronization request was accepted. The cloud validation below establishes that the updated attribute reached Entra ID.

![Joe Cantoni Entra validation after synchronization](Lab15-12-Joe-Entra-Validation.png)

Joe's Entra properties show **Account enabled: Yes**, **On-premises sync enabled: Yes**, a department displayed as **Innovation Ce…**, and a last synchronization time of October 8, 2026 at 6:11 PM.

### Resolution

Joe's enabled AD identity, assigned IC group membership, corrected department attribute, and synchronized Entra identity are supported by the captured evidence.

**Implementation outcome:** Validated in follow-up review; formal ticket closure not independently evidenced.

---

## Ticket 2 — Employee Termination

**Employee:** Paul Merson  
**Role:** Operations Manager  
**Location:** Toronto, Ontario  
**Request:** Terminate corporate access immediately.

In the fictional scenario, HR requested termination of Paul's Vandelay access after he accepted a position with Newman GmbH. Employment and non-compete matters remain with HR and Legal.

I reviewed Paul's existing access, disabled his AD account, and removed his `SG-TOR-IC-Users` membership. I retained the identity rather than deleting it.

### Validation

![Paul Merson pre-termination access](Lab15-04-Paul-Merson-Pre-Termination-Access-CLEAN.png)

The original pre-termination output shows Paul's account enabled and membership in `SG-TOR-IC-Users`.

![Paul Merson AD account disablement](Lab15-05-Paul-Merson-AD-Offboarding-Validation-CLEAN.png)

The subsequent output confirms `Enabled = False` and shows the group-removal command.

![Paul Merson AD group removal validation](Lab15-08-Paul-AD-Group-Removal.png)

The October 8 Member Of view shows Domain Users and confirms that `SG-TOR-IC-Users` is absent.

![Paul Merson Entra account disabled](Lab15-10-Paul-Entra-Disabled.png)

Paul's named Entra properties show **Account enabled: No** and **On-premises sync enabled: Yes**.

### Resolution

Paul's AD account disablement, removal of the specified IC group membership, and disabled Entra account state are supported by the captured evidence.

**Simulated ticket status: Closed after follow-up validation.**

---

## Evidence Scope

The October 8 screenshots validate the account states at the time of review. They do not establish the original ticket completion time, compliance with a termination service-level agreement (SLA), or removal of every possible application entitlement.

The account-creation screenshot containing a plaintext lab password was removed from the current publication. Original screenshots with incomplete results remain in the repository for context; the validation above uses the images that establish each stated outcome.

---

**Technical environment:** Windows Server Active Directory, Microsoft Entra ID, Microsoft Entra Connect, PowerShell.

*Vandelay Health, Newman GmbH, and the scenarios in this project are fictional and were created for hands-on IAM training.*
