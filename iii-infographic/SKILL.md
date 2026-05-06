---
name: iii-infographic
description: Generate a single-page, dense, engineering-poster site for an iii-based project. Reads like a printed system reference, not a marketing page. Six to eight numbered sections, real numbers from the code, cream-paper canvas (or warm dark) with ember-orange + signal-green carrying a binary semantic. Use when the user wants a reference asset (printable, citable) for an iii deployment, a worker, or any technical project sitting on the iii substrate (iii.dev).
license: Apache-2.0
metadata:
  version: "2.0"
  author: iii (https://iii.dev)
  brand: iii
---

# iii Infographic Skill

Generates a single-page, dense, engineering-poster site for an iii-based project. The output is one self-contained `index.html` (CSS and JS inline). The visual vocabulary is opinionated and consistent across iii projects so the same reader can scan two pages and immediately know where to look.

## When to use

- The project sits on iii primitives (workers, functions, triggers, state) and is worth mapping section by section.
- The audience is engineers, platform teams, or AI-evaluating reviewers, not buyers.
- The page should be a reference asset (printable, pinnable, citable), not a funnel.
- The codebase has real numbers worth showing: counts, ports, defaults, formulas, function signatures.

## When NOT to use

- The page is a marketing campaign. Use the iii website's brand register instead.
- The deliverable is one diagram. Use `iii-architecture-diagram` instead.
- The system is small enough to explain in a paragraph; an infographic is overkill.

## Setup

Two passes before any design.

### 1. Inventory the project

Skim, in order:

- `README.md`, `AGENTS.md`, top-level architecture docs.
- The entrypoint (`src/index.ts`, `main.rs`, `app/main.py`) and read the boot/init log lines verbatim. **Numbers in the page must match the boot log.**
- The state/schema module.
- The retrieval / processing core, if there is one.
- The function registry and trigger registry (look for `iii.registerFunction`, `iii.registerTrigger`, `RegisterFunction::new_async`).

Capture, on a scratchpad:

- All registered functions with their signatures.
- All registered triggers (HTTP / queue / cron / event) with their parameters.
- All persistence scopes / KV keys / streams with their shape.
- All external surfaces with port numbers and exact counts.
- All env flags that change behavior.
- Any formula, threshold, weight that's hard-coded.

**Never invent metrics.** If a number isn't in the code or a doc, it doesn't go on the page.

### 2. Identify the binary axis

The page uses ONE accent (ember-orange) and ONE signal (green). Pick a binary axis the project actually has, and bind:

- **`--accent` (ember-orange)** — composable / opt-in / requires a worker / paid path.
- **`--signal` (green)** — built-in / always-on / default / free path.

| Project type | Axis (signal vs accent) |
|---|---|
| iii memory / agent tooling | free path vs paid path (synthetic vs LLM/embedding) |
| iii API worker | sync vs async · function vs queue trigger |
| iii build / CI worker | local vs remote · cached vs fresh |
| iii database / state worker | committed vs in-flight · durable vs ephemeral |
| iii distributed system | leader vs follower · primary vs replica |

State the binding in the legend. **Color without semantic is a fail.**

## Visual system

### Tokens (must match)

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

### Background

A 24px × 24px paper grid drawn with two `linear-gradient` calls at ~4.5% opacity. Same opacity in both themes, just inverted color. **No other decorative texture is allowed.**

### Typography

Two families. No serif. No italic for emphasis.

```html
<link href="https://fonts.googleapis.com/css2?family=Inter+Tight:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
```

- **Inter Tight** (sans, 400/500/600/700) — headings, document title, table cell text.
- **JetBrains Mono** (400/500/700) — eyebrows, page counters, labels, code, formulas, all numeric data.

Hierarchy:

- Document title: Inter Tight 600, `clamp(36px, 5vw, 64px)`, `letter-spacing: -0.025em`, line-height 1.0.
- Section h2: Inter Tight 600, `clamp(22px, 2.4vw, 30px)`, `letter-spacing: -0.018em`.
- Section sub (one paragraph max): JetBrains Mono 11.5px, color `--fg-2`, line-height 1.55, max 90ch.
- Eyebrow: JetBrains Mono 10.5px, `letter-spacing: 0.18em`, uppercase, color `--fg-3`.
- Table headers: JetBrains Mono 10px, `letter-spacing: 0.18em`, uppercase, color `--fg-3`.
- Table cells: JetBrains Mono 12px, `font-variant-numeric: tabular-nums`.

### Density

- `width: min(1320px, 94vw)` for every container.
- Section vertical padding: 52–64px. Never 120px.
- Table row padding: 9px 14px.
- Use `border` for separation, not `gap`. Adjacent cells share a 1px line.
- Section dividers: a single 1px `--line-strong` border at `section { border-top }`.

### Color semantics (critical)

Every use of color must map to the binary axis chosen during setup.

- **`--accent` (ember-orange)**: primary path, paid / opt-in / composable, formula variables, the iii brand element on this page. Also the page's primary surface marker.
- **`--signal` (green)**: free path, always-on, default, succeeded, durable.
- **`--fg-3` (mid neutral)**: optional, dashed, conditional.

A diagram that uses ember for "the title color" and green for "another title color" has failed. The legend at the top of the page is the contract; every section honors it.

Ember is the iii anchor on this page. Use it sparingly — the legend swatch, §04 formula variables, §07 primary surface card, §03 paid-path branch. Two to four occurrences across the page total.

## Information architecture

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

For canonical iii primitive semantics, link to `iii.dev/docs`.

## Copy rules

- **One assertion per section.** The h2 is a sentence; it ends with a period.
- **One sub-paragraph per section.** Mono, two lines max.
- **Cite source files in the body.** Every formula, every default, every count gets a `<code>path/to/file.ts</code>` reference inline.
- **Never use italic for emphasis.**
- **Sentence case throughout**, except for mono labels (uppercase via letter-spacing + transform) and three-letter abbreviations (REST, MCP, KV, BM25, RRF).
- **No em dashes.** Use commas, colons, semicolons, periods, parentheses. Also not `--`.
- **No marketing words.** No "blazing", "revolutionary", "powerful", "easy", "seamless".
- **Numbers carry the prose.**

## Anti-patterns (must refuse)

- Big italic h1 with `<em>` emphasis.
- Pull-quote floating above a section.
- "is not / is" duality block.
- Manifesto in serif italic.
- Three-tile CTA grid in the footer (use the references panel).
- The hero-metric template (big number, small label, supporting stats).
- Identical card grids with icon + heading + paragraph (use a data table).
- Color used for visual interest only.
- Ember on every box or every section title.
- Animations on more than two elements.
- Lede paragraphs longer than two mono lines.
- Skipped section numbering or non-sequential numbers.
- Invented metrics.
- Logo with colorized squares + bars (the iii mark is monochrome).
- Pure `#000` background labelled as iii — the dark canvas here is `#0d0c0a` warm black.

## Process

1. Run **Setup** (inventory + binary axis).
2. Draft the section list (6–8 numbered sections).
3. For each section, decide diagram-only, table-only, or diagram + table.
4. Write the document header.
5. Build §01 topology SVG.
6. Build §02 primitives table.
7. Build §03 ingest pipeline SVG.
8. Build §04 core (project-specific).
9. Build §05 state reference table.
10. Build §06 tiers/cascade if applicable.
11. Build §07 surfaces 4-up grid.
12. Build §08 boot log + port table.
13. Build the footer references panel.
14. Final pass: theme cycle works, every number traces to source, legend semantics honored.

Ship as a single self-contained `index.html` with inline CSS and JS. Only external dependency is Google Fonts.

## Output checklist

- [ ] One self-contained HTML file. No external assets except Google Fonts.
- [ ] Two themes (cream default, dark) cycle via topnav button and persist.
- [ ] Document header: id strip + title + subtitle + 6-cell metadata + legend.
- [ ] Six to eight numbered sections, eyebrow + page counter on each.
- [ ] §04 core has at least one formula block with cited source.
- [ ] At least one full-width SVG topology and one pipeline diagram.
- [ ] At least one data table grouped with `<tr class="group">` rows.
- [ ] Color semantic stated in the legend and obeyed in every diagram.
- [ ] Ember accent appears 2–4 times total, anchored to the binary axis.
- [ ] Every count, port, default, and weight traces to a source file or boot log line.
- [ ] No italic emphasis. No serif. No em dashes. No marketing words.
- [ ] Footer references panel: canonical files · env flags · runtime counters.
- [ ] Footer reads `iii.dev`. Install snippet uses `https://install.iii.dev/iii/main/install.sh`.
- [ ] Cream canvas is `#f2ede1`. Dark canvas is `#0d0c0a`. Never pure `#000`.
- [ ] `prefers-reduced-motion` respected: all animations disabled.

## Reference implementation

`assets/template.html` ships with header + four sections (§01 topology, §02 primitives, §04 core+formula, §08 boot) wired up. Open it next to this skill when generating a new infographic and extend in place.

For canonical iii primitive semantics (`iii.registerFunction`, `iii.registerTrigger`, worker registration, trigger types), see [iii.dev/docs](https://iii.dev/docs).
