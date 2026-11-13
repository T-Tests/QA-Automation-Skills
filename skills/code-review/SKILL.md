---
name: code-review
description: 'Review code or a diff for correctness, regressions, error handling, security, hallucinated APIs, test coverage, and maintainability. Use when asked to review a pull request, diff, change, or test code.'
compatibility: 'Works in plain chat with a pasted diff. With file access, can review against the full repo.'
---

# Code Review

Follow the role and platform settings. If unset, default to engineer and detect the platform.

Review against the requirement first, then in this order: correctness, behavioral regressions, error handling, security and data exposure, concurrency and state, test coverage, maintainability, performance, style.

## Checks
- **Security:** hardcoded secrets; injection (SQL, shell, eval); missing authentication/authorization; unvalidated input; disabled TLS verification; sensitive data in logs/errors; unsafe deserialization.
- **Hallucination:** confirm every function, API, flag, and package the diff uses exists in the project or documented version. Flag any unverified new dependency.
- **Quality:** conventions followed; no dead code or swallowed errors; linter and tests reported.
- **Assumptions:** list any the author made without evidence.

If the ponytail-review skill is available, run it on the diff to catch over-engineering.

## Verification
Run a second pass attempting to disprove each finding. Mark each as `confirmed` (assign severity: blocker, major, minor), `needs validation` (name the exact missing fact), or `rejected`. Keep hardening suggestions separate from confirmed defects.

## Platform specifics
- Mobile: lifecycle handling, main thread blocking, runtime permission checks, deep link validation.
- Web: DOM re-rendering, accessible labels and ARIA, cross-browser APIs, sensitive data in web storage.

## Output
Group confirmed findings by severity: blocker, major, minor. For each, give file and line, why it matters, and a suggested fix. If nothing found, say so.
