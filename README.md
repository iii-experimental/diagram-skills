# diagram-skills

Two skills for documenting [iii](https://iii.dev) projects with a consistent visual vocabulary.

| Skill | Output | When to use |
|---|---|---|
| [`iii-architecture-diagram`](./iii-architecture-diagram/) | `.svg` (+ optional `.png`) | Single-page architecture / mesh / state-machine / layer-stack / editorial diagram |
| [`iii-infographic`](./iii-infographic/) | self-contained `.html` | Printable system reference (6–8 numbered sections) |

Both skills share the iii editorial register: cream paper canvas (or warm dark), ember accent reserved for one focal element, Inter Tight + JetBrains Mono. Full brand contract in each skill's `SKILL.md`.

## Patterns

Five diagram patterns ship in `iii-architecture-diagram/assets/`. Every pattern has a cream variant and a dark variant; pick to match the target medium (deck, README, terminal, slide).

<table>
<tr>
<td align="center" width="50%">
  <img src="iii-architecture-diagram/assets/architecture-cream.png" alt="Architecture · cream"/>
  <br/><b>Architecture</b><br/>
  <sub>Components + connections · one focal worker · 6 nodes · ember primary flow</sub>
</td>
<td align="center" width="50%">
  <img src="iii-architecture-diagram/assets/architecture-dark.png" alt="Architecture · dark"/>
  <br/><b>Architecture · dark</b><br/>
  <sub>Same vocabulary · warm <code>#0d0c0a</code> canvas · brighter ember + link</sub>
</td>
</tr>
<tr>
<td align="center">
  <img src="iii-architecture-diagram/assets/mesh-cream.png" alt="Mesh · cream"/>
  <br/><b>Mesh</b><br/>
  <sub>N narrow workers around a hub · agent spotlit with ember edges · subset-mesh edges</sub>
</td>
<td align="center">
  <img src="iii-architecture-diagram/assets/mesh-dark.png" alt="Mesh · dark"/>
  <br/><b>Mesh · dark</b><br/>
  <sub>The iii.dev landing aesthetic · thin strokes on warm dark</sub>
</td>
</tr>
<tr>
<td align="center">
  <img src="iii-architecture-diagram/assets/layer-stack-cream.png" alt="Layer stack · cream"/>
  <br/><b>Layer stack</b><br/>
  <sub>Stacked abstractions · iii engine modules with adapter classes · one focal layer</sub>
</td>
<td align="center">
  <img src="iii-architecture-diagram/assets/layer-stack-dark.png" alt="Layer stack · dark"/>
  <br/><b>Layer stack · dark</b><br/>
  <sub>Same stack · disabled module shown as dashed</sub>
</td>
</tr>
<tr>
<td align="center">
  <img src="iii-architecture-diagram/assets/state-machine-cream.png" alt="State machine · cream"/>
  <br/><b>State machine</b><br/>
  <sub>States + transitions · sandbox lifecycle · one focal state · masked arrow labels</sub>
</td>
<td align="center">
  <img src="iii-architecture-diagram/assets/state-machine-dark.png" alt="State machine · dark"/>
  <br/><b>State machine · dark</b><br/>
  <sub>Optional transitions dashed · primary entry in ember</sub>
</td>
</tr>
<tr>
<td align="center">
  <img src="iii-architecture-diagram/assets/add-worker-cream.png" alt="Add a worker · cream"/>
  <br/><b>Add a worker (editorial)</b><br/>
  <sub>Big sans heading + mono list · introduces the iii narrow-workers thesis</sub>
</td>
<td align="center">
  <img src="iii-architecture-diagram/assets/add-worker-dark.png" alt="Add a worker · dark"/>
  <br/><b>Add a worker · dark</b><br/>
  <sub>Same editorial · ember accent on the verb that matters</sub>
</td>
</tr>
</table>

## Install

### Claude Code CLI

```bash
git clone https://github.com/iii-experimental/diagram-skills ~/diagram-skills

# user-level (available in every project)
ln -s ~/diagram-skills/iii-architecture-diagram ~/.claude/skills/iii-architecture-diagram
ln -s ~/diagram-skills/iii-infographic         ~/.claude/skills/iii-infographic

# or project-level
ln -s ~/diagram-skills/iii-architecture-diagram ./.claude/skills/iii-architecture-diagram
```

### SkillKit (Claude Code, Cursor, Codex, Gemini CLI, OpenCode, 27 more)

```bash
# from a local clone
npx skillkit install iii-architecture-diagram --from ~/diagram-skills/iii-architecture-diagram
npx skillkit install iii-infographic         --from ~/diagram-skills/iii-infographic

# translate to a different agent format
npx skillkit translate iii-architecture-diagram --agent cursor
npx skillkit translate iii-architecture-diagram --agent codex
npx skillkit translate iii-architecture-diagram --agent opencode

# search the SkillKit marketplace once published
npx skillkit search iii-architecture-diagram
```

### Claude.ai (Pro / Max / Team / Enterprise)

```bash
cd ~/diagram-skills
zip -r iii-architecture-diagram.zip iii-architecture-diagram
zip -r iii-infographic.zip         iii-infographic
```

Upload each zip via **Settings → Capabilities → Skills → + Add**.

### Project-local (any repo)

```bash
mkdir -p .claude/skills
git submodule add https://github.com/iii-experimental/diagram-skills .claude/diagram-skills
ln -s ../diagram-skills/iii-architecture-diagram .claude/skills/iii-architecture-diagram
ln -s ../diagram-skills/iii-infographic         .claude/skills/iii-infographic
```

## Usage

```
Use iii-architecture-diagram to draw the sandbox lifecycle for my iii deployment.
Read the boot log at ~/.agentos/logs/engine.log and pick one focal worker.
Use the architecture pattern, dark theme.
```

```
Use iii-architecture-diagram to draw a mesh of my narrow workers.
Spotlight the agent caller. Cream theme.
```

```
Use iii-architecture-diagram to draw the iii engine module stack.
Show every module from config.yaml as a layer with adapter class + port.
Focal = the State module.
```

```
Use iii-infographic to generate a system reference for ~/agentmemory.
Read AGENTS.md and the boot log. Pick the binary axis from the code.
```

The skill emits a single `.svg` (or `.html`) you open in any browser, ship in a deck, or paste into a PR.

## Render to PNG

```bash
rsvg-convert -w 3840 -o agentos-architecture.png agentos-architecture.svg
# or:
magick -density 200 agentos-architecture.svg agentos-architecture.png
```

`-w 3840` produces a crisp 2x raster of a `1920` viewBox. For 4k decks, `-w 4800`.

## License

Apache-2.0. Matches the iii-sdk family.

## See also

- [iii.dev](https://iii.dev) — the engine
- [iii.dev/docs](https://iii.dev/docs) — primitive reference (`iii.register_function`, `iii.trigger`)
