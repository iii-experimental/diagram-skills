---
name: iii-slides
description: Generate a single-file scroll-snap slide deck for an iii talk, demo, or design review. Same iii editorial register as the architecture and infographic skills — cream paper or warm dark, Inter Tight + JetBrains Mono, ember accent reserved for the binary axis. Each slide is exactly one viewport tall (100dvh). No auto-advance, no transitions on more than two elements, no marketing copy. Use when the user asks for a deck, a slide-deck, or a presentation about an iii project.
license: Apache-2.0
metadata:
  version: "1.0"
  author: iii (https://iii.dev)
  brand: iii
---

# iii Slides Skill

Generates a single-file HTML scroll-snap slide deck. The output is one self-contained `deck.html` with inline CSS and JS. The same iii editorial register as `iii-architecture-diagram` and `iii-infographic` — cream + dark themes, Inter Tight + JetBrains Mono, ember accent anchored to a binary axis.

## When to use

- The user explicitly asks for a deck, slides, or a presentation.
- The audience will scroll or click through one viewport at a time.
- The content fits the iii voice: numbers carry the prose, no marketing words.

## When NOT to use

- The deliverable is a single diagram. Use `iii-architecture-diagram`.
- The deliverable is a dense multi-section reference. Use `iii-infographic`.
- The user wants animated transitions or a presentation with auto-advance. The iii deck has neither.
- The content has no real numbers and would be a marketing page. Refuse.

## Workflow

1. **Inventory the source** — `references/inventory.md`. Count every section, decision, table row, footnote in the source document. Map each to ≥1 slide. A 7-section plan with 6 decisions is ~25 items, so the deck is 18–25 slides — not 10–13.
2. **Pick the binary axis** — the same `--accent` (paid / opt-in / composable) vs `--signal` (free / built-in / always-on) binding from `iii-infographic`. State it on the title slide's legend.
3. **Plan layouts** — for each slide, pick a slide type from `references/slide-grammar.md`: title, content, diagram, quote, two-column, data. Vary across the sequence.
4. **Open the scaffold** — `templates/deck.html` ships scroll-snap container + topnav theme cycle + 3 sample slides wired up.
5. **Pull snippets** — `templates/slide-snippets/{title,content,diagram,quote,two-column,data}.html` for additional slides.
6. **Walk the checklist** — `references/checklist.md`. Refuse anything in `references/anti-patterns.md`.

## References

| File | Covers |
|---|---|
| `references/tokens.md` | Color, typography, density (shared with `iii-infographic`) |
| `references/slide-grammar.md` | Scroll-snap container, 100dvh slides, slide types, type scale, navigation chrome |
| `references/inventory.md` | Source-document → slide mapping; the test for completeness |
| `references/checklist.md` | Pre-output gate |
| `references/anti-patterns.md` | Refuse-to-ship list |

Templates in `templates/deck.html` + `templates/slide-snippets/*.html`.

## Commands

`commands/iii-slides.md` is the entrypoint. Surfaces as `/iii-slides <topic-or-source-file>` in Claude Code.

## iii context

For canonical iii primitive semantics (`iii.registerFunction`, `iii.registerTrigger`, worker registration, trigger types), see [iii.dev/docs](https://iii.dev/docs).
