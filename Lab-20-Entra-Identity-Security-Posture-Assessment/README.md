# Lab 20 — Entra Identity Security Posture Assessment

Vandelay Health is preparing its Microsoft Entra ID environment to transition from active development into a more mature operational state. The environment already contains identity lifecycle processes, privileged access controls, Conditional Access policies, access reviews, external identities, and hybrid identity components developed across earlier labs.

In this lab, I shifted from implementing individual IAM controls to assessing the existing **identity security architecture** as a whole. The objective was to establish a current-state baseline, identify genuine security and governance gaps, recognize controls operating effectively, and document recommendations for the target-state architecture. This lab is an **assessment exercise**; identified issues are documented rather than remediated so they can feed subsequent risk analysis and remediation planning.

## Objective

Perform a structured Microsoft Entra ID identity security posture assessment focused on:

- Identity lifecycle and deprovisioning
- Privileged administrative access
- Authentication and Conditional Access
- Authorization and entitlement governance
- External identity governance
- Access-review effectiveness

The assessment follows a simple operating model:

**ASSESS → IDENTIFY → ANALYZE → RECOMMEND**

Remediation and formal risk scoring are intentionally outside the scope of this lab.

## Assessment Methodology

The review moved outward through the identity architecture in a deliberate sequence:

1. **Identity population and lifecycle** — Who has an identity, and does offboarding fully remove access?
2. **Privileged access** — Who holds administrative authority, and is standing privilege justified?
3. **Authentication and Conditional Access** — Which controls are designed, tested, and actually enforced?
4. **Authorization and entitlements** — How is access granted and periodically reviewed?
5. **External identity governance** — How is guest access governed and recertified?
6. **Control effectiveness** — Which existing governance controls demonstrate successful operation?

Findings were documented only when supported by observed configuration or identity data. Existing controls that operated as intended were also recorded to avoid treating the assessment as a vulnerability-only exercise.

## Assessment Findings

| ID | Finding | Evidence | Recommendation | Status |
|---|---|---|---|---|
| IAM-001 | Disabled identity retains entitlements | Paul Merson is disabled but remains in four Entra groups, including SG-NS2-Project. | Complete entitlement cleanup as part of offboarding. | Open |
| IAM-002 | Standing Global Administrator access | IT - Michael Stanford and BREAK GLASS hold active Global Administrator assignments; the operational administrator also has a PIM-eligible User Administrator role. | Move operational Global Administrator access to PIM/JIT when the architecture reaches operational handoff. | Accepted — Build State |
| IAM-003 | MFA policy not enforced | The MFA Conditional Access policy targets all users and resources but remains Report-only; IT - Michael Stanford and BREAK GLASS are excluded. | Validate exclusions and transition the policy to enforcement at operational handoff. | Open — Report Only |
| IAM-004 | Location restriction not enforced | The Switzerland Conditional Access policy is configured to block access but remains Report-only; IT - Michael Stanford is excluded. | Validate the administrator exclusion and transition the policy to enforcement at operational handoff. | Open — Report Only |

## Finding Analysis

### IAM-001 — Disabled Identity Retains Entitlements

Paul Merson's account is disabled, but the identity retains membership in multiple Entra groups. This demonstrates that disabling an identity and removing its authorization entitlements are separate lifecycle actions. The finding highlights an offboarding gap in the current architecture: account disablement alone does not guarantee complete entitlement cleanup, particularly where dynamic group membership is attribute-driven.

**Target-state recommendation:** Establish a complete deprovisioning process that removes assigned entitlements and accounts for dynamic-group eligibility when an identity is disabled or terminated.

### IAM-002 — Standing Global Administrator Access

The operational administrator and BREAK GLASS account both currently hold direct, active Global Administrator assignments. The operational administrator also has User Administrator configured as a PIM-eligible role, demonstrating that Privileged Identity Management is already part of the environment.

The standing Global Administrator assignment is an intentional **build-state architecture decision** while the tenant remains under active development and assessment. It is therefore documented rather than treated as an unexplained configuration error.

**Target-state recommendation:** At operational handoff, transition the operational Global Administrator assignment from standing active access to PIM-managed eligible/JIT access while preserving the designated emergency-access architecture.

### IAM-003 — MFA Conditional Access Policy Not Enforced

The MFA Conditional Access policy is designed to cover all users and all resources and requires multifactor authentication. The policy remains in **Report-only** mode, meaning it is evaluated but not enforced. BREAK GLASS and the operational administrator are currently excluded.

This configuration is consistent with a development and testing architecture, where report-only deployment can be used to evaluate policy impact before enforcement.

**Target-state recommendation:** Review report-only behavior and exclusions, validate policy impact, and transition the MFA policy to enforcement during operational hardening.

### IAM-004 — Location-Based Access Restriction Not Enforced

The Switzerland Conditional Access policy targets the intended geographic condition and is configured to **Block access**, but the policy remains in Report-only mode. The operational administrator is also excluded.

The control therefore exists in the architecture but has not yet transitioned from evaluation to enforcement.

**Target-state recommendation:** Validate policy behavior and the administrator exclusion, then move the location-based restriction to enforcement during operational hardening.

## Effective Controls Observed

The assessment also identified controls that are operating as designed.

### External Access Review

The **Ninja Sleeper II External Access Review** provides a quarterly access-certification control for guest users assigned to SG-NS2-Project. The review is scoped to external identities and assigned to resource owners, providing recurring governance over access to highly restricted Ninja Sleeper II project resources.

### Toronto Access Recertification

The **Toronto Office Access Recertification** demonstrates completed internal access governance for SG-IC-Users. Five identities received review decisions: four were approved and one was denied, with the review status showing **Result applied**. This provides evidence that access-review decisions can progress through certification and application rather than remaining purely informational.

## Architecture Assessment

The assessment shows an Entra environment with meaningful identity-governance controls already in place, alongside several controls that remain in development or transition state.

The principal architecture themes identified were:

- Identity disablement must be paired with complete entitlement cleanup.
- Standing privileged access is acceptable as a documented build-state exception but should not become the long-term operational model.
- Conditional Access controls have been designed but require transition from report-only evaluation to enforcement.
- Access reviews provide working governance mechanisms for both internal and external access.

These observations establish a current-state identity security baseline and define clear target-state architecture recommendations without changing the environment during the assessment itself.

## Deliverable

The primary output of this lab is an **Identity Security Assessment Findings Register** containing four evidence-supported findings and their recommended target states.

Formal likelihood, impact, severity, risk ownership, treatment decisions, and residual-risk tracking are intentionally deferred to a subsequent **Identity Security Risk Register & Remediation Planning** exercise.

## Skills Demonstrated

- Microsoft Entra ID security posture assessment
- Identity architecture analysis
- Identity lifecycle and deprovisioning review
- Privileged-access assessment
- Privileged Identity Management (PIM)
- Conditional Access assessment
- MFA policy analysis
- Access-review and entitlement-governance assessment
- External identity governance
- Evidence-based security findings
- Current-state and target-state architecture analysis
- Security-control effectiveness validation
- IAM assessment documentation

## Outcome

Lab 20 demonstrates the transition from configuring individual IAM controls to evaluating how those controls operate together within an enterprise identity architecture. The result is a documented security baseline that identifies both control gaps and effective governance mechanisms and provides a defensible foundation for subsequent risk prioritization and remediation planning.
