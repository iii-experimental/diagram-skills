# Information architecture — §01 through §08

Six to eight numbered sections, in this order. Skip any that don't apply, but never reorder.

```
HEADER          · doc title block + metadata strip + legend
§ 01  SYSTEM    · topology: callers → triggers → functions → state
§ 02  PRIMITIVES· function signatures table (TS-flavored or Rust-flavored)
§ 03  INGEST    · pipeline diagram with branching paths
§ 04  CORE      · the thing that makes this project distinctive
                  (retrieval, scheduling, planning, codegen, etc.)
                  one big diagram + formula(s) + weight matrix
§ 05  STATE     · KV / table / scope reference, grouped by category
§ 06  TIERS     · derivation cascade if the system has one
§ 07  SURFACES  · external interfaces card grid (4-up) with exact counts
§ 08  BOOT      · annotated boot log + port table
FOOTER          · references panel + colophon
```

`§ 04` is project-specific. Spend the most attention there. Everything else is scaffolding.

The `§` numbering and right-aligned page counter (`04 / 08`) is non-negotiable.

## Component library

### Document header

Five elements, in order:

1. `.doc-id` — id strip (`SYSTEM REFERENCE · SINGLE-PAGE` left, `REV YYYY.MM · III.DEV` right), all mono, `letter-spacing: 0.18em`.
2. `.doc-title` — `<projectname> <span class="ghost">/ system reference</span>`. Inter Tight 600, tight tracking.
3. `.doc-subtitle` — one sentence, mono uppercase, color `--fg-2`.
4. `.doc-meta` — 6-cell border-divided grid: Version · Runtime · Workers · Functions · Triggers · Tests. Each cell mono, label `--fg-3`, value `--fg`, with one or two ember numerics.
5. `.legend` — the color/symbol contract, immediately under the meta grid.

### Section pattern

Every section opens with the same three rows:

1. **Eyebrow row**: `<b>§ 0N · NAME</b> · QUALIFIER` left, `0N / 0M` right.
2. **h2**: one assertion, sentence case, no italic, ends with a period.
3. **`.sub`**: one mono paragraph, two lines max, max 90ch.

Then exactly one of: a full-width diagram, a data table, or a diagram + table pair. Nothing else.

### Data tables

- Outer: `border: 1px solid var(--line-strong)`.
- Header: mono 10px, uppercase, `letter-spacing: 0.18em`, color `--fg-3`, background `--bg-2`.
- Body cells: mono 12px, padding 9px 14px, bottom border `--line`.
- Hover row: background `--bg-2`.
- Group header: `<tr class="group">` with mono 10px uppercase, background `--bg-2`, top + bottom borders `--line-strong`.
- Numeric column: `font-variant-numeric: tabular-nums`, right-aligned.

Always wrap in `.scroll-x` so narrow viewports get a scrollbar.

### Diagrams

All inline SVG, manually authored. No D3, no chart libraries.

Conventions:

- **Markers** for arrowheads. Define `<marker id="arr">` once, plus `arr-a` (accent) and `arr-s` (signal).
- **Boxes**: `fill="var(--bg-2)"`, stroke `var(--fg)` for primary nodes, `var(--fg-2)` for secondary, stroke-width 1 or 1.4.
- **Lines**: solid for required, `stroke-dasharray="3 4"` for optional/async.
- **Labels**: JetBrains Mono via `font-family="JetBrains Mono, monospace"`, sizes 10–11.
- **Color**: only via the legend semantic.
- **Animation**: at most one `<animateMotion>` per stream. `prefers-reduced-motion` disables.

Three diagram archetypes that recur:

1. **Topology grid** (§01): four columns (callers · triggers · functions · state), three column dividers, boxes per column.
2. **Pipeline with branches** (§03): horizontal main line, fork node, two branches (signal-green + accent-ember), merge node.
3. **Worker boundary** (when the §04 core happens to be a single worker): see `iii-architecture-diagram` for the canonical pattern.

### Formula blocks

When the system has a real formula, render it. No MathJax dependency.

```html
<div class="formula">
  <div class="name">FORMULA NAME · QUALIFIER</div>
  <div class="expr">
    score<span class="op">(</span>D,t<span class="op">) =</span>
    IDF<span class="op">(</span>t<span class="op">) ·</span>
    tf<span class="op">(</span>t,D<span class="op">) · (</span><span class="v">k₁</span><span class="op">+</span>1<span class="op">)</span>
    …
  </div>
  <div class="where">
    <code>k₁ = 1.2</code>, <code>b = 0.75</code>. Source: <code>path/to/file.ts</code>.
  </div>
</div>
```

`.op` is `--fg-2`, `.v` is ember (formula variables), defaults are listed in a mono `where` line that cites the source file.

### Code blocks

Boot logs and install snippets only. Four manual classes:

- `.c` — comments, color `--fg-3`
- `.d` — prompts, prefixes, brackets, color `--fg-2`
- `.a` — accent ember (the verb that matters: `iii worker register`, `RegisterFunction`, `http://localhost:49134`)
- `.s` — signal green (success states, JSON success bodies)
- `.t` — full-foreground bold (numbers in the boot log)

Install snippets always show the canonical iii URL:

```bash
curl -fsSL https://install.iii.dev/iii/main/install.sh | sh
```

### Footer references panel

Three columns:

1. **Canonical files** — 8 to 12 source paths to open next, mono 11px with a `→` arrow.
2. **Env flags** — every behavior toggle the page mentioned, mono with a `·` bullet.
3. **Runtime counters** — the same counts from the metadata strip, expanded.

Below the panel, a single colophon row: `<project> · v<version> · iii system reference` left, `↑ top · iii.dev →` right. Both mono uppercase, letter-spacing 0.18em.

## Snippet templates

`templates/section-snippets/*.html` ships one starter HTML fragment per section. Copy the relevant snippet, replace the placeholders with values from your fact-sheet, and paste into the scaffold from `templates/index.html`.

| Snippet | For section |
|---|---|
| `header.html` | Document header (id strip + title + meta + legend) |
| `topology.html` | §01 SYSTEM |
| `primitives-table.html` | §02 PRIMITIVES |
| `pipeline.html` | §03 INGEST |
| `core-formula.html` | §04 CORE |
| `state-table.html` | §05 STATE |
| `tier-cascade.html` | §06 TIERS |
| `surfaces-grid.html` | §07 SURFACES |
| `boot-log.html` | §08 BOOT |
