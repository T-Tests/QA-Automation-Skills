---
name: test-strategy
description: 'Formulate test strategy, scope, risk analysis, and resource plans for features, releases, or projects. Use when asked for a test strategy, quality plan, test approach, risk mitigation, or QA estimate. Keywords: test strategy, test plan, quality approach, risk assessment, QA roadmap.'
compatibility: 'Works in plain chat with pasted input.'
---

# Test Strategy

Follow the role and platform settings. If unset, default to lead and detect the platform.

Lead with the core risk, proposed scope boundary, and the go/no-go criteria.

## Process
1. Scope boundaries: define what is in scope and explicitly what is out of scope. Never default to testing everything.
2. Risk assessment: map capabilities by likelihood and business impact (high, medium, low). Focus effort on high-impact failure modes.
3. Test levels: allocate coverage across unit, integration, API, UI, and manual exploratory based on cost and feedback speed.
4. Entry and exit criteria: define measurable gating conditions for starting test phases and release sign-off.
5. Environments and data: state prerequisites for test beds, device access, synthetic data sets, and third-party stubs.
6. Assumptions and dependencies: list unverified external dependencies and key operational assumptions.

## Platform specifics
- Mobile: minimum supported OS versions, top device tiers, network throttling, battery/thermal constraints, store submission lead times.
- Web: browser compatibility matrix, viewport breakpoints, accessibility compliance level (WCAG), CDN/caching invalidation.

If team size, timeline, or architecture is not supplied, state the planning assumption or ask before committing estimates.
