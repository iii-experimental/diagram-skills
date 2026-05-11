# Anti-patterns

Refuse to ship if any of these are in the deck.

- **Auto-advance.** The deck is scroll-driven. The user controls pace.
- **Transitions on more than two elements at once.** Subtle motion only — `prefers-reduced-motion` disables it.
- **A third theme.** Two is enough.
- **A title slide with marketing copy.** "The future of …", "Re-imagining …", "Powerful, simple, elegant". Refuse.
- **Italic emphasis** for "weight". Use bold or `--accent`.
- **Em dashes (`—`) or double-hyphens (`--`).** Use commas, colons, semicolons, periods, parentheses.
- **Five consecutive content slides.** Vary the layout.
- **A 10-slide deck for a 25-item source.** Inventory failure. See `inventory.md`.
- **Slides shorter than `100dvh`.** Scroll-snap breaks; the deck looks like a long page.
- **Slides taller than `100dvh`.** Content overflow inside a slide is a sign the slide should be two slides.
- **Pull-quotes formatted as marketing testimonials.** A quote slide is one short line + mono attribution. No portrait. No company logo.
- **Color-only legends.** The binary-axis swatch always has a text label.
- **Pure `#000`** background labelled iii. The dark canvas is `#0d0c0a` warm black.
- **Logo with colorized squares + bars.** The iii mark is monochrome.
- **Fonts other than Inter Tight + JetBrains Mono.** No serif. No display fonts.
- **Slide numbering that skips or restarts.** Counter is `0N / 0M`, sequential, sticky.
- **A slide whose only purpose is "thanks" or "questions?".** Either it carries content or it gets removed.
