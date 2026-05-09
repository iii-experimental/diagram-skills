---
description: Generate a single-file iii playground — throwaway HTML editor with copy-as-prompt export
---
Load the iii-playground skill. Generate a throwaway HTML editor for: $@ (the task the user wants to manipulate values for).

Read in order before writing HTML:

1. `SKILL.md` — when-to-use and workflow.
2. `references/patterns.md` — pick exactly ONE pattern: kanban, tuner, form-editor, split-preview, or curate.
3. `references/tokens.md` — color and typography tokens (shared with the rest of the bundle).
4. `references/playground-grammar.md` — page frame, sticky export bar, vanilla-JS rules, state model, clipboard pattern.

Then:

- Decide the export shape **before** writing HTML. What does the user copy back to the agent? A list, a JSON blob, a prompt fragment, a diff. State this in a comment at the top of the file.
- Open `templates/playground.html` as the scaffold (topnav theme cycle, title block, sticky export bar wired).
- Swap the body for the chosen pattern's snippet from `templates/playground-snippets/<pattern>.html`.
- Wire `[copy as prompt]` (ember, primary) and optionally `[copy as JSON]` (neutral). Both write via `navigator.clipboard.writeText` and flash a `signal`-green `copied` confirmation in the status slot.
- Pre-fill state from the user's input where possible — pre-sort tickets, pre-set sliders to current values, pre-fill the form from existing config.
- Keep state in a single `state` object. Every event handler ends with a single `render()` call.

Before declaring done, walk every checkbox in `references/checklist.md`. Refuse anything in `references/anti-patterns.md`.

Output: one self-contained `<task-slug>-playground.html`. Open in a browser. The user manipulates, clicks `[copy as prompt]`, pastes back into the agent.
