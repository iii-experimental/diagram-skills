# Five patterns

Pick exactly one. A playground that mixes patterns is two playgrounds.

| Pattern | Snippet | Use for |
|---|---|---|
| **kanban** | `templates/playground-snippets/kanban.html` | Reorder, triage, or bucket items across columns. Drag-and-drop. Export = ordered list per column. |
| **tuner** | `templates/playground-snippets/tuner.html` | Tune numeric or enum values that drive a live preview. Sliders, number inputs, color pickers. Export = params JSON or CSS values. |
| **form-editor** | `templates/playground-snippets/form-editor.html` | Edit structured config with constraints. Group by section. Show dependencies. Export = diff or full JSON. |
| **split-preview** | `templates/playground-snippets/split-preview.html` | Edit text on the left, live preview on the right. Prompts, templates, copy. Export = final string. |
| **curate** | `templates/playground-snippets/curate.html` | Approve / reject / tag rows in a dataset. Keyboard shortcuts. Export = filtered list with tags. |

## Picking a pattern

- **Things to reorder?** kanban.
- **Numbers to dial in?** tuner.
- **A config object with N keys and constraints?** form-editor.
- **Text edited with live consequence?** split-preview.
- **A flat list to filter?** curate.

If the answer is "all of the above", split into two playgrounds. Better one focused tool than one cluttered tool.

## What every pattern shares

- Topnav with brand + theme cycle.
- Title + one-line summary.
- Sticky export bar with `[copy as prompt]` ember + `[copy as JSON]` neutral + status slot.
- Mono counter showing meaningful state (`N items`, `3 changed`, `12 / 30 approved`).
- Keyboard support where natural — Enter to confirm, Esc to cancel, arrow keys for navigation in lists.
- `prefers-reduced-motion` respected.

## What no pattern does

- Persists to a server.
- Calls a remote API.
- Loads remote JS (other than Google Fonts).
- Asks for the user's account, login, or any credential.
- Has more than one primary export action.
