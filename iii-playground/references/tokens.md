# Brand tokens — colors + typography

Identical to the rest of the bundle. One addition: ember is the export-action color, signal is the saved/approved state.

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
  --accent:    oklch(0.62 0.16 45);   /* export action · the verb that matters */
  --signal:    oklch(0.55 0.13 155);  /* saved · approved · success */
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

- **Inter Tight** — page title, card titles, body.
- **JetBrains Mono** — labels, value readouts, code, JSON output, all numeric data.

## Color semantics (playground-specific)

- `--accent` ember — the **export button** (the verb the user came here to do) and the active/focused control. Use exactly twice on a page: the primary export button + the focus ring on the control being adjusted.
- `--signal` green — saved / approved / success badge. Toast confirmation after `copy` succeeds.
- `--fg-3` neutral — disabled, placeholder, helper text.
- `--line-strong` border — the sticky export bar's top edge.

A playground that uses ember for "card backgrounds" and green for "another card type" has failed. Color carries a single semantic.
