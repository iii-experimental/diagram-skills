# Slide grammar — container, types, navigation

The deck is a scroll-snap container. Each slide is exactly one viewport tall. Single-file HTML with inline CSS + JS. No external dependencies except Google Fonts.

## Container

```html
<body>
  <nav class="topnav"> … theme cycle + counter … </nav>
  <div class="deck">
    <section class="slide slide--title">     … </section>
    <section class="slide slide--content">   … </section>
    <section class="slide slide--diagram">   … </section>
    <!-- one <section> per slide -->
  </div>
</body>
```

```css
.deck {
  height: 100dvh;
  overflow-y: auto;
  scroll-snap-type: y mandatory;
  scroll-behavior: smooth;
  -webkit-overflow-scrolling: touch;
}

.slide {
  height: 100dvh;
  scroll-snap-align: start;
  overflow: hidden;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: clamp(40px, 6vh, 80px) clamp(40px, 8vw, 120px);
  isolation: isolate;
}
```

`isolation: isolate` per slide so absolutely-positioned chrome (page numbers, eyebrows) stays inside its own stacking context.

## Slide types

Six. Don't invent more.

| Type | Use for |
|---|---|
| `slide--title` | Deck cover. One display-size title + one mono subtitle + the legend. |
| `slide--content` | A single assertion + supporting bullets or a short paragraph. The default. |
| `slide--diagram` | A single inline SVG occupying most of the viewport. One eyebrow + one caption max. |
| `slide--quote` | A single short pull quote in display-size sans, mono attribution beneath. Use sparingly. |
| `slide--two-column` | Side-by-side comparison. Title on top. Two columns share the legend's binary axis. |
| `slide--data` | One data table or one formula block, full-width, with eyebrow and a one-line caption. |

Vary across the sequence: a content slide after a diagram, a quote between two data slides. Five identical content slides in a row is a deck failure.

## Navigation chrome

One topnav at `position: sticky; top: 0`:

- Brand: `iii · <project>` left.
- Slide counter: `03 / 18` mono right.
- Theme cycle button: cycles cream ↔ dark, persists via `localStorage`.

Counter updates on `IntersectionObserver` against the `.slide` elements.

No keyboard handlers other than the browser's native scroll. No auto-advance. No fade transitions on more than two elements at once.

## Typography rules

- Display type uses `text-wrap: balance` so titles don't break awkwardly.
- One assertion per slide. The h2 is a sentence; ends with a period.
- No italic emphasis. Bold or `--accent` carry weight.
- Mono is for technical content (function names, ports, formulas, signatures, code).

## Reduced motion

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation: none !important; transition: none !important; }
  .deck { scroll-behavior: auto; }
}
```

Always include this. The deck must work for users who can't see motion.

## Density rules

- Container: `width: min(1320px, 94vw)` for content blocks inside a slide.
- Padding inside a slide: `clamp(40px, 6vh, 80px) clamp(40px, 8vw, 120px)`.
- Vertical rhythm inside a slide: 24px gap between sibling blocks. Never 64px.
- Tables and formulas inside data slides use the same component shapes as `iii-infographic`.

## File output

One self-contained `<project>-deck.html`. CSS + JS inline. Fonts via Google Fonts. Open in any browser to verify scroll-snap on Safari and Chrome.
