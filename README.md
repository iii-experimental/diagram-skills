# diagram-skills

Two skills for documenting [iii](https://iii.dev) projects with a consistent visual vocabulary.

| Skill | Output | When to use |
|---|---|---|
| [`iii-architecture-diagram`](./iii-architecture-diagram/) | `.svg` (+ optional `.png`) | Single architecture diagram of an iii deployment |
| [`iii-infographic`](./iii-infographic/) | One self-contained `.html` page | Printable, citable system reference (6–8 numbered sections) |

Both skills share the iii editorial register: cream paper canvas (or warm dark), ember accent reserved for one focal element, Inter Tight + JetBrains Mono. Full brand contract in each skill's `SKILL.md`.

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

Once installed, prompt the agent:

```
Use iii-architecture-diagram to draw the sandbox lifecycle for my iii deployment.
Read the boot log at ~/.agentos/logs/engine.log and pick one focal worker.
```

```
Use iii-infographic to generate a system reference for ~/agentmemory.
Read AGENTS.md and the boot log. Pick the binary axis from the code.
```

The agent emits a single `.svg` (or `.html`) file you can open in any browser, ship in a deck, or paste into a PR.

## Render to PNG

```bash
rsvg-convert -w 3840 -o agentos-architecture.png agentos-architecture.svg
# or:
magick -density 200 agentos-architecture.svg agentos-architecture.png
```

## License

Apache-2.0. Matches the iii-sdk family.

## See also

- [iii.dev](https://iii.dev) — the engine
- [iii.dev/docs](https://iii.dev/docs) — primitive reference (`iii.register_function`, `iii.trigger`)
