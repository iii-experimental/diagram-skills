# Anti-patterns

Refuse to ship if any of these are on the page.

- **No export button.** A playground without an export is a static page. Refuse.
- **More than one primary export.** Pick one shape: prompt or JSON. Optional second is the other format.
- **A framework.** No React / Vue / Svelte / Alpine / htmx. Vanilla JS only.
- **A bundler step.** The output is a single HTML file the user opens in a browser.
- **Remote scripts.** Only Google Fonts. No CDN libraries, no analytics, no telemetry.
- **Account / login / credential prompts.** The playground is single-session and local.
- **Server calls.** No `fetch`, no `XMLHttpRequest`, no WebSockets. The agent ingests the export.
- **Two patterns mixed on one page.** kanban + tuner is two playgrounds.
- **Color used for visual interest only.** Ember is the export verb. Signal is success. Anything else is noise.
- **Drag-and-drop without a keyboard alternative.** Accessibility failure.
- **Persistence by default.** Ephemeral first. `localStorage` is opt-in.
- **Marketing copy.** "Powerful tuner", "delightful editor". Refuse. State the task in a sentence.
- **Pure `#000`** background labelled iii. The dark canvas is `#0d0c0a` warm black.
- **Italic for emphasis.** Bold or `--accent` carry weight.
- **Em dashes (`—`) or double-hyphens (`--`).** Use commas, colons, semicolons, periods, parentheses.
- **Animations on more than two elements at once.** Subtle motion only.
- **Auto-execute on load** that mutates state without user intent. The page renders, then waits for the user.
