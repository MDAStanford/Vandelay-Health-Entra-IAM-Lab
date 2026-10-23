# Portfolio Documentation and AI-Assisted Workflow Standard

**Applies to:** Vandelay Health IAM labs and future scenario-based GRC exercises.

## Working agreement

- **Author owns:** Technical execution, configuration decisions, risk assessments, evidence interpretation, and ability to explain results.
- **AI assistant supports:** Repository organization, Markdown, screenshot links, repeatable templates, code/script drafting, troubleshooting hypotheses, and documentation consistency.
- **Verification rule:** Never describe AI-generated text, an untested script, or a proposed control as executed or validated. Mark unverified work explicitly.

## Standard lab layout

Existing lab paths stay unchanged. New labs may use:

```text
Lab-XX-Descriptive-Name/
  README.md
  evidence/
  scripts/
```

Only create folders when needed. Keep existing screenshot filenames and relative links intact; do not reorganize older lab assets without reviewing links first.

## README structure

1. **Scenario and business requirement** — why the work matters.
2. **Scope and environment** — fictional vs. actual lab tenant, relevant tools, and prerequisites.
3. **Risk and intended control** — threat, affected identities/data, and design choice.
4. **Implementation** — steps actually completed, commands/scripts, and configuration decisions.
5. **Evidence and validation** — screenshots or outputs with dates, expected vs. observed results.
6. **Troubleshooting and limitations** — failures, assumptions, unresolved issues.
7. **Outcome and lessons learned** — supported conclusions only.
8. **Interview defense questions** — 4–5 short written questions testing understanding.

## Evidence conventions

- Use descriptive screenshot names and relative Markdown links, e.g. `![Conditional Access policy evidence](evidence/conditional-access-policy.png)`.
- Do not invent evidence files or claim tests passed without supporting output.
- Remove secrets, tokens, personal identifiers, and sensitive data from screenshots and scripts.
- Label screenshots as **observed evidence**, diagrams as **illustrative**, and future actions as **proposed**.
- Preserve exact metrics and distinguish simulated populations from production scale.

## Review checklist

- [ ] Business problem and scope are clear.
- [ ] Steps described were actually performed.
- [ ] Claims match available evidence.
- [ ] Screenshot links resolve and captions explain what they prove.
- [ ] Scripts have prerequisites, safety notes, and validation instructions.
- [ ] Sensitive information is redacted.
- [ ] Unresolved issues and AI assistance are disclosed accurately.
- [ ] Author can answer 4–5 interview defense questions.

## Suggested AI-assisted review workflow

1. Author supplies the completed lab README, screenshots, and relevant scripts.
2. AI reviews structure, missing evidence, link consistency, and technical claims.
3. AI proposes changes and explicitly marks assumptions.
4. Author verifies the configuration and outcomes.
5. Changes are committed on a review branch before merging into `main`.

## Automation candidates (not yet implemented)

- Markdown link validation in GitHub Actions.
- Checks for missing referenced local images.
- README section consistency checks for new labs.
- Optional secret scanning and spelling checks.

**Status:** Documentation standard established; the automation candidates above are proposals, not active GitHub workflows.
