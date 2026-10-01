# Lab 06 — Reviewing and Recertifying Employee Access

**Vandelay Health** is a fictional healthcare technology company headquartered in Santa Monica, California and the company behind the **Ninja Sleeper** — an ultra-light, compact and virtually noiseless CPAP system designed for travelers who need to sleep comfortably in flight without disturbing fellow passengers.

The technology behind the Ninja Sleeper began as a **federal government contract project**, developed to provide military personnel in the field with a quiet and highly portable sleep-apnea solution. Vandelay Health later adapted the technology for the commercial market, incorporating as much of the original proprietary intellectual property as possible into the consumer Ninja Sleeper platform.

---

## Business Scenario

Following the expansion of Vandelay Health's Toronto Innovation Center, I needed to verify that employees with Toronto access still had a legitimate business need for it.

During the review, I identified **Lisa Brock**, who was on an extended leave of absence with no confirmed return date. Lisa remained an employee, so disabling her identity wasn't appropriate, but she no longer had a current need for Toronto Innovation Center access.

Rather than removing her access as a one-off administrative change, I used **Microsoft Entra Access Reviews** to recertify the entire Toronto access group. This gave me a documented process for reviewing each user's access, recording approval or denial decisions, removing access that was no longer justified, and retaining evidence of the review.


---

## IAM Requirements

For the Toronto access recertification, I needed to:

- Review membership in `SG-IC-Users` and determine whether each user still had a legitimate business need for access.
- Establish an accountable reviewer and a fallback reviewer so the certification could proceed if the resource owner was unavailable.
- Use sign-in activity as **decision support**, while keeping the final access decision based on business context.
- Require justification for review decisions and retain evidence of the certification process.
- Preserve access for employees with a continuing business need while removing Lisa Brock's Toronto entitlement without disabling her workforce identity.
- Apply the completed review decisions to the governed resource.
- Verify that denied access was actually removed.


---

## Implementation

### 1. Configure the Access Review

I created a **Microsoft Entra Access Review** to recertify membership in `SG-IC-Users`.

I configured the review with:

- **Review scope:** All users
- **Reviewer:** Resource owner
- **Fallback reviewer:** Configured
- **Duration:** 3 days
- **Recurrence:** One time
- **Auto-apply results:** Enabled
- **No reviewer response:** No change
- **30-day sign-in inactivity decision helper:** Enabled
- **Reviewer justification:** Required
- **Email notifications:** Enabled
- **Reminders:** Enabled

The reviewer was responsible for determining whether each employee still had a legitimate business need for Toronto access.

![Access Review Settings](01-access-review-settings-CLEAN.png)

---

### 2. Establish the Initial Review Population

The access review identified **five members of `SG-IC-Users`** who required recertification.

All five began the review without a decision, giving me the population I needed to evaluate for continued Toronto access.

---

### 3. Establish Reviewer Accountability

I configured the review so the **resource owner** was responsible for deciding whether each user's access remained appropriate.

When the resource owner wasn't available to perform the review, I used the configured **fallback reviewer** to keep the certification process moving through Microsoft My Access.

This demonstrated why a fallback reviewer matters: without one, an unavailable resource owner can delay or stall an access review.

![Assigned Access Review](06-myaccess-access-review-assigned-CLEAN.png)

---

### 4. Review the Access Population

I reviewed all five members of `SG-IC-Users` through Microsoft My Access.

Microsoft Entra displayed sign-in activity as a decision helper and recommended **Deny** for all five users because the lab identities lacked recent sign-in activity.

I did not automatically accept those recommendations. I used the inactivity data as supporting evidence and evaluated each user's actual business need for Toronto access before making the final decision.

![Pending Access Decisions](07-access-review-pending-decisions-CLEAN.png)

---

### 5. Record Certification Decisions

After reviewing the five identities, I recorded the following decisions:

