# Five patterns

Pick the pattern that matches what you're showing. Don't hybridize grammars.

| Pattern | Template files | Use for |
|---|---|---|
| **Architecture** | `templates/architecture-{cream,dark}.svg` | Components + connections · one focal worker · 6 nodes max · ember primary flow |
| **Mesh** | `templates/mesh-{cream,dark}.svg` | N narrow workers around a hub · agent spotlit with ember edges · subset-mesh edges |
| **Layer stack** | `templates/layer-stack-{cream,dark}.svg` | Stacked abstractions · iii engine modules with adapter classes · one focal layer |
| **State machine** | `templates/state-machine-{cream,dark}.svg` | States + transitions · sandbox lifecycle · one focal state · masked arrow labels |
| **Add-a-worker** (editorial) | `templates/add-worker-{cream,dark}.svg` | Big sans heading + mono list · introduces the iii narrow-workers thesis |

Every pattern has a cream variant and a dark variant. Pick the one matching the consumer (deck, README, slide, terminal). To ship both, run the same diagram through cream + dark token sets.

## How to use a template

1. Copy `templates/<pattern>-cream.svg` (or dark) to your project.
2. Read the file. It's working SVG with placeholder text — the geometry is correct.
3. Edit text only:
   - Title, subtitle, eyebrow.
   - Node names + sublabels.
   - Type tags (pick from the vocabulary in `svg-grammar.md`).
   - Arrow labels (≤8 chars).
   - The ghost numeral on the focal node.
   - Legend swatches.
   - Footer colophon.
4. Don't change geometry unless the node count or layout mandates it. The 4px grid is non-negotiable.
5. Run the checklist (`checklist.md`) before declaring done.

## Pattern selection cheatsheet

- **One focal worker plus 3–5 supporting** → architecture.
- **Hub-and-spoke, fleet of narrow workers** → mesh.
- **Vertical abstraction tower (engine modules, adapter layers)** → layer-stack.
- **Sandbox / job / connection lifecycle** → state-machine.
- **Editorial card introducing the iii thesis (no boxes-and-arrows)** → add-worker.

If two patterns feel close, you probably have two diagrams. Pick the one that answers the loudest question; ship the other later.
