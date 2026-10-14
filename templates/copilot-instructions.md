<!--
Template for .github/copilot-instructions.md in YOUR repo.
This file is sent with every request, so keep it short.
Fill in the bracketed lines and delete this comment.
-->

# Copilot instructions

## Project
- Build: `[build command]`
- Test: `[test command]`
- Layout: [one line on where source and tests live]
- Conventions: see [CONTRIBUTING.md]

## Working rules
- Be concise. Give the smallest response that fully answers the request.
- For any code generation or edit, invoke the ponytail skill if installed. Otherwise write the smallest correct implementation.
- Don't guess. Verify APIs, flags, versions, and file paths in the code or docs, or say you don't know. Never invent them. End with a one-line list of assumptions, and ask first when a wrong guess is costly.
- Look only at the relevant area. Don't re-read files already in context. Filter command output (grep, tail) before reading it. Don't paste large blocks back.
- State what you verified (tests run, code read) versus what you assume. Don't claim untested code works.
- Docs: 1-3 sentences of what and why. Prefer tables or bullets over paragraphs.
