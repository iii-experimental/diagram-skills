---
description: Generate a single-file iii slide deck (scroll-snap, 100dvh per slide, cream + dark themes)
---
Load the iii-slides skill. Generate a slide deck for: $@ (a topic, plan file, or source document path).

Read in order before writing HTML:

1. `SKILL.md` — when-to-use and workflow.
2. `references/inventory.md` — enumerate every section, card, table row, decision, footnote in the source. Map each to ≥1 slide.
3. `references/tokens.md` — color and typography tokens (shared with iii-infographic).
4. `references/slide-grammar.md` — scroll-snap container, slide types, navigation chrome.

Then:

- Open `templates/deck.html` as the scaffold (scroll-snap container, topnav theme cycle, 3 sample slides).
- For each planned slide, pull a snippet from `templates/slide-snippets/{title,content,diagram,quote,two-column}.html`.
- Fill placeholders with values from the source. Numbers must trace to source files or boot-log lines.
- Pick the binary axis (`--accent` paid/composable vs `--signal` free/built-in) and bind it on the title slide's legend.
- Vary slide types across the sequence. Five identical content slides in a row is a deck failure.

Before declaring done, walk every checkbox in `references/checklist.md`. Refuse anything in `references/anti-patterns.md`.

The reader test: a reader who has never seen the source should be able to reconstruct every major point from the slides alone. If they'd miss sections, add slides.

Output: one self-contained `<project>-deck.html`. Open in Safari and Chrome to verify scroll-snap and theme persistence.
