# IAM-2026-015A — Joe Cantoni Onboarding

> **SIMULATED HR SERVICE REQUEST** — Vandelay Health and this request are fictional. Ticket ID, request authority, and workflow are illustrative, not real organizational records.

| Field | Value |
|---|---|
| Ticket | IAM-2026-015A |
| Request type | Joiner — New Hire |
| Requesting function | Human Resources |
| Assigned function | IAM Operations |
| Employee | Joe Cantoni |
| Location | Toronto, Ontario |
| Department | Innovation Center |
| Status | Lab outcome documented; formal ticket closure not independently evidenced |

## Business Request

Provision Joe Cantoni with a corporate identity and standard Toronto Innovation Center (IC) access in the hybrid Active Directory (AD) and Microsoft Entra ID environment.

## Requested Scope

- Create and enable Joe's AD account in the Toronto Users organizational unit.
- Populate appropriate identity attributes, including Innovation Center as department.
- Assign the standard `SG-TOR-IC-Users` security group.
- Synchronize and validate the identity in Microsoft Entra ID.

## Acceptance Criteria and Evidence

- [x] AD account enabled — captured AD validation.
- [x] Toronto IC security-group membership — Member Of screenshot.
- [x] Department corrected to Innovation Center — saved AD properties.
- [x] Entra Connect delta sync requested successfully — PowerShell output.
- [x] Synced, enabled Entra identity observed — Entra properties screenshot.
- [ ] HR source record, original request authorization, and completion time independently verified.

See the [Lab 15 README](README.md) for inline screenshots and implementation details.

## Closure / Limitations

**Simulated implementation outcome: validated in follow-up review.** The screenshots support the observed configuration, including the October 8, 2026 correction and cloud validation. They do not independently prove an original HR approval, elapsed ticket handling time, or SLA compliance.
