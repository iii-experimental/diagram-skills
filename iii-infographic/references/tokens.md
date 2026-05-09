# Brand tokens — colors + typography

The iii editorial register. Identical across every iii-* skill. The CSS values match `templates/index.html` exactly — keep them in sync if you bump either.

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
  --accent:    oklch(0.62 0.16 45);   /* ember · primary axis */
  --signal:    oklch(0.55 0.13 155);  /* secondary axis */
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

Two themes. Cream (default, canonical). Dark (terminal / conference / night). The button in the topnav cycles them and persists via `localStorage`. Skip a third theme — two is enough.

The dark canvas is `#0d0c0a` (warm black). Not pure `#000`.

## Background

A 24px × 24px paper grid drawn with two `linear-gradient` calls at ~4.5% opacity. Same opacity in both themes, just inverted color. **No other decorative texture is allowed.**

## Typography

```html
<link href="https://fonts.googleapis.com/css2?family=Inter+Tight:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
```

- **Inter Tight** (sans, 400/500/600/700) — headings, document title, table cell text.
- **JetBrains Mono** (400/500/700) — eyebrows, page counters, labels, code, formulas, all numeric data.

No serif. No italic for emphasis.

| Element | Family / size / weight |
|---|---|
| Document title | Inter Tight 600, `clamp(36px, 5vw, 64px)`, `letter-spacing: -0.025em`, line-height 1.0 |
| Section h2 | Inter Tight 600, `clamp(22px, 2.4vw, 30px)`, `letter-spacing: -0.018em` |
| Section sub | JetBrains Mono 11.5px, color `--fg-2`, line-height 1.55, max 90ch |
| Eyebrow | JetBrains Mono 10.5px, `letter-spacing: 0.18em`, uppercase, color `--fg-3` |
| Table headers | JetBrains Mono 10px, `letter-spacing: 0.18em`, uppercase, color `--fg-3` |
| Table cells | JetBrains Mono 12px, `font-variant-numeric: tabular-nums` |

## Density

- `width: min(1320px, 94vw)` for every container.
- Section vertical padding: 52–64px. Never 120px.
- Table row padding: 9px 14px.
- Use `border` for separation, not `gap`. Adjacent cells share a 1px line.
- Section dividers: a single 1px `--line-strong` border at `section { border-top }`.

## Color semantics (critical)

Every use of color must map to the binary axis chosen during inventory (see `inventory.md`).

- **`--accent` (ember-orange)**: primary path, paid / opt-in / composable, formula variables, the iii brand element on this page. Also the page's primary surface marker.
- **`--signal` (green)**: free path, always-on, default, succeeded, durable.
- **`--fg-3` (mid neutral)**: optional, dashed, conditional.

A diagram that uses ember for "the title color" and green for "another title color" has failed. The legend at the top of the page is the contract; every section honors it.

Ember is the iii anchor on this page. Use it sparingly — the legend swatch, §04 formula variables, §07 primary surface card, §03 paid-path branch. Two to four occurrences across the page total.
