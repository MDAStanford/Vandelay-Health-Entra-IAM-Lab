# IAM-2026-015B — Paul Merson Offboarding

> **SIMULATED HR SERVICE REQUEST** — Vandelay Health, Newman GmbH, and this request are fictional. Ticket ID, request authority, and workflow are illustrative, not real organizational records.

| Field | Value |
|---|---|
| Ticket | IAM-2026-015B |
| Request type | Leaver — Termination |
| Requesting function | Human Resources |
| Assigned function | IAM Operations |
| Employee | Paul Merson |
| Role | Operations Manager |
| Location | Toronto, Ontario |
| Status | Lab outcome documented; formal ticket closure not independently evidenced |

## Business Request

Disable Paul Merson's corporate identity and revoke his specified Toronto Innovation Center (IC) security-group access while retaining the disabled identity as a record.

## Requested Scope

- Review the existing AD account and specified IC group membership.
- Disable Paul's AD account.
- Remove membership in `SG-TOR-IC-Users`.
- Validate the disabled account state in Microsoft Entra ID.
- Retain the disabled identity rather than deleting it.

## Acceptance Criteria and Evidence

- [x] Pre-change enabled state and IC group membership documented.
- [x] AD account disabled — post-change PowerShell evidence.
- [x] `SG-TOR-IC-Users` membership absent — follow-up Member Of screenshot.
- [x] Entra account disabled — named cloud properties screenshot.
- [ ] Original HR authorization, termination SLA timing, and all downstream application entitlements independently verified.

See the [Lab 15 README](README.md) for inline screenshots and implementation details.

## Closure / Limitations

**Simulated implementation outcome: validated in follow-up review.** The evidence establishes the observed AD and Entra account states and the specified group removal. It does not establish the original completion time or confirm revocation of every application entitlement. HR and Legal matters remain outside the IAM scope.
