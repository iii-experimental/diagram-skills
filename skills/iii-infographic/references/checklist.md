# Pre-output checklist

Run before declaring the page done.

## Structure

- [ ] One self-contained HTML file. No external assets except Google Fonts.
- [ ] Two themes (cream default, dark) cycle via topnav button and persist.
- [ ] Document header: id strip + title + subtitle + 6-cell metadata + legend.
- [ ] Six to eight numbered sections, eyebrow + page counter on each.
- [ ] §04 core has at least one formula block with cited source.
- [ ] At least one full-width SVG topology and one pipeline diagram.
- [ ] At least one data table grouped with `<tr class="group">` rows.

## Semantics

- [ ] Color semantic stated in the legend and obeyed in every diagram.
- [ ] Ember accent appears 2–4 times total, anchored to the binary axis.
- [ ] Every count, port, default, and weight traces to a source file or boot log line.

## Voice

- [ ] No italic emphasis. No serif. No em dashes. No marketing words.
- [ ] One assertion per section h2; sentence case; ends with a period.
- [ ] Every formula and default cites a source file.

## Footer

- [ ] References panel: canonical files · env flags · runtime counters.
- [ ] Footer reads `iii.dev`. Install snippet uses `https://install.iii.dev/iii/main/install.sh`.

## Brand

- [ ] Cream canvas is `#f2ede1`. Dark canvas is `#0d0c0a`. Never pure `#000`.
- [ ] iii logo mark is monochrome — no colorized squares + bars.

## Accessibility

- [ ] `prefers-reduced-motion` respected: all animations disabled.
- [ ] Color is never the sole information channel.

## Process recap

1. Inventory + binary axis (`inventory.md`).
2. Verification fact-sheet — every claim with `file:line` source.
3. Section list (6–8 numbered).
4. Per section: diagram-only, table-only, or both.
5. Build header, then §01 → §08.
6. Footer references panel.
7. Final pass against this checklist.
