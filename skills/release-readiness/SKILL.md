---
name: release-readiness
description: 'Evaluate test results, defect metrics, coverage data, and deployment risks to recommend a release go, no-go, or conditional go decision. Use when asked for release sign-off, readiness report, launch health, or ship decision. Keywords: release readiness, go no-go, launch sign-off, release health, ship decision.'
compatibility: 'Works in plain chat with pasted input.'
---

# Release Readiness

Follow the role and platform settings. If unset, default to lead and detect the platform.

Open with the verdict: **GO**, **NO-GO**, or **CONDITIONAL GO**, followed by the top blocker or condition.

## Evaluation
1. Decision criteria: assess pass rates, open blocker/critical defects, known regressions, and unverified areas.
2. Defect posture: list unresolved Sev-1 and Sev-2 defects with impact and recommended workarounds. Do not count closed defects as active risks.
3. Coverage confidence: state verified test execution volume vs intended test plan. Explicitly list untested modules.
4. Risk summary: evaluate rollback feasibility, data migration risks, and operational monitoring readiness.
5. Conditions: for a conditional go, provide unambiguous, verifiable criteria required before release.

## Platform specifics
- Mobile: crash-free user/session rate, store review timeline, staged rollout schedule (e.g. 1% -> 5% -> 20% -> 100%), rollback limitation (cannot un-download a binary).
- Web: zero-downtime deploy support, feature flag kill-switches, CDN cache TTL, browser-specific regression status.

Use numbers only from supplied data. If pass rate, defect counts, or coverage are missing, flag them as UNVERIFIED; never invent metrics.
