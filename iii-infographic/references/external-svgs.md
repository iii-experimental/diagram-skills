# External SVG sources — brand logos and generic icons

Sometimes the page needs a real product mark (the source host, the CDN, the database, the LLM provider) or a generic UI icon (lock, shield, warning, check). Don't redraw them — fetch them.

## Sources, in priority order

| Source | URL | Use for | Notes |
|---|---|---|---|
| **svgl** | https://svgl.app · API at https://api.svgl.app | Brand and product logos | 600+ marks, JSON catalog, served as plain SVG. Best first-stop. |
| **Simple Icons** | https://simpleicons.org · CDN: `https://cdn.simpleicons.org/<slug>/<hex>` | Brand logos (monochrome) | 3000+ marks. Use `currentColor` slug variant or pin to `--fg` hex. |
| **Lucide** | https://lucide.dev · CDN: `https://unpkg.com/lucide-static@latest/icons/<name>.svg` | Generic UI icons | Open-source, 1500+, stroke-based, monochrome. |
| **Heroicons** | https://heroicons.com | Generic UI icons | Tailwind family, two weights, monochrome. |

## How to fetch

```bash
# svgl: list marks, then fetch
curl -s https://api.svgl.app | jq '.[] | select(.title | test("cloudflare"; "i"))'
curl -s https://svgl.app/library/cloudflare.svg -o cloudflare.svg

# Simple Icons via CDN, color baked in
curl -s 'https://cdn.simpleicons.org/github/0c0b0a' -o github.svg

# Lucide via unpkg
curl -s https://unpkg.com/lucide-static@latest/icons/shield-check.svg -o shield-check.svg
```

For sites that gate downloads behind JS (rare, but svgl renders client-side for some marks), use a headless browser:

```bash
# playwright (Node)
npx playwright-core download <url>

# or via the gstack browse tool / surf-cli if available in your env
```

## Inlining into the page

Inline the SVG directly in the HTML — don't link `<img src>`. Inline lets you theme it via `currentColor` and `var(--fg)`.

```html
<svg class="icon" viewBox="0 0 24 24" width="20" height="20" fill="currentColor">
  <!-- paste the SVG path data here -->
</svg>
```

```css
.icon { color: var(--fg-2); vertical-align: middle; }
.icon.accent { color: var(--accent); }
.icon.signal { color: var(--signal); }
```

## Brand-mark hygiene

- **Don't recolor a brand mark to ember.** A brand's canonical color is the brand's. Use the mark as-shipped. The legend's binary axis sits on iii-owned shapes — boxes, arrows, numbered circles — not on third-party logos.
- **Don't crop or distort.** Use the source SVG's `viewBox` as-is.
- **Don't replace the mark with a likeness.** If the canonical mark isn't available, use a labeled rectangle with the product name in mono. That's better than an off-brand redraw.
- **Attribution.** Simple Icons requires attribution in non-display use; Lucide is ISC; svgl proxies upstream licenses (varies per mark — check). For an internal infographic, attribution in the footer references panel is enough: `marks: svgl.app · simpleicons.org · lucide.dev`.
- **Strip metadata before inlining.** Run the SVG through `svgo --multipass` (or paste through https://jakearchibald.github.io/svgomg/) to remove editor cruft.

## When to draw vs fetch

Draw it yourself with iii grammar:

- iii primitives: workers, functions, triggers, state scopes — these belong in the iii vocabulary (boxes + type tags + ghost numerals), not as external icons.
- Generic shapes: arrows, dividers, swatches, numbered circles.
- Pipeline / topology / state-machine — `iii-architecture-diagram/references/svg-grammar.md` covers it.

Fetch it from a registry:

- A real product or brand the page is referring to.
- Universal UI affordance the reader will recognize instantly (lock, shield, warning triangle, check, lightning bolt, trophy).

If you spend more than a minute hand-drawing a logo, you're in the wrong mode. Fetch it.
