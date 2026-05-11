---
description: Generate a single-page iii system reference infographic for a project
---
Load the iii-infographic skill. Build a single-page system reference for: $@ (a project path or repo URL).

Read in order before writing HTML:

1. `SKILL.md` — when-to-use and workflow.
2. `references/inventory.md` — run the inventory pass on the project. Capture every registered function, trigger, KV scope, port, env flag, and formula. Build the verification fact-sheet with `file:line` citations.
3. `references/tokens.md` — color and typography tokens.
4. `references/sections.md` — pick six to eight sections from §01–§08 in canonical order.

Then:

- Open `templates/index.html` as the scaffold (it already wires up the topnav theme cycle, header, and four sections).
- Pull additional snippets from `templates/section-snippets/*.html` for any sections beyond what the scaffold ships.
- Replace placeholders with values from the fact-sheet. Every count traces to a source file or the boot log.
- Pick the binary axis (`--accent` paid/composable vs `--signal` free/built-in) and bind it in the legend.

Before declaring done, walk every checkbox in `references/checklist.md`. Refuse anything in `references/anti-patterns.md`.

Output: one self-contained `<project>-system-reference.html`. Open in a browser to verify cream ↔ dark theme cycle persists.
