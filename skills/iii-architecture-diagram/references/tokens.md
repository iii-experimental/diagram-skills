# Brand tokens — colors + typography

The iii editorial register. Identical across every iii-* skill.

## Color

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

Dark theme swaps canvas to `#0d0c0a` (warm black, never pure `#000`), ink to `#efe9d8`, accent to `oklch(0.72 0.16 45)`. Same vocabulary either way.

The iii logo mark is monochrome. Never colorize the bars yellow.

## Cream → dark substitution

| Cream | Dark |
|---|---|
| `#f2ede1` (paper) | `#0d0c0a` |
| `#0c0b0a` (ink) | `#efe9d8` |
| `rgba(12,11,10,…)` (ink alpha) | `rgba(239,233,216,…)` |
| `#d9763a` (ember) | `#e88a4e` |
| `rgba(217,118,58,…)` (ember alpha) | `rgba(232,138,78,…)` |
| `#2e5aa8` (link blue) | `#7aa9ff` |
| `#ffffff` (worker fill) | `#15140f` |

Single-file SVGs can't theme-cycle. Pick the variant that matches the consumer (deck, README, slide, terminal). To ship both, run the same diagram through cream + dark token sets.

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

Embed font fallbacks so `rsvg-convert` renders without Google Fonts:

```svg
font-family="JetBrains Mono, Menlo, ui-monospace, monospace"
font-family="Inter Tight, system-ui, sans-serif"
```
