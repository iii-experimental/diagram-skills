# Pre-output checklist

Run before declaring the playground done.

## Pattern fit

- [ ] Exactly one pattern from `patterns.md`. Not a hybrid.
- [ ] The export shape is decided before the HTML is written.
- [ ] The user could finish the task in under five minutes — playgrounds are throwaway.

## Page frame

- [ ] One self-contained HTML file. No external assets except Google Fonts.
- [ ] Two themes (cream default, dark) cycle via topnav button and persist via `localStorage` under `iii-playground-theme`.
- [ ] Topnav: brand left, theme cycle right.
- [ ] Title (Inter Tight h1) + one-line mono summary.
- [ ] Sticky export bar at bottom with `[copy as prompt]` (ember) + optional `[copy as JSON]` (neutral) + mono status slot.

## Export

- [ ] At least one ember `[copy as prompt]` button. Exactly one.
- [ ] `navigator.clipboard.writeText` is used (not `document.execCommand`).
- [ ] After a successful copy, the status slot shows `copied` in `--signal` for ~1.4 seconds.
- [ ] The exported text or JSON matches the shape the agent expects.

## State

- [ ] All state lives in a single `state` object at the top of the script.
- [ ] Every event handler ends with a single `render()` call.
- [ ] Default is ephemeral. `localStorage` persistence is opt-in only and cleared by a button if the user wants to start over.

## Voice

- [ ] No marketing copy. The title states the task in a sentence.
- [ ] No italic emphasis. No serif. No em dashes.
- [ ] Sentence case for headings; mono uppercase for labels and counters.

## Brand

- [ ] Cream canvas is `#f2ede1`. Dark canvas is `#0d0c0a`. Never pure `#000`.
- [ ] Ember appears on the primary export button and the active/focused control. Two places max.
- [ ] iii logo mark stays monochrome.

## Accessibility

- [ ] Every interactive control has a visible focus ring.
- [ ] Keyboard alternative for every drag-and-drop action (e.g. `↑/↓` to move card up/down a column, `←/→` to change column).
- [ ] `prefers-reduced-motion` disables all animations.

## Final pass

- [ ] Open the file. Click the primary export. The clipboard contains the expected shape.
- [ ] Paste the export back into a Claude Code prompt. The agent can act on it without further parsing.
