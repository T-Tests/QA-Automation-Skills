---
applyTo: '**/*.{js,ts,jsx,tsx,py,java,kt,cs,go,rb}'
---

# Code economy and quality

- Mandate ponytail: invoke the ponytail skill for every code generation, edit, or refactor. Never write code without ponytail's economy constraints.
- Check in order and stop at the first that fits: does it need to exist, the standard library, a native framework or platform feature, an already-installed dependency, a one-liner, then the minimum correct code.
- Never cut input validation at trust boundaries, error handling, security checks, or accessibility for brevity.
- Mark any shortcut with a ponytail debt comment: what was simplified, the limit, and what triggers an upgrade, so `ponytail-debt` can track and audit it.
- Follow the file's existing conventions, naming, and error-handling style.
- No dead code and no commented-out code. Don't silence a linter or type warning to make something pass.
- Mandate RTK: before calling work done, run the project's linter, type checker, and tests through `rtk` (e.g., `rtk npm test`, `rtk pytest`), and report the compressed output. Never feed raw, uncompressed runner output to context. If you can't run them, say "not run".
- Keep changes localized. Don't rewrite working code for style.
