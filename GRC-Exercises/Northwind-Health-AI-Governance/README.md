# Northwind Health — AI Governance Risk Assessment

**Exercise type:** Guided scenario-based GRC analysis  
**Date:** October 23, 2026  
**Environment:** Fictional Northwind Health scenario; no production systems reviewed  
**Evidence standard:** Decisions based on the facts supplied in the exercise; proposed controls were not implemented or independently tested.

## Objective

Inventory five AI use cases, apply the supplied risk guide, select a treatment and priority control, identify the first investigation priority, and write three universal AI governance rules.

## Risk classification criteria (exercise-specific)

- **High:** ePHI involvement; decisions about people (including hiring, access, pay, or care); or customer-facing output that could cause harm if wrong.
- **Medium:** Internal confidential information or customer-facing output that could mislead.
- **Low:** Public or nonsensitive information only, with low-stakes or human-reviewed output.
- Apply the highest applicable classification.

## Assessment register

| Case | Use case | Risk | Proposed disposition | Primary control / condition |
| --- | --- | --- | --- | --- |
| 1 | Public-help-article website chatbot (live) | Low, assuming low-stakes output | Approve, subject to scope validation | Restrict to approved help content; guard against clinical advice and sensitive visitor inputs |
| 2 | Resume screener auto-rejecting bottom 50% (live) | High | Pause automated rejection | Qualified human review **before** rejection; documented job-related criteria; independent bias assessment |
| 3 | AI coding assistant receiving production logs (live) | High where logs contain ePHI | Approve with conditions | Redact/mask patient-related identifiers and sensitive content **before** submission; validate filtering |
| 4 | Clinical visit-note summarizer sending ePHI to vendor API (planned) | High | Conditional approval; do not launch until controls verified | Pre-launch privacy/security review of vendor data handling and retention; enable zero retention or approve a justified alternative; verify BAA and safeguards |
| 5 | AI sales-call recorder/transcriber with no customer notice (live) | High, pending full legal/privacy review | Pause recording until compliant | Determine applicable recording-notice and consent requirements; implement notice/consent and appropriate data-handling controls |

**Classification notes:** A public chatbot's classification can increase if it gives consequential clinical guidance. Patient identifiers are not automatically ePHI in every context; the scenario's production-log context warrants investigation. Clinic patient volumes/incidents are not automatically ePHI. Recording legality depends on the jurisdictions and circumstances; noncompliance is a material risk to investigate, not a legal conclusion.

## First investigation priority

**Case 5 — Sales recording.** Undisclosed recording is an active practice with potential consent, privacy, litigation, and business-continuity exposure. Immediately establish the relevant jurisdictions, what notices/consents exist, which calls and data are retained, and whether recording should remain paused pending remediation.

## Universal AI governance rules (under 100 words combined)

1. **Risk assessment:** Every AI system requires a documented pre-deployment risk assessment, periodic reassessment, and additional review after material changes.
2. **Data protection:** Employees may submit confidential information, PII, or ePHI only to AI systems explicitly approved for that data, with verified safeguards.
3. **Human oversight:** AI systems influencing consequential decisions require accountable human reviewers with authority to review, challenge, and override outcomes before they take effect.

## Bonus — HR screener

A vendor's claim that its model is unbiased is **not independent evidence** of fairness. Automated rejection should not resume without qualified human review of adverse outcomes, documented job-related criteria, and credible bias testing.

## Learning and defensibility notes

**Original insights from the exercise:** Data masking for logs; pre-launch audit of the ePHI summarizer; potential business-continuity impact of undisclosed call recording; baseline risk assessment and recalibration; need for human oversight.

**Areas refined during guided review:** The HR screener was initially rated Medium but must be High under the supplied rubric because it makes hiring decisions. Approval conditions were made more precise, particularly human review before rejection and verification of vendor data handling.

**Not claimed:** No production audit, regulatory determination, vendor assessment, bias test, or technical control implementation was performed in this exercise.

## Interview defense prompts

1. Why does a hiring decision make an AI system High risk even without evidence of bias?
2. What evidence would prove masking works before logs are sent to a coding assistant?
3. Why is a signed BAA insufficient by itself to authorize a clinical AI launch?
4. What facts would you gather before concluding call recording violates applicable law?
5. When would you change the chatbot's Low classification?
