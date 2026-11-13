---
name: qa-metrics
description: 'Analyze QA metrics, defect leakage, test efficiency, and quality trends to produce actionable leadership summaries. Use when asked for QA dashboards, defect density, escape rate, test execution status, or ROI reports. Keywords: QA metrics, defect density, defect removal efficiency, test velocity, quality trends, QA dashboard.'
compatibility: 'Works in plain chat with pasted input.'
---

# QA Metrics

Follow the role and platform settings. If unset, default to manager and detect the platform.

Open with the executive conclusion: overall quality health, top risk trend, and immediate decision required.

## Analysis
1. Executive summary: one-page distillation of current quality state, trend direction (improving, flat, degrading), and key bottleneck.
2. Core indicators:
   - Defect metrics: arrival rate, closure rate, defect leakage (escape rate), severity distribution.
   - Test execution: run completion rate, first-pass pass rate, flakiness index.
   - Automation ROI: time saved per cycle, maintenance overhead, execution duration.
3. Root cause trends: identify systemic failure patterns (unclear requirements, environment instability, test data gaps).
4. Actionable recommendations: pair every highlighted negative trend with a concrete process or engineering intervention.

## Platform specifics
- Mobile: crash-free user and session percentages, ANR rates, app launch latency, App Store and Play Store review sentiment trends.
- Web: Core Web Vitals (LCP, FID/INP, CLS), browser-specific defect distribution, client-side JavaScript error budgets.

Compute calculations strictly from supplied raw counts. If inputs are missing, mark them as UNVERIFIED; do not estimate or invent baseline figures.
