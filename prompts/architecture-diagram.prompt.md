---
description: Generate a Mermaid diagram of how the codebase, or a named part of it, fits together.
---

Inspect the workspace (or only the folder or module the user named) and draw how it works.

1. Identify the top-level modules, packages, or services and how they call or import each other.
2. Identify the entry points (CLI command, server start, test runner) and the main data or request flow.
3. Pick the diagram type: `graph TD` for module structure, `sequenceDiagram` for a request or test-run flow, `flowchart` for branching processes such as a CI pipeline.
4. Keep it to the 8-15 most important nodes. Fold minor helpers into their parent node's label.
5. Include only modules you actually found in the code. Don't guess.
6. Output one ```mermaid block, then at most 5 bullets for what the diagram can't show (async boundaries, external services, config-driven behavior).

Don't restate the diagram in prose.
