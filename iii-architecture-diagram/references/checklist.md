# Pre-output checklist

Run before declaring the diagram done. Every box must be checked.

## Type fit

- [ ] One focal worker (or two), not five.
- [ ] Total node count ≤ 9.
- [ ] Would a paragraph or table do the same job? If yes, don't ship.

## Remove test

- [ ] Any node mergeable with its neighbor?
- [ ] Any arrow whose absence wouldn't change the meaning?
- [ ] Any label restating what color or shape already says?

## Technical

- [ ] Arrows drawn before boxes (z-order).
- [ ] Every arrow line stops 4px before the target box.
- [ ] Every arrow label has an opaque cream rect mask BEHIND the text, ON TOP of the line.
- [ ] Every node has a type tag (`EXT`, `EDGE`, `WKR`, `KV`, …).
- [ ] Focal worker carries a ghost numeral.
- [ ] Legend is a horizontal bottom strip below a hairline.
- [ ] Every coord, font size, width, height, gap divisible by 4.
- [ ] No JetBrains Mono on node names.

## Brand

- [ ] Canvas is `#f2ede1` (or `#0d0c0a` for dark). Never `#000`.
- [ ] Ember `#d9763a` appears on the focal box, the primary-flow arrow, and the legend swatch — three places max.
- [ ] Footer reads `iii.dev · iii.dev/docs`.

## Render to PNG

```bash
rsvg-convert -w 3840 -o <project>-architecture.png <project>-architecture.svg
# or via ImageMagick:
magick -density 200 <project>-architecture.svg <project>-architecture.png
```

`-w 3840` produces a crisp 2x raster of a `1920` viewBox. For 4k decks, `-w 4800`.
