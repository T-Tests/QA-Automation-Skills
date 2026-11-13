---
name: test-automation
description: 'Write, convert, or review automated tests for UI, API, mobile, and performance. Use when asked to automate a test case, create page objects, locators, API tests, test data, or load tests.'
compatibility: 'Needs project files and a shell to run tests.'
---

# Test Automation

Needs project files and a shell to run tests. For test case design without execution, use the test-design skill in chat with pasted requirements.

Follow the role and platform settings. If unset, default to engineer and detect the platform.

**Before writing:** inspect project files to detect the framework in use (for example Appium, XCUITest, Espresso, Playwright, Selenium, Cypress); never assume one. Reuse its existing utilities, page or screen objects, naming, and reporting. Don't duplicate selectors or helpers. Automate only stable scenarios with real maintenance value.

**Writing the code:** if the ponytail skill is available, invoke it. Otherwise write the smallest correct implementation: built-ins first, no speculative abstraction, no new dependency without a verified reason.

## Rules
- Never invent locators, IDs, endpoints, expected values, or test data. Use marked placeholders (such as `TODO_FILL_FROM_SOURCE`) and ask for real values. Never use empty strings for selectors.
- No hard waits. Use framework-native explicit synchronization.
- Keep test data deterministic and synthetic. No real credentials or production data.
- Read secrets from environment variables and mask them in logs. Never disable TLS verification.
- Failures must report what failed, where, and expected versus actual.
- Never weaken an assertion or add a sleep to make a test pass.
- Evidence before done: show test or lint execution output before reporting work complete. If unable to run, state "not run".
- One case per pass: write one test, run it, report the result, then proceed. Do not batch or loop script.

## Platform specifics
- Mobile: device and OS matrix, permissions, interruptions (calls, notifications), background and foreground, offline and weak network, deep links, build variants.
- Web: cross-browser, responsive layouts, accessibility, page performance.
