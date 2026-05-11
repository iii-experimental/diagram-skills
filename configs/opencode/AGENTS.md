Use the canonical iii diagram skills from this repo: `iii-architecture-diagram`, `iii-infographic`, `iii-slides`, `iii-playground`.

For OpenCode/opencode, the observed native skill path is `~/.config/opencode/skill/`. Copy each skill directory under that path:

```bash
mkdir -p ~/.config/opencode/skill
cp -r skills/iii-architecture-diagram ~/.config/opencode/skill/
cp -r skills/iii-infographic         ~/.config/opencode/skill/
cp -r skills/iii-slides              ~/.config/opencode/skill/
cp -r skills/iii-playground          ~/.config/opencode/skill/
```

Optional command templates may be copied to `~/.config/opencode/command/` if your build supports them:

```bash
mkdir -p ~/.config/opencode/command
cp skills/iii-architecture-diagram/commands/*.md ~/.config/opencode/command/
cp skills/iii-infographic/commands/*.md         ~/.config/opencode/command/
cp skills/iii-slides/commands/*.md              ~/.config/opencode/command/
cp skills/iii-playground/commands/*.md          ~/.config/opencode/command/
```

Activate by asking OpenCode to use the `iii-architecture-diagram`, `iii-infographic`, `iii-slides`, or `iii-playground` skill for diagrams, system references, slide decks, or throwaway interactive editors. Generated outputs go next to the source code by default; browser auto-open depends on the harness.

Command-template behavior is build-dependent. The canonical skill docs (`SKILL.md` + `references/`) are the source of truth.
