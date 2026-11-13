# Evaluation tasks and scoring

Eight fixed tasks to measure quality and cost before and after changes. Run each task, score the output, and record tokens from the provider's usage view.

## Tasks

### T1 — Design test cases from a story (engineer, mobile, chat)

**Input:** "As a user I can reset my password via an in-app link that expires after 15 minutes. The link is sent by push notification on Android and iOS."

**Score:** requirement coverage, no invented APIs or locators, cases are reproducible, mobile concerns addressed (OS matrix, deep link, notification permission, background state, expiry edge).

### T2 — Write a test plan for a feature (lead, both, chat)

**Input:** "Plan testing for a new checkout flow that supports credit card and wallet payments on web and mobile apps. Launch in 4 weeks, 2 SDETs available."

**Score:** scope and risk priorities, resource and timeline realism, platform-specific risks named, no invented metrics, decision-ready format.

### T3 — Analyse a crash log (engineer, mobile, chat)

**Input:** Paste a real or representative Android crash log (NullPointerException in a RecyclerView adapter). If no log is available, use the placeholder below.

*Placeholder log (replace with a real one for accurate scoring):*
```
FATAL EXCEPTION: main
java.lang.NullPointerException: Attempt to invoke virtual method
  'int java.util.List.size()' on a null object reference
  at com.example.app.CartAdapter.getItemCount(CartAdapter.java:42)
  at androidx.recyclerview.widget.RecyclerView.dispatchLayoutStep1(RecyclerView.java:4085)
  ...
```

**Score:** correct root cause identification, evidence cited, facts vs hypotheses separated, no invented fix details, confidence stated, regression risk identified.

### T4 — Review a diff (engineer, web, chat)

**Input:** Paste a diff (20–60 lines) that contains at least one real bug and one style issue. If unavailable, use any recent PR diff from the team's repo.

**Score:** requirement checked first, bugs found, hallucinated APIs flagged, security check applied, findings grouped by severity, no false positives on valid code.

### T5 — Release-readiness summary (lead/manager, both, chat)

**Input:** "Sprint 14 results: 312 tests, 298 pass, 8 fail (3 blockers in checkout, 2 known flaky in notifications, 3 minor UI), 6 open bugs (2 P1), code coverage 74%, crash-free rate 99.1% Android / 99.4% iOS. Ship decision needed by Friday."

**Score:** decision-first format, no invented numbers beyond input, risk summary, blockers highlighted, recommendation with conditions, concise (under 300 words for manager view).

### T6 — Explain a flaky test to a fresher (fresher, web, chat)

**Input:** "This Selenium test for login fails about 30% of the time with StaleElementReferenceException on the submit button click. The test uses Thread.sleep(2000) before the click."

**Score:** explanation understandable to a fresher, learning note included, correct diagnosis (stale element + hard wait), suggested fix (explicit wait), no jargon without definition, terms explained.

### T7 — Generate an API test case (engineer, both, chat)

**Input:** "POST /api/v1/orders creates an order. Requires auth token. Body: {items: [{sku, qty}], address_id}. Returns 201 with order_id, or 400/401/422."

**Score:** cases cover auth, validation, boundary, error bodies, idempotency consideration, no invented endpoints or response fields, test data is synthetic.

### T8 — Mentor interview opening (fresher, files, files)

**Input:** Open the project-mentor agent on a real project and send "Start".

**Score:** one opening line (no project summary), first question references real code, level and mode stated, commands listed, question is approachable for a fresher.

## Scoring rubric

For each task, score 1–5 on each applicable dimension:

| Dimension | 1 (poor) | 3 (adequate) | 5 (excellent) |
|---|---|---|---|
| **Requirement coverage** | Major gaps, missing categories | Core covered, some gaps | Thorough, risk-prioritized, no excess |
| **Accuracy** | Invented APIs, locators, or data | Minor assumptions stated | Every claim backed by input or evidence |
| **Runnability** | Tests won't compile or are pseudocode | Would run with minor edits | Runs green as written (where applicable) |
| **Defects caught** | Missed the planted bug | Found it with wrong severity | Found it, correct severity, evidence cited |
| **Role fit** | Wrong audience level | Mostly right but verbose | Matches stated role perfectly |
| **Brevity** | Walls of text, greetings, recaps | Some padding | Conclusion first, no filler |

**Overall task score** = average of applicable dimensions (not all apply to every task).

## Token tracking

Record from the provider's usage view after each run. One row per task per configuration.

| Run ID | Date | Config | Task | Input tokens | Output tokens | Total tokens | Overall score | Notes |
|---|---|---|---|---|---|---|---|---|
| baseline-1 | | current repo, no changes | T1 | | | | | |
| baseline-1 | | current repo, no changes | T2 | | | | | |
| baseline-1 | | current repo, no changes | T3 | | | | | |
| baseline-1 | | current repo, no changes | T4 | | | | | |
| baseline-1 | | current repo, no changes | T5 | | | | | |
| baseline-1 | | current repo, no changes | T6 | | | | | |
| baseline-1 | | current repo, no changes | T7 | | | | | |
| baseline-1 | | current repo, no changes | T8 | | | | | |

## How to run a baseline

1. Install the current repo into your IDE (see `docs/setup.md`).
2. Run each task T1–T8 in a fresh chat session. Use the exact input above.
3. Record input and output tokens from the provider's usage view (Copilot: not exposed per-request; Claude Code: shown in the terminal; other providers: check their dashboard).
4. Score the output using the rubric. Be honest; if a dimension doesn't apply, skip it.
5. Fill in the table. The baseline row uses the current repo with no Phase 1+ changes.
6. After each phase, re-run changed tasks and add a new row set.

> [!IMPORTANT]
> Savings are never claimed, only measured. A new skill ships only if it scores equal or better than baseline on its applicable tasks without increasing total tokens.
