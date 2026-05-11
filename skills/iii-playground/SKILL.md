---
name: iii-playground
description: Generate a single-file, throwaway HTML editor for a specific task — drag-and-drop kanban, slider tuner, form editor, split-preview, or annotation canvas. Always ends in a "copy as prompt" or "copy as JSON" button so the user can paste the result back into the agent. Same iii editorial register as the architecture, infographic, and slides skills — cream paper or warm dark, Inter Tight + JetBrains Mono, ember accent on the export action. Use when the user asks for a tuner, a sliders panel, a draggable interface, a custom editor, a triage UI, or any one-off interactive HTML to manipulate values they'll feed back into the agent.
license: Apache-2.0
metadata:
  version: "1.0"
  author: iii (https://iii.dev)
  brand: iii
---

# iii Playground Skill

Generates a single-file HTML page that lets the user manipulate values, then exports the result back to the agent via a `copy as prompt` or `copy as JSON` button. The page is throwaway by design — no build step, no framework, vanilla JS only. Same iii editorial register as the rest of the bundle.

## When to use

- The user is reordering, triaging, or bucketing items (tickets, test cases, feedback, todos).
- The user is tuning numeric values that are painful to express in text (animation parameters, easing curves, color, cron expressions, regex, weight matrices).
- The user is editing structured config with constraints (feature flags, env vars, JSON/YAML with dependencies).
- The user is curating a dataset (approve/reject/tag rows).
- The user is annotating a document, transcript, or diff and exporting annotations.
- The agent is iterating on a prompt, copy, or template with live preview.

## When NOT to use

- The output is a long-lived product feature. Build the real thing in the project's actual stack, not a playground.
- The output is a static deliverable (diagram, page, deck). Use `iii-architecture-diagram`, `iii-infographic`, or `iii-slides`.
- The user wants persistence beyond their browser session. The playground is single-session by default.
- The use case has zero export action. A playground without an export button is just a static page.

## Workflow

1. **Pick a pattern** — `references/patterns.md`. Five patterns: kanban, tuner, form-editor, split-preview, curate. Pick exactly one.
2. **Decide the export shape** — what does the user copy back to the agent? A list, a JSON blob, a prompt fragment, a diff. State this up-front.
3. **Open the scaffold** — `templates/playground.html` ships a working tuner with the topnav, two-column body, sticky export bar, and theme cycle wired.
4. **Pull a snippet** — `templates/playground-snippets/<pattern>.html` swaps the body for the chosen pattern.
5. **Wire the export** — exactly one `[copy as prompt]` button (ember) plus optional `[copy as JSON]` (neutral). Both write to clipboard via `navigator.clipboard.writeText`.
6. **Walk the checklist** — `references/checklist.md`. Refuse anything in `references/anti-patterns.md`.

## References

| File | Covers |
|---|---|
| `references/tokens.md` | Color, typography, density (shared with the rest of the bundle) |
| `references/playground-grammar.md` | Page frame, sticky export bar, vanilla-JS rules, state model, clipboard pattern |
| `references/patterns.md` | Five patterns and when to pick each |
| `references/checklist.md` | Pre-output gate |
| `references/anti-patterns.md` | Refuse-to-ship list |

Templates in `templates/playground.html` + `templates/playground-snippets/*.html`.

## Commands

`commands/iii-playground.md` is the entrypoint. Surfaces as `/iii-playground <task>` in Claude Code, namespaced as `/iii-playground:iii-playground` in plugin form.

## iii context

For canonical iii primitive semantics (`iii.registerFunction`, `iii.registerTrigger`, worker registration, trigger types), see [iii.dev/docs](https://iii.dev/docs).
