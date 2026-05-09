# Brand tokens — colors + typography

Identical to `iii-infographic/references/tokens.md` and `iii-architecture-diagram/references/tokens.md`. Two themes only — cream (default, canonical) and dark (terminal / conference / night). The dark canvas is `#0d0c0a` (warm black), never pure `#000`.

## CSS variables

```css
:root[data-theme="cream"] {
  --bg:        #f2ede1;
  --bg-2:      #ebe5d4;
  --paper-grid: rgba(12, 11, 10, 0.045);
  --fg:        #0c0b0a;
  --fg-2:      rgba(12, 11, 10, 0.74);
  --fg-3:      rgba(12, 11, 10, 0.5);
  --line:        rgba(12, 11, 10, 0.14);
  --line-strong: rgba(12, 11, 10, 0.26);
  --accent:    oklch(0.62 0.16 45);
  --signal:    oklch(0.55 0.13 155);
}
:root[data-theme="dark"] {
  --bg:        #0d0c0a;
  --bg-2:      #15140f;
  --paper-grid: rgba(232, 226, 211, 0.045);
  --fg:        #efe9d8;
  --fg-2:      rgba(239, 233, 216, 0.78);
  --fg-3:      rgba(239, 233, 216, 0.52);
  --line:        rgba(239, 233, 216, 0.12);
  --line-strong: rgba(239, 233, 216, 0.22);
  --accent:    oklch(0.72 0.16 45);
  --signal:    oklch(0.72 0.13 155);
}
```

## Typography

```html
<link href="https://fonts.googleapis.com/css2?family=Inter+Tight:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
```

- **Inter Tight** — slide displays, slide titles, body text.
- **JetBrains Mono** — eyebrows, slide counters, code, formulas, tabular data.

## Slide-specific scale

Slides are 2–3× larger type than scrollable pages. Page-sized text on a viewport-sized canvas looks like a mistake.

| Element | Size |
|---|---|
| Display (title slide) | `clamp(48px, 10vw, 120px)`, weight 600, `letter-spacing: -2px`, `text-wrap: balance` |
| Slide h2 | `clamp(36px, 6vw, 72px)`, weight 600, `letter-spacing: -1px` |
| Body | `clamp(18px, 1.6vw, 24px)`, weight 400, line-height 1.5 |
| Eyebrow | mono 12px, `letter-spacing: 0.18em`, uppercase |
| Slide counter (topnav) | mono 12px tabular-nums |

No serif. No italic for emphasis. Mono is technical content only.

## Color semantics

Same binary axis as `iii-infographic`:

- `--accent` — paid path / opt-in / composable / formula variables.
- `--signal` — free path / built-in / always-on.
- `--fg-3` — optional / dashed / conditional.

State the binding on the title slide's legend. Every subsequent slide honors it.
