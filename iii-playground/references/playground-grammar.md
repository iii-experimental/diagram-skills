# Playground grammar — frame, export bar, vanilla JS

The page is one self-contained HTML file. No build step. No framework. Vanilla JS, inline. Google Fonts is the only external dependency.

## Page frame

```
┌─────────────────────────────────────────────┐
│  topnav · brand left · theme cycle right    │
├─────────────────────────────────────────────┤
│                                             │
│  task title (Inter Tight, h1)               │
│  one-line task summary (mono, fg-2)         │
│                                             │
│  ┌────── pattern body ──────┐               │
│  │ kanban / tuner / form /  │               │
│  │ split-preview / curate   │               │
│  └──────────────────────────┘               │
│                                             │
├─────────────────────────────────────────────┤
│  sticky export bar                          │
│  [copy as prompt]  [copy as JSON]   N items │
└─────────────────────────────────────────────┘
```

- Topnav: `position: sticky; top: 0`. Brand left, theme cycle right.
- Title block: page-level h1 + one-line summary.
- Pattern body: `width: min(1320px, 94vw)`, centered.
- Sticky export bar: `position: sticky; bottom: 0`, top border `--line-strong`, padded, ember `[copy as prompt]` first, neutral `[copy as JSON]` second, mono counter `N items / N selected / N changed` right.

## Sticky export bar

```css
.export-bar {
  position: sticky; bottom: 0; z-index: 30;
  background: color-mix(in srgb, var(--bg) 92%, transparent);
  backdrop-filter: blur(6px);
  border-top: 1px solid var(--line-strong);
  padding: 16px clamp(20px, 4vw, 48px);
  display: flex; align-items: center; gap: 12px;
}
.export-btn {
  font-family: 'JetBrains Mono', ui-monospace, monospace;
  font-size: 12px;
  letter-spacing: 0.06em;
  background: var(--accent);
  color: var(--bg);
  border: 1px solid var(--accent);
  padding: 10px 18px;
  cursor: pointer;
}
.export-btn--secondary {
  background: transparent;
  color: var(--fg);
  border: 1px solid var(--line-strong);
}
.export-status {
  margin-left: auto;
  font-family: 'JetBrains Mono', ui-monospace, monospace;
  font-size: 12px;
  color: var(--fg-3);
}
.export-status.ok { color: var(--signal); }
```

## Vanilla JS rules

- No React, Vue, Svelte, htmx, Alpine. The skill is for throwaway editors; a framework is overkill.
- No bundler. ES module syntax inline (`<script>` tag, no `type="module"` unless needed for `import`).
- State lives in a single `state` object at the top of the script. Read state on render, write state on event.
- Re-render via a single `render()` function called from every event handler.
- Don't use `eval` or `Function()`. Don't load remote scripts.

## State model

```js
const state = {
  theme: 'cream',
  items: [ /* … */ ],
  selection: new Set(),
  values: { /* sliders, fields */ },
};

function render() {
  // read state, update DOM
}

function exportAsPrompt() {
  return `…natural-language prompt summarizing state…`;
}

function exportAsJson() {
  return JSON.stringify({
    /* the canonical shape the agent expects back */
  }, null, 2);
}
```

The export shape is the playground's contract. The user pastes it back into the agent and the agent processes it. Agree on the shape before writing the page.

## Clipboard pattern

```js
async function copyText(text, statusEl) {
  try {
    await navigator.clipboard.writeText(text);
    statusEl.textContent = 'copied';
    statusEl.classList.add('ok');
    setTimeout(() => {
      statusEl.textContent = '';
      statusEl.classList.remove('ok');
    }, 1400);
  } catch (e) {
    statusEl.textContent = 'copy failed';
  }
}
```

Use `navigator.clipboard.writeText`. Don't use `document.execCommand('copy')` (deprecated). Show a brief `signal`-green confirmation in the export-bar status slot.

## Persistence

Default: ephemeral. State lives in memory only. Refresh wipes it. This matches the throwaway use case.

Opt-in: persist to `localStorage` under a single key `iii-playground:<task-slug>` if the task is long-running and the user is likely to refresh. Always write the export shape to `localStorage`, not raw DOM state — that way the persisted blob is the same as what the export buttons emit.

The theme cycle always persists via `localStorage` under `iii-playground-theme`. That's separate from task state.

## Reduced motion

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation: none !important; transition: none !important; }
}
```

## Output

One self-contained `<task-slug>-playground.html`. Open in a browser. Manipulate. Click `[copy as prompt]`. Paste back into the agent.
