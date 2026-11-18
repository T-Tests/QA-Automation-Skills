# Contributor guide

This repo is a catalog of Markdown files. There is no build, lint, or test system.

## File rules

| Type | Location | Name | Required frontmatter |
|---|---|---|---|
| Skill | `skills/<name>/SKILL.md` | lowercase-hyphens, max 64 chars, matches folder | `name`, `description` |
| Agent | `agents/<name>.agent.md` | lowercase-hyphens | `description` (`name` recommended) |
| Instruction | `instructions/<name>.instructions.md` | lowercase-hyphens | `applyTo` |
| Prompt | `prompts/<name>.prompt.md` | lowercase-hyphens | `description` |

## Style

- Keep files short. A skill is a playbook, not a tutorial; aim for under 60 lines.
- Skill descriptions state WHAT it does, WHEN to use it, and the KEYWORDS a user would type. The description is what decides whether the skill loads.
- Don't pin `model` in any frontmatter.
- Omit `tools` unless needed; tool names differ between IDEs.
- Every agent has a Constitution section with MUST DO and WON'T DO lists.
- Keep always-on text (the copilot-instructions template) minimal. Put detail in skills, which load on demand.
- Don't duplicate rules across files. Link or reference by name.
- No secrets, tokens, or internal URLs.
- Third-party skills (such as the mandated ponytail skill) are referenced by name only; never copy their content here. Scan any external skill with SkillSpector before referencing it.
- Each skill states its environment tier in a `compatibility:` frontmatter line (`Works in plain chat with pasted input.`, `Needs read access to the project files.`, or `Needs project files and a shell to run tests.`). If a target tool ignores this key, place the same line as the first body line.
- Each non-`chat` skill opens with a capability check: if the environment lacks what it needs, state that in one line, name the chat-safe alternative, and ask for pasted input.
- Exception to the no-duplication rule: `chat/qa-assistant.md` is a hand-maintained condensed copy of all chat-tier skills. Its header names the source skills so they are updated together.
