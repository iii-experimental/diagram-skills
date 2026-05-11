# External SVG sources — brand logos and generic icons

Architecture diagrams sometimes need a real product mark next to an iii worker (the LLM provider, the source host, the database adapter). Don't redraw them — fetch them.

## Sources, in priority order

| Source | URL | Use for |
|---|---|---|
| **svgl** | https://svgl.app · API at https://api.svgl.app | Brand and product logos |
| **Simple Icons** | https://simpleicons.org · CDN: `https://cdn.simpleicons.org/<slug>/<hex>` | Brand logos (monochrome) |
| **Lucide** | https://lucide.dev · CDN: `https://unpkg.com/lucide-static@latest/icons/<name>.svg` | Generic UI icons |
| **Heroicons** | https://heroicons.com | Generic UI icons |

## How to fetch

```bash
# svgl
curl -s https://api.svgl.app | jq '.[] | select(.title | test("anthropic"; "i"))'
curl -s https://svgl.app/library/anthropic.svg -o anthropic.svg

# Simple Icons (color baked in)
curl -s 'https://cdn.simpleicons.org/github/0c0b0a' -o github.svg

# Lucide
curl -s https://unpkg.com/lucide-static@latest/icons/database.svg -o database.svg
```

For pages that gate downloads behind JS, use a headless browser (playwright, the gstack browse tool, or surf-cli if available).

## Inlining into the diagram

Embed the fetched SVG inside an SVG `<g>` or `<symbol>` block. Use the mark in its canonical color — don't recolor a brand logo to ember.

```svg
<g transform="translate(80, 240) scale(0.6)">
  <!-- paste the fetched <path> elements here, leaving fill colors intact -->
</g>
```

If the mark needs to sit inside an iii node box, position the box around it normally, keep the type tag (`EXT`, `WKR`, etc.) in the corner, and let the brand mark live in the box body. The iii vocabulary (boxes, type tags, ghost numerals, masked arrow labels) carries the diagram; the brand mark is a recognizable label, not a primary semantic.

## Hygiene

- **Don't recolor brand marks to ember.** Ember is the iii primary path. A brand's canonical color belongs to the brand.
- **Don't crop or skew.** Use the source `viewBox` as-is, scale uniformly with `transform="scale(k)"`.
- **Don't replace a missing mark with a likeness.** Fall back to a labeled rectangle with the product name in mono — it's better than an off-brand redraw.
- **Strip metadata.** Run through `svgo --multipass` (CLI) or https://jakearchibald.github.io/svgomg/ (paste).
- **Footer attribution** for marks used: `marks: svgl.app · simpleicons.org · lucide.dev`.

## When to fetch vs draw

Fetch:

- The diagram references a real product or service the iii worker integrates with.
- A universal UI affordance the reader recognizes instantly (lock, shield, warning, check, bolt).

Draw it yourself with iii grammar (`references/svg-grammar.md`):

- iii primitives — workers, functions, triggers, state scopes.
- Generic shapes — arrows, dividers, type tags, ghost numerals, legend swatches.
- Anything that needs the 4px grid + ember-on-focal contract honored exactly.

If you spend more than a minute hand-drawing a logo, fetch it instead.
