# Anti-patterns

Refuse to ship if the diagram has any of these.

| Anti-pattern | Why it fails |
|---|---|
| Ember on every box | Erases the focal signal. One worker max. |
| 12+ nodes in one diagram | Past the budget. Split. |
| Arrow labels on the line, no mask | Bleeds into the line. Always mask. |
| Arrow labels longer than 8 chars | Belongs in the caption. |
| Pill-shaped type tags | Tags are rectangular `rx="2"`. |
| `JetBrains Mono` for node names | Mono is technical. Names are Inter Tight sans. |
| Drop shadows | Borders only. |
| `rounded-2xl` on boxes | Max radius 8px. |
| Legend floating inside the diagram | Always a horizontal bottom strip with hairline separator. |
| Pure `#000` background | iii cream is `#f2ede1`. Dark theme is `#0d0c0a` warm. Never `#000`. |
| Diagonal text | Horizontal only. No `writing-mode`. |
| Worker boxes without type tags | Every node carries a tag. |
| No ghost numeral on focal | Focal node feels like every other node. |
| Logo with colorized squares + bars | The iii mark is monochrome. |
| Marketing words in title or subtitle | "Powerful", "blazing", "seamless" — refuse. The subtitle is the mechanism. |
| Mixing two pattern grammars | Architecture-with-mesh-edges-on-a-state-machine. Pick one. |
