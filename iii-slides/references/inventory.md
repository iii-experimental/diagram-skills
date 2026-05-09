# Inventory — source document to slides

Two passes before writing any HTML. Skipping these is how 30–40% of source material silently disappears from the deck.

## 1. Inventory the source

Read the source document end to end. Enumerate every:

- Section heading.
- Subsection heading.
- Card or callout.
- Table row.
- Decision.
- Specification.
- Collapsible / expandable detail.
- Footnote.

Count them. A plan with 7 sections, 6 decision cards, a 7-row file table, 4 presets, 6 technique guides, and a spec block with 3 sub-specs and 2 collapsibles is **~25 distinct content items**. All 25 need slide real estate.

## 2. Map source to slides

Assign each inventory item to one or more slides. Every item appears somewhere. Rules:

- **6 decisions = 6 slides**, not "the 2 that fit on a split slide".
- **7 table rows = all 7 rows show up** — split across two data slides if it doesn't fit on one.
- **Collapsible details in the source are not optional in the deck.** They become their own slides.
- **Subsections with multiple cards** (e.g., "6 Visual Technique cards") may need 2–3 slides at readable density.
- **Each major section** typically needs a divider slide + 1–3 content slides depending on density.

A 25-item source maps to 18–25 slides, plus title and end slides — around **22–28 total**. Not 10–13.

## 3. Choose layouts

For each planned slide, pick a slide type from `slide-grammar.md`: title / content / diagram / quote / two-column / data.

Vary across the sequence. A content slide after a diagram. A quote between two data slides. Five identical content slides in a row is a deck failure.

## 4. Pick the binary axis

Same axis as `iii-infographic`:

- `--accent` — paid / opt-in / composable / formula variables.
- `--signal` — free / built-in / always-on.

State the binding on the title slide's legend. Every diagram, every accent use, honors it.

## 5. The completeness test

After mapping inventory to slides, scan once more. Is anything unmapped? Would a reader of the source document notice something missing from the deck?

If yes, add slides.

**The reader test:** a reader who has never seen the source document should be able to reconstruct every major point from the slides alone. If they'd miss entire sections, the deck is incomplete.
