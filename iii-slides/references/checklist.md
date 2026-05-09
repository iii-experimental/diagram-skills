# Pre-output checklist

Run before declaring the deck done.

## Inventory

- [ ] Source-document inventory enumerated every section, card, table row, decision, footnote.
- [ ] Every inventory item maps to ≥1 slide.
- [ ] The reader-without-source test passes: a reader could reconstruct every major point.
- [ ] Total slide count is 18–25 for a typical 25-item source — not 10–13.

## Structure

- [ ] One self-contained HTML file. No external assets except Google Fonts.
- [ ] Two themes (cream default, dark) cycle via topnav button and persist via `localStorage`.
- [ ] Topnav shows `iii · <project>` left, slide counter `0N / 0M` right.
- [ ] Each slide is exactly `100dvh` and uses `scroll-snap-align: start`.
- [ ] Slide counter updates on `IntersectionObserver` as the user scrolls.

## Slide variety

- [ ] No more than two consecutive slides of the same type.
- [ ] At least one diagram slide if the source has any structural diagrams.
- [ ] At least one data slide if the source has any tables.

## Voice

- [ ] One assertion per slide. The h2 is a sentence, ends with a period.
- [ ] No italic emphasis. No serif. No em dashes. No marketing words.
- [ ] Numbers carry the prose. Every count traces to source.

## Brand

- [ ] Cream canvas is `#f2ede1`. Dark canvas is `#0d0c0a`. Never pure `#000`.
- [ ] Ember `--accent` is anchored to the binary axis stated on the title slide.
- [ ] iii logo mark is monochrome. No colorized squares + bars.

## Accessibility

- [ ] `prefers-reduced-motion` disables all animations and `scroll-behavior: smooth`.
- [ ] Color is never the sole information channel.

## Final pass

- [ ] Open in Safari and Chrome. Scroll-snap works on both.
- [ ] Theme cycle persists across reload.
