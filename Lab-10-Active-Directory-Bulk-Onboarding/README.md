# Vandelay Health — Toronto Active Directory Identity & Access Lab

## Project Overview

This lab simulates a post-acquisition identity and access management scenario for Vandelay Health, a fictional consumer medical-device company headquartered in Santa Monica, California.

Vandelay Health recently acquired a small design studio in Toronto, Canada. Six employees joined the Toronto Innovation Center, while one employee supports Toronto Operations. The acquired employees needed to be incorporated into the company's Active Directory environment with a consistent organizational structure, standardized identity attributes, and appropriate security-group access.

The project demonstrates a practical IAM workflow:

**Identity source → user provisioning → identity attributes → security-group access → validation**

> **Note:** Vandelay Health and the business scenario in this project are fictional. The environment was created solely as a hands-on identity and access management lab.

---

## Business Scenario

Following the Toronto acquisition, Vandelay Health needed to onboard seven employees from the acquired design studio into its corporate identity environment.

The implementation needed to:

- Establish a dedicated Toronto organizational structure in Active Directory.
- Provision the acquired employees efficiently rather than creating each account manually.
- Populate consistent employee attributes from a structured source.
- Create security groups representing the Toronto Innovation Center and Operations access populations.
- Assign employees to the appropriate security groups.
- Validate that the resulting identities and access assignments were correct.

The lab represents the type of identity administration work that can accompany an acquisition, office expansion, or bulk employee onboarding event.

---

## Lab Environment

- **Windows Server 2022**
- **Active Directory Domain Services (AD DS)**
- **Domain:** `vandelay.local`
- **Domain Controller:** `Vandelay-DC01`
- **Administrative tools:** Active Directory Users and Computers (ADUC) and PowerShell
- **Structured identity source:** CSV
- **Location:** Toronto, Ontario, Canada

The Toronto Active Directory structure contains separate organizational units for users, groups, and computers:

```text
vandelay.local
└── Toronto
    ├── Computers
    ├── Groups
    └── Users
```

---

## Phase 1 — Toronto Organizational Structure

A Toronto organizational unit was established to separate the newly acquired location from the existing Vandelay environment.

Dedicated child OUs were used for users, groups, and computers, creating a structure that can support future administration, access management, and policy assignment.

### Evidence — Toronto Users

![Toronto Users](screenshots/06-toronto-users-ou.png)

---

## Phase 2 — Bulk User Provisioning

Seven Toronto employee identities were provisioned in Active Directory.

Rather than manually creating each identity through the GUI, PowerShell was used to support repeatable and scalable onboarding.

The Toronto identity population consists of:

| Employee | Toronto Assignment |
|---|---|
| Eric Lund | Innovation Center |
| Erik Wallace | Innovation Center |
| Jay Martin | Innovation Center |
| Lisa Brock | Innovation Center |
| Lori Van Meter | Innovation Center |
| Paul Merson | Innovation Center |
| Shawn Rudey | Operations |

This approach models a bulk onboarding event in which an acquired employee population must be incorporated into an existing directory.

---

## Phase 3 — Structured Identity Attribute Management

A CSV file was created to serve as the structured source for employee identity information.

The dataset included:

- `SamAccountName`
- `Title`
- `Department`
- `Company`
- `Office`
- `City`
- `State/Province`
- `Country`

PowerShell imported the CSV and updated the corresponding Active Directory user objects with `Set-ADUser`.

Example workflow:

