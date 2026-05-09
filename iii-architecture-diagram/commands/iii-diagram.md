---
description: Generate a standalone iii architecture diagram (SVG, optional PNG)
---
Load the iii-architecture-diagram skill. Generate a single architecture / mesh / layer-stack / state-machine / editorial SVG diagram for: $@

Read in order before drawing:

1. `SKILL.md` — philosophy + when-to-use.
2. `references/tokens.md` — brand colors and typography.
3. `references/svg-grammar.md` — type tags, ghost numerals, masked arrows, 4px grid, complexity budget.
4. `references/patterns.md` — pick ONE pattern. Don't hybridize.

Then:

- Copy the matching `templates/<pattern>-cream.svg` (or `-dark.svg`) as a scaffold.
- Edit text only — node names, type tags, arrow labels, ghost numeral, title, subtitle, eyebrow, legend, colophon.
- Keep the geometry. The 4px grid is non-negotiable.
- Honor the complexity budget: ≤9 nodes, ≤2 focal, ≤12 arrows, ≤5 type tags.

Before declaring done, walk every checkbox in `references/checklist.md`. Refuse to ship if anything in `references/anti-patterns.md` is on the page.

Output `<project>-architecture.svg` next to the source files. If the user wants a raster: `rsvg-convert -w 3840 -o <project>-architecture.png <project>-architecture.svg`.
