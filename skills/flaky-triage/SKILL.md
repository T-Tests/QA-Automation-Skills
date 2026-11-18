---
name: flaky-triage
description: 'Investigate, isolate, and remediate non-deterministic or intermittent automated test failures across UI, mobile, and API suites. Use when asked to fix flaky tests, intermittent failures, race conditions, or stale elements. Keywords: flaky test, flaky triage, intermittent failure, race condition, stale element, test retry.'
compatibility: 'Needs project files and a shell to run tests repeatedly. Chat variant: paste logs and test code for root-cause hypothesis.'
---

# Flaky Triage

Needs project files and a shell to reproduce flakiness. In plain chat, paste the test code, failure logs, and run history for triage.

Follow the role and platform settings. If unset, default to engineer and detect the platform.

Inspect project files to detect the test runner and framework; never assume one.

## Triage hierarchy
1. Synchronization: evaluate race conditions between UI rendering and test execution. Look for implicit waits masking missing explicit waits.
2. Shared state: check for test pollution, shared static caches, leftover database records, or uncleaned local storage.
3. Order dependency: run the failing test in isolation, then in reverse suite order to detect predecessor coupling.
4. Environment & resources: check for CI container CPU throttling, memory spikes, or network flakiness.

## Fix rules
- Never fix with hard sleeps (`Thread.sleep`, `time.sleep`). Replace with condition-based explicit polling.
- Never fix by adding test-level retries without addressing the underlying race condition. Retries hide defects.
- Isolate test data: use unique UUID-stamped synthetic data per test run.
- Mandate RTK: execute repeated test triage runs through `rtk` (e.g. `rtk npm test`, `rtk pytest`) to compress output and reduce token context.
- Evidence before done: run the test repeatedly (e.g. 5-10 iterations) through `rtk` and display compressed execution output proving zero failures. If unable to run, state "not run".

## Platform specifics
- Mobile: Appium driver synchronization, Espresso idling resources, device animations enabled on emulator, keyboard dismissal latency.
- Web: DOM hydration races, stale element reference recovery, animation CSS transitions, browser tab storage cross-contamination.
