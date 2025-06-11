---
aliases:
  - RCA
tags:
  - incident
---
A Root Cause Analysis (RCA) is a structured document that answers:

- What happened?
- Why did it happen?
- What can we do to prevent it in the future?

A valid RCA document contains the following section:

## Summary

Write a short, non-technical paragraph explaining:

- What went wrong
- When it happened
- How it was resolved

**Example**:

> _On May 9th, a feature flag rollout caused the homepage and checkout to return 500 errors for 30% of users between 11:03 AM and 11:20 AM. The flag triggered a code path that overwhelmed an internal service, which had no retry or fallback. The issue was mitigated by rolling back the flag._

## Impact

Explain the **user and business impact**:

- How many users were affected?
- Was there data loss?
- What was the revenue/latency/cost implication?

**Example**:

- 500 errors for ~30% of traffic
- Checkout failures for logged-in users
- Revenue impact estimated at $18K
- No data loss, no security exposure

## Timeline of Events

Build a timeline with exact timestamps and key events.

![](https://miro.medium.com/v2/resize:fit:875/1*WIiC7NH2wSBHhYt1zBlmCw.png)

Tips:

- Stick to facts, not interpretations
- Use logs, alert timestamps, and monitoring data

## Root Cause Analysis (5 Whys)

Use the **5 Whys** to move from symptoms to root causes.

**Tip**: The 5 Whys depend on your ability to identify _systemic gaps_, _process failures_, or _human assumptions_.

Example:

1. **Why** were users seeing 500s?  
    → Because an internal API failed due to rate limits.
2. **Why** did it fail?  
    → Because traffic surged from a flag rollout.
3. **Why** wasn’t the API prepared for this load?  
    → Because it wasn’t load-tested for partial rollouts.
4. **Why** wasn’t load testing tied to flag rollouts?  
    → Because we lacked a defined launch checklist.
5. **Why** don’t we have a checklist?  
    → Because our deployment process doesn’t include flag readiness steps.

> _🎯_ **_Root Cause_**_: Missing rollout standards for feature flags and lack of capacity validation._

## Learnings

Summarize the _insights_ gained. Split into:

- What went wrong
- What worked
- What could have reduced the impact

**Example**:

**What went wrong:**

- Flag enabled at 50% without validating downstream impact
- No fallback for API failure
- Alerting was reactive, not proactive

**What worked:**

- Rapid rollback mechanism
- On-call rotation responded within SLA

**What could have helped:**

- Canary rollout strategy
- Monitoring for 429 errors
- Feature flag guardrails

## Action Items

Your most important section — **concrete steps** to prevent recurrence.

![](https://miro.medium.com/v2/resize:fit:875/1*MfRWy5pPuHIIK9qJZi_Ekg.png)

Tips:

- Assign owners and dates
- Track status (In Progress, Done, Blocked)

## Appendix

Attach graphs, logs, screenshots of alerts, etc. This provides supporting context without cluttering the main document.

---
[📘 The Ultimate Guide to Writing a Root Cause Analysis (RCA)](https://medium.com/@das.sudeept/the-ultimate-guide-to-writing-a-root-cause-analysis-rca-b678d5236174)