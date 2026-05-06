---
name: iii-architecture-diagram
description: Standalone architecture diagrams for iii projects. Output is `.svg` (+ optional `.png` via rsvg-convert). One focal element per diagram, max 9 nodes, ember accent reserved for the iii primary path. Cream paper canvas, Inter Tight + JetBrains Mono, type tags above every node, arrow labels masked. Use when the user asks for a diagram (SVG or PNG) of an iii deployment, a worker, or any inter-worker dataflow on iii (iii.dev).
license: Apache-2.0
metadata:
  version: "3.1"
  author: iii (https://iii.dev)
  brand: iii
---

# iii Architecture Diagram Skill

Generates a STANDALONE architecture diagram as `.svg`. Renders to `.png` via `rsvg-convert`.

```
<project>-architecture.svg     # vector, primary
<project>-architecture.png     # 2x raster, ~3840px, optional
```

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
- One focal worker plus 3-5 supporting workers / surfaces.
- Inter-worker `iii.trigger(...)` flow with one primary path highlighted.

## When NOT to use

- Multi-section system reference (tables, formulas, boot log). Use `iii-infographic`.
- A complete worker fleet > 9 boxes. Split into overview + per-worker detail.
- A list of things. Use a table or bullet list.

Before drawing, ask: *would the reader learn more from this than from a well-written paragraph?* If no, don't draw.

## Render to PNG

```bash
rsvg-convert -w 3840 -o agentos-architecture.png agentos-architecture.svg
# or via ImageMagick:
magick -density 200 agentos-architecture.svg agentos-architecture.png
```

`-w 3840` produces a crisp 2x raster of a `1920` viewBox. For 4k decks, `-w 4800`.

## Brand contract

```css
--paper:    #f2ede1;   /* iii cream canvas */
--ink:      #0c0b0a;
--muted:    rgba(12,11,10,0.74);
--soft:     rgba(12,11,10,0.50);
--rule:     rgba(12,11,10,0.14);
--accent:   #d9763a;   /* iii ember · the focal mark */
--acc-tint: rgba(217,118,58,0.10);
--link:     #2e5aa8;   /* HTTP / external request */
--signal:   #2f8f5a;   /* free / always-on path · optional */
```

Dark theme: swap canvas to `#0d0c0a` warm black, ink to `#efe9d8`, accent to `oklch(0.72 0.16 45)`. Same vocabulary either way.

The iii logo mark is monochrome. Never colorize the bars yellow.

## Typography

```
Inter Tight        — title, node names
JetBrains Mono     — type tags, sublabels, arrow labels, technical content
```

No serif. No italic for emphasis. Mono is for **technical** content (ports, function names, URLs, type tags, arrow verbs). Names go in Inter Tight.

| Element | Family | Size | Weight |
|---|---|---|---|
| Title | Inter Tight | 56–64px | 500 |
| Subtitle | JetBrains Mono | 14px | 400 |
| Eyebrow | JetBrains Mono | 12px, `letter-spacing: 3.5` | 400 |
| Node name | Inter Tight | 18–22px | 600–700 |
| Sublabel | JetBrains Mono | 11–12px | 400 |
| Type tag | JetBrains Mono | 9px, `letter-spacing: 1.2` | 400 |
| Arrow label | JetBrains Mono | 10px, `letter-spacing: 1.4` | 600–700 |

## Node treatment by semantic type

One row per type. Use the matching fill/stroke pair; don't invent new ones.

| Type | Fill | Stroke | Use for |
|---|---|---|---|
| **Focal** (1, max 2) | `--acc-tint` | `--accent` 1.6 | The iii primary path — the worker the diagram is about |
| **Worker** | `#ffffff` | `--ink` 1 | Sibling workers, backend functions |
| **Edge** | `ink @ 0.05` | `--soft` 1.2 | iii REST module, gateways, HTTP surfaces |
| **State / Store** | `ink @ 0.05` | `--soft` 1 | KV, streams, queue, durable adapters |
| **External** | `ink @ 0.03` | `--soft` 1.2 | Caller, browser, agent UI, third party |
| **Optional / Async** | `ink @ 0.02` | `--soft` 1, dashed `4 3` | Opt-in workers, async fan-out, conditional |
| **Security boundary** | transparent | `--accent` 1, dashed `4 4` | Auth, RBAC, namespace isolation |

The legend at the bottom of every diagram lists every type used and nothing else.

## Type tags (above every node)

Every node carries a small rectangular tag in its top-left corner. Tag border matches the node stroke; tag is **always rectangular `rx="2"` — never a pill**.

```svg
<rect x="92" y="492" width="36" height="16" rx="2" fill="transparent"
      stroke="rgba(12,11,10,0.30)" stroke-width="0.8"/>
<text x="110" y="503" font-family="JetBrains Mono, monospace"
      font-size="9" letter-spacing="1.2" text-anchor="middle"
      fill="rgba(12,11,10,0.50)">EXT</text>
```

iii tag vocabulary:

| Tag | Meaning |
|---|---|
| `FOCAL` | The diagram's focal worker |
| `WKR` | Generic iii worker |
| `EDGE` | iii REST / HTTP surface |
| `EXT` | External caller (browser, agent, third party) |
| `KV` | KV state scope |
| `STR` | Stream module |
| `Q` | Queue topic |
| `PUB` | PubSub topic |
| `CRON` | Cron job |
| `EVT` | Event source |
| `SEC` | Security boundary |

Pick from this list. Don't invent new ones.

## Ghost numeral on focal nodes

The focal worker carries a large faint numeral inside its box (right-aligned, vertically centered) — `01`, `02`, …  It's the diagram counter, the eye-catch, and the reason the focal box looks heavier than the others without being visually loud.

```svg
<text x="980" y="616" font-family="Inter Tight, sans-serif"
      font-size="120" font-weight="700" fill="rgba(217,118,58,0.10)"
      text-anchor="end" letter-spacing="-4">01</text>
```

Render BEFORE the focal box's filled rectangle so the box paints over it. Only the ghosted edge shows through. One numeral per focal. Skip on non-focal boxes.

## Arrow rules (zero overlaps)

The single most common failure mode: arrow labels overlapping target boxes. Five rules, in order, prevent it.

1. **Draw arrows BEFORE boxes.** SVG paints in document order. Arrows drawn after will sit on top of the boxes they're supposed to connect.
2. **Terminate the line 4px before the target box edge.** `x2 = box.x - 4`. The arrowhead sits in the gap; it never overlaps the box stroke.
3. **Mask every arrow label with an opaque cream rect.** Drawn AFTER the line, BEFORE the text.
   ```svg
   <line x1="..." y1="..." x2="..." y2="..." stroke="..." marker-end="url(#arrow)"/>
   <rect x="MID-28" y="MID_Y-10" width="56" height="20" rx="3" fill="#f2ede1"/>
   <text x="MID" y="MID_Y+4" font-family="JetBrains Mono, monospace"
         font-size="10" font-weight="600" letter-spacing="1.4" text-anchor="middle">HTTPS</text>
   ```
4. **Arrow label vocabulary: ≤8 chars, all-caps, mono.** `HTTPS`, `INVOKE`, `READ`, `WRITE`, `ACQUIRE`, `CREATE`, `CHECK`, `PUBLISH`, `TRIGGER`. Long labels (`trigger(security::check_capability)`) belong in the caption, not on the arrow.
5. **Color codes the arrow:**
   - **Ink** (`--ink`) — default, internal trigger, generic.
   - **Link blue** (`--link`) — HTTP / external request crossing a network boundary.
   - **Ember** (`--accent`) — the iii primary flow, only on the one path the diagram is about.
   - **Dashed** — async, opt-in, conditional. Combine with any color.

## Z-order

```
1. canvas / paper rect
2. background pattern (optional dots — usually skip)
3. ghost numerals on focal nodes
4. all arrows
5. all node boxes (paper-mask + styled rect + type tag + name + sublabel)
6. arrow label masks + arrow label text
7. legend strip + footer
```

## 4px grid (non-negotiable)

Every coordinate, font size, width, height, gap divisible by 4. Stroke widths and opacity are exempt.

| Category | Allowed |
|---|---|
| Font sizes | 8, 9, 10, 11, 12, 14, 16, 18, 20, 22, 24, 32, 40, 56, 64, 120 |
| Node width | 200, 240, 280, 320 |
| Node height | 120, 160, 200 |
| Gap between nodes | 120, 160, 200, 240 |
| Padding inside boxes | 8, 12, 16 |
| Border radius | 2 (tag), 3 (label), 8 (node) |

Quick check: if a coordinate ends in 1, 2, 3, 5, 6, 7, 9 — fix it.

## Complexity budget

| Rule | Limit |
|---|---|
| Total nodes | **9** |
| Focal nodes (ember) | **2** |
| Arrows | 12 |
| Type tags used | 5 |

Past the budget? Split into two diagrams (overview + detail).

## Page layout

ViewBox `1920 × 1080` is the default (16:9 slide-friendly). Use `1920 × 1200` if the legend strip needs more room.

Top to bottom:

1. **Eyebrow** at `(80, 100)` — mono 12px, `letter-spacing: 3.5`, soft, all-caps. `ARCHITECTURE · <PROJECT> · iii`.
2. **Title** at `(80, 180)` — Inter Tight 64px / 500 / `letter-spacing: -1.5`. One sentence, no period.
3. **Subtitle** at `(80, 220)` — mono 14px soft. The mechanism, not marketing. `POST /api/sandboxes · 32 workers · ws://:49134`.
4. **Diagram body** centered around `y = 540`. Left-to-right flow with at most one diagonal fan-out on the right.
5. **Legend hairline** at `y = 900` spanning `x = 80` to `x = viewBox.w - 80`, stroke `--rule` 0.8.
6. **Legend strip** at `y = 932` — `LEGEND` label left, swatches + arrows in a horizontal row.
7. **Colophon** at `y = 1020` — mono 10px, `letter-spacing: 2.4`. `<PROJECT> · iii ARCHITECTURE` left, `iii.dev · iii.dev/docs` right.

## Anti-patterns

These mark a slop diagram. Refuse to ship if you spot any.

| Anti-pattern | Why it fails |
|---|---|
| Ember on every box | Erases the focal signal. One worker max. |
| 12+ nodes in one diagram | Past the budget. Split. |
| Arrow labels on the line, no mask | Bleeds into the line. Always mask. |
| Arrow labels longer than 8 chars | Belongs in the caption. |
| Pill-shaped type tags | Tags are rectangular `rx="2"`. |
| `JetBrains Mono` for node names | Mono is technical. Names are Inter Tight sans. |
| Drop shadows | Borders only. |
| `rounded-2xl` on boxes | Max radius 8px. |
| Legend floating inside the diagram | Always a horizontal bottom strip with hairline separator. |
| Pure `#000` background | iii cream is `#f2ede1`. Dark theme is `#0d0c0a` warm. Never `#000`. |
| Diagonal text | Horizontal only. No `writing-mode`. |
| Worker boxes without type tags | Every node carries a tag. |
| No ghost numeral on focal | Focal node feels like every other node. |

## Pre-output checklist

Before declaring done.

**Type fit:**
- [ ] One focal worker (or two), not five.
- [ ] Total node count ≤ 9.
- [ ] Would a paragraph or table do the same job? If yes, don't ship.

**Remove test:**
- [ ] Any node mergeable with its neighbor?
- [ ] Any arrow whose absence wouldn't change the meaning?
- [ ] Any label restating what color or shape already says?

**Technical:**
- [ ] Arrows drawn before boxes (z-order).
- [ ] Every arrow line stops 4px before the target box.
- [ ] Every arrow label has an opaque cream rect mask BEHIND the text, ON TOP of the line.
- [ ] Every node has a type tag (`EXT`, `EDGE`, `WKR`, `KV`, …).
- [ ] Focal worker carries a ghost numeral.
- [ ] Legend is a horizontal bottom strip below a hairline.
- [ ] Every coord, font size, width, height, gap divisible by 4.
- [ ] No JetBrains Mono on node names.

**Brand:**
- [ ] Canvas is `#f2ede1` (or `#0d0c0a` for dark). Never `#000`.
- [ ] Ember `#d9763a` appears on the focal box, the primary-flow arrow, and the legend swatch — three places max.
- [ ] Footer reads `iii.dev · iii.dev/docs`.

## Patterns

Five canonical patterns ship in `assets/`. Pick the pattern that matches what you're showing; don't hybridize grammars.

| Pattern | File | Use for |
|---|---|---|
| **Architecture** | `architecture-{cream,dark}.svg` | Components + connections · one focal worker · 6 nodes max |
| **Mesh** | `mesh-{cream,dark}.svg` | N narrow workers around a hub · agent spotlit with ember edges |
| **Layer stack** | `layer-stack-{cream,dark}.svg` | Stacked abstractions · iii engine modules · one focal layer |
| **State machine** | `state-machine-{cream,dark}.svg` | States + transitions · arrows masked · one focal state |
| **Add-a-worker** | `add-worker-{cream,dark}.svg` | Editorial · big sans + mono list · introduces the iii thesis |

Every pattern has a cream variant and a dark variant. Single-file SVGs can't theme-cycle; pick the variant that matches the consumer (deck, README, slide, terminal). To ship both, run the same diagram through the cream and dark token sets.

## Theme tokens

Color substitution from cream to dark:

| Cream | Dark |
|---|---|
| `#f2ede1` (paper) | `#0d0c0a` |
| `#0c0b0a` (ink) | `#efe9d8` |
| `rgba(12,11,10,…)` (ink alpha) | `rgba(239,233,216,…)` |
| `#d9763a` (ember) | `#e88a4e` |
| `rgba(217,118,58,…)` (ember alpha) | `rgba(232,138,78,…)` |
| `#2e5aa8` (link blue) | `#7aa9ff` |
| `#ffffff` (worker fill) | `#15140f` |

For canonical iii primitive semantics (`iii.register_function`, `iii.trigger`, worker registration, trigger types), see [iii.dev/docs](https://iii.dev/docs).
