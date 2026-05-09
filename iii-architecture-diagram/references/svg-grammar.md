# SVG grammar — type tags, ghost numerals, masked arrows, layout

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

The focal worker carries a large faint numeral inside its box (right-aligned, vertically centered) — `01`, `02`, … It's the diagram counter, the eye-catch, and the reason the focal box looks heavier than the others without being visually loud.

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

## Complexity budget

| Rule | Limit |
|---|---|
| Total nodes | **9** |
| Focal nodes (ember) | **2** |
| Arrows | 12 |
| Type tags used | 5 |

Past the budget? Split into two diagrams (overview + detail).
