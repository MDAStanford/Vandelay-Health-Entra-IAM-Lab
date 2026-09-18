Lab 17 — Microsoft Graph PowerShell: Identity Investigation & Access Remediation
Scenario

Vandelay Health's IAM team needed to investigate the status and access footprint of an Innovation Center user as part of an identity lifecycle review supporting the Ninja Sleeper program.

The original Ninja Sleeper was developed under a federal contract to provide military personnel in the field with a silent sleeping solution. Vandelay Health subsequently adapted the technology for commercial use while retaining as much proprietary intellectual property as possible. Protecting access to Ninja Sleeper development resources therefore requires disciplined identity lifecycle management, least privilege, and auditable administrative activity.

During the review, Sandra Melancon, an Innovation Program Manager, remained enabled in Microsoft Entra ID and retained access to multiple resources, including the Innovation Center and Ninja Sleeper II project groups. The IAM investigation used Microsoft Graph PowerShell and Entra audit data to identify her current identity state, group memberships, and historical administrative activity before remediation.

Objectives
Connect securely to Microsoft Graph using delegated permissions.
Validate the authenticated administrator and granted Graph scopes.
Query Entra ID users and groups with PowerShell.
Investigate Sandra Melancon's identity state and group memberships.
Review Entra audit logs for historical administrative activity.
Remove unnecessary project access using Microsoft Graph.
Diagnose authorization and authentication failures encountered during remediation.
Validate the resulting identity state and preserve evidence of the investigation.
Investigation

Microsoft Graph PowerShell was used to enumerate tenant users and groups and verify Sandra's cloud identity.

Sandra was confirmed as:

Display Name: IC - Sandra Melancon
Department: Innovation Center
Job Title: Innovation Program Manager
Account Enabled: True

The investigation also established that Sandra was a cloud-only Entra identity, with no corresponding account in the on-premises vandelay.local Active Directory environment.

Her Entra group memberships included:

SG-IC-Users
M365-IC-Team
SG-TOR-Users-Dynamic
SG-NS2-Project

The presence of SG-NS2-Project identified project-specific access requiring remediation.

Microsoft Graph Permissions

The investigation demonstrated delegated Microsoft Graph access using permissions including:

AuditLog.Read.All
Group.Read.All
GroupMember.ReadWrite.All
User.Read.All

The lab also demonstrated an important distinction between authentication and authorization. A successful Graph connection did not automatically provide permission to perform every administrative operation.

An attempted group-membership removal initially returned:

403 Forbidden — Authorization_RequestDenied — Insufficient privileges to complete the operation.

The Graph context and delegated scopes were subsequently reviewed as part of troubleshooting.

Security Defaults Troubleshooting

Microsoft Graph authentication also generated Error 530035 during testing.

Rather than treating the failure simply as a PowerShell problem, Entra sign-in logs were examined to determine the control responsible for the failure.

The investigation showed:

Failure reason: Access has been blocked by security defaults.

Authentication details demonstrated that authentication had been satisfied, while the Conditional Access evaluation identified:

Policy: Security Defaults
Grant control: Block
Result: Failure

Tenant properties independently confirmed that Security Defaults were enabled.

This provided a complete troubleshooting chain:

PowerShell failure → Entra sign-in event → authentication review → access-control evaluation → tenant configuration

IAM Lessons Demonstrated

This lab demonstrates several operational IAM concepts relevant to enterprise identity administration:

Identity investigation before remediation
Cloud-only versus synchronized identity recognition
Microsoft Graph delegated permissions
Least-privilege administrative access
Group-based authorization
Identity lifecycle remediation
Entra audit-log analysis
Authentication versus authorization troubleshooting
Security Defaults enforcement
Evidence-based root-cause analysis
Evidence

Lab17-01 — Graph Security Defaults Blocked Sign-In
Entra sign-in record showing Error 530035 and identifying Security Defaults as the reason access was blocked.

Lab17-02 — Graph Authentication Details
Authentication details used to determine that the failure was not simply an invalid username or password.

Lab17-03 — Graph Conditional Access Evaluation
Access-control evaluation showing Security Defaults, Block, and Failure.

Lab17-04 — Security Defaults Enabled
Tenant configuration confirming that Vandelay World Wide had Security Defaults enabled.

Outcome

The investigation successfully used Microsoft Graph PowerShell, Microsoft Entra ID, delegated permissions, group membership analysis, and Entra audit/sign-in logs to investigate an identity lifecycle issue and trace administrative failures to their underlying security controls.

Rather than bypassing an unexplained failure, the IAM workflow identified the affected identity, established its access footprint, examined the relevant audit trail, evaluated Graph authorization, and traced authentication behavior through Entra sign-in telemetry.

This lab demonstrates a practical enterprise IAM workflow in which PowerShell administration and Entra security telemetry are used together to investigate, troubleshoot, and validate identity access.
