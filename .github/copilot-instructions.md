# Copilot instructions

## Project
- Build: none (Markdown-only catalog)
- Test: none
- Layout: `skills/` (playbooks), `agents/` (role definitions), `prompts/` (slash commands), `instructions/` (file-scoped rules), `chat/` (paste-ready chat pack), `templates/`, `docs/`
- Conventions: see [AGENTS.md](../AGENTS.md)

## Settings
- `role`: fresher | engineer | lead | manager (default: engineer). Fresher: explain terms and why, add a learning note. Engineer: terse artifact. Lead: risk, scope, decision. Manager: one-page summary first, decision needed, numbers only from supplied data.
- `platform`: mobile | web | both (default: detect from the project or ask once).
- Brevity: lead with the conclusion or decision needed, then detail. No greetings or recaps. Mentor notes and warnings are exempt.

## Working rules
- Follow the role and platform settings above. If unset, default to `engineer` and detect the platform.
- Be concise. Give the smallest response that fully answers the request.
- Mandate ponytail: for any code generation, edit, or refactor, invoke the mandatory ponytail skill. For reviews, invoke ponytail-review.
- Mandate RTK: always execute test runs, linters, and terminal commands through `rtk` (e.g. `rtk test`, `rtk run <cmd>`) to compress output and reduce context token bloat. Never feed raw uncompressed terminal output.
- Don't guess. Verify APIs, flags, versions, and file paths in the code or docs, or say you don't know. Never invent them. End with a one-line list of assumptions, and ask first when a wrong guess is costly.
- Look only at the relevant area. Don't re-read files already in context. Filter command output before reading it. Don't paste large blocks back.
- State what you verified (tests run via rtk, code read) versus what you assume. Don't claim untested code works.
- Docs: 1-3 sentences of what and why. Prefer tables or bullets over paragraphs.
