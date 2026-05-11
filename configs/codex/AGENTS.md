Use the canonical iii diagram skills from this repo: `iii-architecture-diagram`, `iii-infographic`, `iii-slides`, `iii-playground`.

For Codex CLI, copy the skill directories to `~/.codex/skills/`:

```bash
mkdir -p ~/.codex/skills
cp -r skills/iii-architecture-diagram ~/.codex/skills/
cp -r skills/iii-infographic         ~/.codex/skills/
cp -r skills/iii-slides              ~/.codex/skills/
cp -r skills/iii-playground          ~/.codex/skills/
```

If your Codex build supports prompt templates, copy command files to `~/.codex/prompts/`:

```bash
mkdir -p ~/.codex/prompts
cp skills/iii-architecture-diagram/commands/*.md ~/.codex/prompts/
cp skills/iii-infographic/commands/*.md         ~/.codex/prompts/
cp skills/iii-slides/commands/*.md              ~/.codex/prompts/
cp skills/iii-playground/commands/*.md          ~/.codex/prompts/
```

Activate by asking Codex to use `$iii-architecture-diagram`, `$iii-infographic`, `$iii-slides`, or `$iii-playground` before generating, or invoke the matching slash command (`/iii-diagram`, `/iii-infographic`, `/iii-diff-review`, `/iii-plan-review`, `/iii-project-recap`, `/iii-slides`, `/iii-playground`).

If prompts are unavailable in your Codex version, read the relevant `commands/*.md` file and follow the skill workflow manually. The skill itself (`SKILL.md` plus `references/`) is the source of behavior; commands are convenience entrypoints.

Generated SVG, HTML, and deck files go next to the source code by default. Browser auto-open behavior depends on Codex sandbox permissions.
