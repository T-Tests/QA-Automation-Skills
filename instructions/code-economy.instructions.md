---
applyTo: '**/*.{js,ts,jsx,tsx,py,java,kt,cs,go,rb}'
---

# Code economy and quality

- If the ponytail skill is installed, invoke it for every code generation or edit. Don't restate its rules here.
- Otherwise, check in order and stop at the first that fits: does it need to exist, the standard library, a native framework or platform feature, an already-installed dependency, a one-liner, then the minimum correct code.
- Never cut input validation at trust boundaries, error handling, security checks, or accessibility for brevity.
- Mark a shortcut that has a known limit with a one-line comment: what was simplified, the limit, and what would trigger an upgrade. If ponytail is installed, keep its marker format so `ponytail-debt` can list them.
- Follow the file's existing conventions, naming, and error-handling style.
- No dead code and no commented-out code. Don't silence a linter or type warning to make something pass.
- Before calling work done, run the project's linter, type checker, and the relevant tests, and report the result. If you can't run them, say "not run".
- Keep changes localized. Don't rewrite working code for style.