```powershell
Import-Csv "C:\Users\Administrator\Desktop\Toronto-User-Attributes.csv" | ForEach-Object {
    Set-ADUser -Identity $_.SamAccountName `
        -Title $_.Title `
        -Department $_.Department `
        -Company $_.Company `
        -Office $_.Office `
        -City $_.City `
        -State $_.State `
        -Country $_.Country
}
```

The results were then validated using `Get-ADUser` and ADUC.

### Evidence — Bulk Attribute Update and Verification

*Insert existing bulk attribute verification screenshot.*

### Evidence — ADUC Attribute Verification

*Insert existing ADUC attribute verification screenshot.*

---

## Phase 4 — Toronto Security Groups

Global Security Groups were created in the Toronto `Groups` OU to represent the two access populations used in this scenario:

- `SG-TOR-IC-Users`
- `SG-TOR-Operations`

The naming convention identifies the objects as security groups (`SG`) associated with the Toronto location (`TOR`).

`SG-TOR-IC-Users` represents the six users assigned to the Toronto Innovation Center, while `SG-TOR-Operations` represents the Toronto Operations user.

This separates organizational placement in the directory from security-group membership used to manage access.

### Evidence — Toronto Security Groups

*Insert corrected screenshot showing `SG-TOR-IC-Users` and `SG-TOR-Operations`.*

---

## Phase 5 — Security-Group Access Assignment

PowerShell was used to assign the six Innovation Center identities to `SG-TOR-IC-Users`.

```powershell
Add-ADGroupMember -Identity "SG-TOR-IC-Users" `
    -Members "Eric.Lund","Erik.Wallace","Jay.Martin","Lisa.Brock","Lori.VanMeter","Paul.Merson"
```

The Toronto Operations identity was assigned separately:

```powershell
Add-ADGroupMember -Identity "SG-TOR-Operations" `
    -Members "Shawn.Rudey"
```

Using PowerShell for the multi-user assignment provides a faster and more repeatable administrative workflow than adding each account individually through the GUI.

ADUC was then used to visually verify the resulting memberships.

---

## Phase 6 — Access Validation

Group memberships were queried with PowerShell and reviewed in ADUC to verify that each Toronto identity had been assigned to the expected security group.

The final validated access model was:

| Security Group | Members |
|---|---|
| `SG-TOR-IC-Users` | Eric Lund, Erik Wallace, Jay Martin, Lisa Brock, Lori Van Meter, Paul Merson |
| `SG-TOR-Operations` | Shawn Rudey |

### Evidence — Innovation Center Group Membership

![Innovation Center Group Membership](screenshots/09-sg-tor-ic-users-membership.png)

### Evidence — Operations Group Membership

![Operations Group Membership](screenshots/10-sg-tor-operations-membership.png)

Membership was also validated directly through PowerShell:

```powershell
Get-ADGroupMember "SG-TOR-IC-Users" |
    Select Name,SamAccountName

Get-ADGroupMember "SG-TOR-Operations" |
    Select Name,SamAccountName
```

This provided both command-line and graphical verification of the final access configuration.

---

## IAM Concepts Demonstrated

This project demonstrates hands-on experience with:

- Active Directory Domain Services administration
- Organizational Unit design
- Bulk identity provisioning
- CSV-driven identity administration
- PowerShell automation
- Active Directory user attributes
- Identity lifecycle onboarding
- Global Security Groups
- Security-group access assignment
- Group membership administration
- Access validation
- ADUC and PowerShell verification
- Repeatable identity administration processes

---

## Why This Matters

Identity administration is more than creating accounts. An effective onboarding process should establish reliable identity data, organize identities consistently, assign appropriate access, and verify the resulting configuration.

In this scenario, the Toronto acquisition required Vandelay Health to move from a list of acquired employees to managed Active Directory identities with standardized attributes and defined security-group access.

The resulting workflow demonstrates how structured identity information, PowerShell automation, Active Directory organizational design, and access validation can reduce repetitive administration and create a more consistent onboarding process.

---

## Future Expansion

This on-premises Active Directory environment can serve as the foundation for future hybrid identity work, including:

- Configuring a routable User Principal Name (UPN) suffix
- Integrating on-premises identities with Microsoft Entra ID
- Exploring hybrid identity synchronization
- Extending group and attribute strategies into cloud identity
- Applying Joiner-Mover-Leaver lifecycle processes
- Testing access reviews and identity governance controls

These items are intentionally outside the scope of the completed Toronto onboarding phase.

---

## Project Status

**Completed — Toronto Active Directory provisioning and security-group access assignment**

The seven-person Toronto employee population has been provisioned, identity attributes have been standardized, the Toronto OU structure has been established, security groups have been configured for the Innovation Center and Operations populations, and resulting group memberships have been validated using both PowerShell and ADUC.

---

*Vandelay Health is a fictional organization created for cybersecurity and identity-management portfolio projects. No production systems, patient information, or real organizational data were used in this lab.*
