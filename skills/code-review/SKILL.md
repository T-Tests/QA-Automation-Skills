---
name: code-review
description: 'Review code or a diff for correctness, regressions, error handling, security, hallucinated APIs, test coverage, and maintainability. Use when asked to review a pull request, diff, change, or test code.'
---

# Code Review

Review in this order: correctness, behavioral regressions, error handling, security and data exposure, concurrency and state, test coverage, maintainability, performance, style.

## Checks

- **Security:** hardcoded secrets; injection (SQL, shell, eval); missing authentication or authorization; unvalidated input; disabled TLS verification; sensitive data in logs or error messages; unsafe deserialization.
- **Hallucination:** confirm every function, API, flag, and package the diff uses exists in the project or in the documented version. Flag any new dependency that wasn't verified.
- **Quality:** conventions followed; no dead code, duplication, or swallowed errors; formatter, linter, and tests run and reported.
- **Assumptions:** list any the author made without evidence.

If the ponytail-review skill is available, run it on the diff to catch over-engineering.

This skill reviews by reading. It is not a security scanner. For security-sensitive changes, recommend a dedicated scanner.

## Output

Group findings by severity: blocker, major, minor. For each, give the file and line, why it matters, and a suggested fix. Report actionable findings only. Raise style preferences only when they violate a stated project convention. If you find nothing, say so.
