---
name: iii-architecture-diagram
description: Standalone architecture diagrams for iii projects. Output is `.svg` (+ optional `.png` via rsvg-convert). One focal element per diagram, max 9 nodes, ember accent reserved for the iii primary path. Cream paper canvas, Inter Tight + JetBrains Mono, type tags above every node, arrow labels masked. Use when the user asks for a diagram (SVG or PNG) of an iii deployment, a worker, or any inter-worker dataflow on iii (iii.dev).
license: Apache-2.0
metadata:
  version: "3.2"
  author: iii (https://iii.dev)
  brand: iii
---

# iii Architecture Diagram Skill

Generates a STANDALONE architecture diagram as `.svg`. Renders to `.png` via `rsvg-convert`.

```text
<slug>-architecture.svg     # vector, primary
<slug>-architecture.png     # 2x raster, ~3840px, optional
```

`<slug>` is derived from the user's prompt or the working-directory basename; see `commands/iii-diagram.md` for the deterministic rule.

The SVG embeds its own `<style>` block. Fonts use `font-family="JetBrains Mono, Menlo, ui-monospace, monospace"` and `Inter Tight, system-ui, sans-serif` so `rsvg-convert` falls back gracefully without Google Fonts loaded. No HTML wrapper, no JavaScript. Just the diagram.

## Philosophy

The highest-quality move is deletion.

- Every node is a distinct idea. Two nodes that always travel together are one node.
- Every arrow carries information. If the relationship is obvious from layout, remove the line.
- Ember is editorial, not a flag. **One focal element per diagram, two max.** Embering five nodes erases the signal.
- The diagram isn't done when everything is added. It's done when nothing more can be removed.

**Target density: 4/10.** Not 9/10. Above 9 nodes, it's two diagrams.

## When to use

- User asks for "a diagram" of an iii deployment, worker, or dataflow.
- One focal worker plus 3–5 supporting workers / surfaces.
- Inter-worker `iii.trigger(...)` flow with one primary path highlighted.

## When NOT to use

- Multi-section system reference (tables, formulas, boot log). Use `iii-infographic`.
- A complete worker fleet > 9 boxes. Split into overview + per-worker detail.
- A list of things. Use a table or bullet list.
- A talk deck. Use `iii-slides`.

Before drawing, ask: *would the reader learn more from this than from a well-written paragraph?* If no, don't draw.

## Workflow

1. Pick a pattern from `references/patterns.md`. Don't hybridize.
2. Copy the matching `templates/<pattern>-{cream,dark}.svg` as a starting scaffold.
3. Read `references/tokens.md` and `references/svg-grammar.md` for the brand contract.
4. Edit text only — geometry is correct in the templates.
5. Run `references/checklist.md` before declaring done.
6. Refuse to ship if any item in `references/anti-patterns.md` applies.

## References

| File | Covers |
|---|---|
| `references/tokens.md` | Color palette, typography, cream → dark substitution |
| `references/svg-grammar.md` | Type tags, ghost numerals, arrow rules, z-order, 4px grid, page layout, complexity budget |
| `references/patterns.md` | Five canonical patterns and how to pick |
| `references/checklist.md` | Pre-output gate and PNG render command |
| `references/anti-patterns.md` | Refuse-to-ship list |
| `references/external-svgs.md` | Where to fetch real product/brand SVG logos (svgl, simpleicons, lucide) when a node refers to an external product |

Templates in `templates/*.svg` — copy, edit, ship.

## Commands

`commands/iii-diagram.md` is the entrypoint. Surfaces as `/iii-diagram <topic>` in Claude Code, namespaced as `/iii-architecture-diagram:iii-diagram` in plugin form.

## iii context

For canonical iii primitive semantics (`iii.register_function`, `iii.trigger`, worker registration, trigger types), see [iii.dev/docs](https://iii.dev/docs).
