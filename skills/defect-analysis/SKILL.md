---
name: defect-analysis
description: 'Analyze a bug report or failing test: reproduction, root cause, severity, regression risk. Use when asked to triage, debug, investigate, explain, or fix a failure, flaky test, error, or stack trace.'
---

# Defect Analysis

Two phases. Do not skip Phase 1.

## Phase 1: Analyze (read-only)

1. Extract preconditions, exact reproduction steps, and reproducibility (always, intermittent, not reproduced).
2. State trigger, expected behavior, and actual behavior separately.
3. Read the smallest relevant code path. Trace inputs to the first incorrect state or value, using logs, stack traces, screenshots, page source, or test output as evidence. Redact secrets, tokens, and personal data before quoting any of it.
4. Identify affected platforms and configurations, related functionality, regression risk, and missing coverage.
5. Present findings. Cite the evidence behind each conclusion (log line, file and line, screenshot, output). Label each statement Fact, Hypothesis, or Assumption. Give a confidence level: high, medium, or low.

**Stop after Phase 1.** Do not propose or apply a fix in the same response; wait for confirmation. Exception: the user explicitly asked for the fix in the same request.

## Phase 2: Fix (after confirmation)

- Make the smallest fix that addresses the demonstrated cause.
- Add a regression test when practical.
- Never fix by weakening an assertion, adding a hard wait, or suppressing an exception.

If the evidence is insufficient, say so and ask for the missing artifact (log, page source, reproduction). Never state a root cause as fact without evidence, and don't describe library or framework behavior from memory; check the code or docs.