| **User** | **Decision** |
|---|---|
| Jay Martin | Approved |
| Lisa Brock | **Denied** |
| Lori Van Meter | Approved |
| Paul Merson | Approved |
| Sandra Melancon | Approved |

I approved the four employees who still had a business need for Toronto access despite Entra's inactivity recommendation.

I denied Lisa Brock's Toronto access because she was on extended leave and did not currently require the entitlement. I left her Microsoft Entra identity intact because she remained a Vandelay Health employee.

This was an **access change, not an identity termination**.

I also recorded reviewer justification so the certification retained the business rationale behind each decision.

---

### 6. Validate the Completed Review

After completing the certification, I checked the Microsoft Entra administrative view to verify that all five users had been reviewed.

Final results:

- **5 users reviewed**
- **4 approved**
- **1 denied**
- **0 not reviewed**
- **0 don't know**

This confirmed that the review was complete and no certification decisions remained outstanding.

![Completed Access Review](09-access-review-completed-decisions-CLEAN.png)

---

### 7. Review the Audit Evidence

Microsoft Entra audit logs were reviewed to confirm that the access-review activity was recorded by the identity governance platform.

The audit trail provides traceability for:

- Reviewer accountability
- Control validation
- Compliance review
- Investigation of access changes
- Internal and external audit evidence

This provides evidence that the certification occurred through Vandelay's formal identity governance process rather than through an undocumented manual access change.

![Access Review Audit Log](10-access-review-audit-log-CLEAN.png)

---

### 8. Verify Access Remediation

Because **Auto apply results to resource** was enabled, the denied certification decision was applied to `SG-IC-Users`.

The group's membership was independently reviewed after remediation.

Four members remained:

- Jay Martin
- Lori Van Meter
- Paul Merson
- Sandra Melancon

Lisa Brock was no longer a member.

Her underlying Microsoft Entra identity remained intact because she was still associated with Vandelay Health.

![Remediation Verification](12-remediation-verified-group-membership-CLEAN.png)

---

## Validation

The completed governance process confirmed that:

- All five identities received a certification decision.
- Four employees retained access based on continuing business need.
- Lisa Brock's Toronto entitlement was denied.
- Lisa's underlying workforce identity was retained.
- Automated inactivity recommendations did not override documented business context.
- Reviewer justification was captured.
- No certification decisions remained outstanding.
- The denied entitlement was automatically remediated.
- Lisa was independently confirmed as removed from `SG-IC-Users`.
- Microsoft Entra retained audit evidence of the governance activity.

The end-to-end control can be summarized as:

**Identify access → Assign accountability → Review business need → Certify access → Document decisions → Remediate unnecessary access → Verify the outcome**

---

## IAM Controls Demonstrated

- **Access Reviews** — periodically evaluate whether existing access remains appropriate.
- **Access recertification** — require an accountable reviewer to approve or deny continued access.
- **Entitlement lifecycle management** — remove access without unnecessarily terminating the underlying identity.
- **Reviewer accountability** — associate access decisions with responsible business reviewers.
- **Fallback review** — maintain the certification process when the primary resource owner is unavailable.
- **Decision support** — use identity telemetry to inform rather than replace business judgment.
- **Reviewer justification** — document the business rationale supporting access decisions.
- **Automated remediation** — apply denied certification results to the governed resource.
- **Least privilege** — remove access when a current business requirement no longer exists.
- **Audit evidence** — retain traceable records of governance activity.
- **Post-remediation validation** — verify that a governance decision produced the intended access change.

---

## Key Takeaway

Access that was appropriate when it was granted may not remain appropriate indefinitely.

This lab demonstrates how Vandelay Health can use **Microsoft Entra Access Reviews to periodically recertify access, require accountable business decisions, remediate unnecessary entitlements, and retain evidence that the governance control actually worked**.

Lisa Brock's case also demonstrates an important distinction: **identity lifecycle and entitlement lifecycle are related, but they are not the same thing**. Her employment relationship with Vandelay has not ended, but her current need for Toronto access has changed.
