Use the canonical iii diagram skills from this repo: `iii-architecture-diagram`, `iii-infographic`, `iii-slides`, `iii-playground`.

OpenClaw support is lightweight rules guidance, not a native plugin adapter. Point the agent at the relevant `SKILL.md` and ask it to follow that workflow:

- Architecture diagram: `iii-architecture-diagram/SKILL.md`
- System reference, diff review, plan review, project recap: `iii-infographic/SKILL.md`
- Slide deck: `iii-slides/SKILL.md`
- Throwaway interactive editor (kanban / tuner / form-editor / split-preview / curate): `iii-playground/SKILL.md`

Each skill's `references/*.md` covers tokens, grammar, checklist, and anti-patterns; `templates/` ships copy-paste starter scaffolds.

Generated outputs go next to the source code by default. If OpenClaw doesn't support command templates, read the matching file under `commands/` and execute its instructions manually.

The skills have no runtime dependencies. The architecture skill can optionally render SVG to PNG via `rsvg-convert` or ImageMagick if the environment provides them.
