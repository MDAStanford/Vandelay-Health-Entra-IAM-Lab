# Lab 14 — Hybrid Identity with Microsoft Entra Connect Sync

## Project Overview

Vandelay Health is a fictional medical-device company headquartered in Santa Monica, California. Its flagship product, the **Ninja Sleeper**, originated from a federal government contract requiring an exceptionally quiet sleeping solution for military personnel operating in the field. Vandelay later adapted as much of the proprietary technology as possible for the commercial market, creating a lightweight and quiet consumer sleep-therapy platform.

As Vandelay Health expands its operations, the company is moving from separate on-premises and cloud identity environments toward a **hybrid identity architecture**. Employees working in the recently established Toronto Innovation Center already have accounts in the company's `vandelay.local` Active Directory domain, while Vandelay also uses Microsoft Entra ID for cloud identity and access management.

This lab implements **Microsoft Entra Connect Sync** to integrate those environments and establish synchronized hybrid identities.

---

## Business Scenario

Vandelay Health's Toronto Innovation Center was previously established as an on-premises Active Directory environment. Seven Toronto employees were provisioned into a dedicated organizational structure with standardized identity attributes and department-based access.

The next requirement was to connect those identities to Vandelay Health's Microsoft Entra ID tenant.

Rather than independently administering separate Active Directory and Entra identities for the same employees, Vandelay needed an identity architecture in which the on-premises directory could act as an authoritative identity source while selected identity information synchronized to Microsoft Entra ID.

The implementation needed to:

- Prepare the existing Toronto Active Directory identities for synchronization.
- Align user principal names with the Microsoft Entra ID tenant.
- Install and configure Microsoft Entra Connect Sync.
- Enable Password Hash Synchronization.
- Establish synchronization between `vandelay.local` and the Vandelay Health Entra tenant.
- Validate that Entra recognized synchronized users as originating from on-premises Active Directory.
- Confirm the relationship between an Entra identity and its corresponding Active Directory object.
- Validate the synchronization scheduler.
- Perform and verify an administrator-initiated delta synchronization.

---

## Environment

### On-Premises

- Windows Server 2022
- Active Directory Domain Services
- Domain: `vandelay.local`
- Domain Controller: `Vandelay-DC01`
- Toronto organizational units
- Active Directory Users and Computers
- Active Directory PowerShell module

### Cloud

- Microsoft Entra ID
- Vandelay Health Microsoft Entra tenant
- Microsoft Entra Connect Sync

### Synchronization

- Microsoft Entra Connect Sync
- Password Hash Synchronization
- Scheduled delta synchronization
- Administrator-initiated delta synchronization

---

## Hybrid Identity Architecture

The resulting identity flow is:

**Active Directory (`vandelay.local`) → Microsoft Entra Connect Sync → Microsoft Entra ID**

This creates a hybrid identity model in which the on-premises Active Directory object and Microsoft Entra ID identity are connected rather than managed as unrelated accounts.

---

## 1. Validate Existing Toronto Identities

Before configuring synchronization, the existing Toronto Active Directory environment was reviewed.

Seven users were already provisioned under the Toronto Users OU:

- Eric Lund
- Erik Wallace
- Jay Martin
- Lisa Brock
- Lori Van Meter
- Paul Merson
- Shawn Rudey

![Toronto Active Directory users before hybrid synchronization](images/01-toronto-ad-users-before-hybrid-sync.png)

This established the on-premises identity population that would participate in the hybrid identity implementation.

---

## 2. Validate User Principal Names

Eric Lund was selected as the primary validation identity for the synchronization process.

His Active Directory account was reviewed to verify the User Principal Name configuration before synchronization.

![Eric Lund Active Directory UPN before synchronization](images/02-eric-lund-ad-upn-before-sync.png)

The corresponding Microsoft Entra identity was also reviewed before synchronization.

![Eric Lund Entra identity before synchronization](images/03-eric-lund-entra-upn-before-sync.png)

PowerShell was then used to validate the UPN configuration across the Toronto user population.

![Toronto Active Directory UPN validation](images/04-toronto-ad-upn-validation-before-sync.png)

This step helped ensure that identity attributes were prepared consistently before establishing synchronization.

---

## 3. Configure Microsoft Entra Connect Sync

Microsoft Entra Connect Sync was installed on `Vandelay-DC01` and configured to connect the on-premises `vandelay.local` Active Directory forest with the Vandelay Health Microsoft Entra tenant.

The configuration included:

- Active Directory forest connectivity
- Microsoft Entra tenant connectivity
- Source anchor configuration
- Password Hash Synchronization
- Synchronization services
- Microsoft Entra ID export deletion protection

After configuration, Microsoft Entra Connect reported that configuration had completed successfully and that the synchronization process had been initiated.

![Microsoft Entra Connect configuration complete](images/14-entra-connect-configuration-complete.png)

---

## 4. Validate Synchronized Identities in Microsoft Entra ID

After synchronization, the Microsoft Entra admin center was used to review the user population.

The synchronized Toronto identities displayed an **On-premises sync** status of **Yes**, confirming that Microsoft Entra recognized the accounts as synchronized identities.

![Microsoft Entra ID synchronized users](images/15-entra-id-synchronized-users.png)

This represented the transition from independently maintained cloud identities to identities associated with the on-premises Active Directory environment.

---

## 5. Validate the Hybrid Identity Relationship

Eric Lund's Entra identity was examined in greater detail to validate the relationship with his Active Directory account.

Microsoft Entra reported:

- **On-premises sync enabled:** Yes
- **On-premises distinguished name:** Toronto Users OU
- **On-premises immutable ID:** populated
- **On-premises SAM account name:** `Eric.Lund`
- **On-premises security identifier:** populated
- **On-premises domain name:** `vandelay.local`

![Hybrid identity on-premises synchronization details](images/16-hybrid-identity-on-premises-sync-details.png)

These attributes provide direct evidence that the Entra identity is associated with an object originating from Vandelay Health's on-premises Active Directory environment.

---

## 6. Validate the Active Directory Source Identity

The same identity was then reviewed from the Active Directory side.

Using **Active Directory Users and Computers → Attribute Editor**, Eric Lund's `userPrincipalName` attribute was validated against the identity appearing in Microsoft Entra ID.

![Microsoft Entra Connect Active Directory UPN validation](images/17-entra-connect-ad-upn-validation.png)

This provides validation from both sides of the hybrid identity relationship:

**Active Directory identity → Entra Connect → Microsoft Entra identity**

---

## 7. Validate the Synchronization Scheduler

Microsoft Entra Connect's synchronization scheduler was inspected using PowerShell:

```powershell
Get-ADSyncScheduler
