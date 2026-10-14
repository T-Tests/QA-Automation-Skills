---
name: test-automation
description: 'Write, convert, or review automated tests for UI, API, mobile, and performance. Use when asked to automate a test case, create page objects, locators, API tests, test data, or load tests.'
---

# Test Automation

**Before writing:** inspect the existing framework. Reuse its utilities, page or screen objects, naming, and reporting. Don't duplicate selectors or helpers. Automate only stable scenarios with real maintenance value, not every manual case.

**Writing the code:** if the ponytail skill is available, invoke it. Otherwise write the smallest correct implementation: built-ins first, no speculative abstraction, no new dependency without a reason.

## Rules

- Never invent locators, IDs, endpoints, expected values, or test data. If the real value isn't in the evidence (page source, inspector output, API spec, requirement), use a clearly marked placeholder such as `TODO_FILL_FROM_SOURCE` and ask for it. Never use an empty string; it can silently match the wrong element.
- No hard waits. Use explicit synchronization.
- Keep test data deterministic and synthetic. No real credentials or production data.
- Read secrets from environment variables and mask them in logs and reports. Never disable TLS verification to make a test pass.
- Failures must say what failed, where, and expected versus actual.
- Never weaken an assertion to make a test pass.

## By test type

**API:** validate meaning, not just status codes. Cover auth and authorization, request validation, response schema, error bodies, boundary, null and missing fields, idempotency, pagination, filtering, sorting, and data integrity.

**Mobile:** consider OS and device, permissions, lifecycle (background, force-close), network loss, notifications and deep links, locale and time zone, and accessibility. Use risk-based combinations, not the full matrix.

**Performance:** define workload, baseline, targets, concurrency, duration, and environment first. Distinguish latency, throughput, error rate, and saturation. Compare against a baseline; don't extrapolate a local run to production.
