---
applyTo: '**/*.{js,ts,jsx,tsx,py,java,kt,cs,go,rb}'
---

# Code safety

## Security
- Never hardcode secrets, tokens, passwords, or keys. Read them from environment variables or a secret manager. Never print or log them, including in test output and CI logs.
- Validate external input at trust boundaries. Use parameterized queries. Never build SQL or shell commands from strings, and never `eval` or `exec` untrusted input.
- Never disable TLS or certificate verification to make something work.
- Use synthetic test data. Never use real customer data or production credentials.
- Don't broaden permissions to make something work.
- Handle errors explicitly. Never swallow them, and don't expose sensitive details in error messages.

## Dependencies
- Before adding a package, verify it exists in the official registry and is the one you intend. AI tools can invent plausible package names, and attackers register them. Prefer what is already installed. Ask before adding.

## Accuracy
- Use only APIs, flags, and config keys you have seen in the code, the lockfile version, or that version's docs. If unsure, check the code or docs, or say so. Never invent them.
