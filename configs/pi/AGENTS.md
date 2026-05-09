Use the canonical iii diagram skills from this repo: `iii-architecture-diagram`, `iii-infographic`, `iii-slides`, `iii-playground`.

For Pi, prefer `pi install git:github.com/iii-experimental/diagram-skills` once the repo is published, or install a local checkout with `pi install ./diagram-skills`. Each skill is self-contained under its own directory and ships its own `commands/`, `references/`, and `templates/`.

If your Pi version doesn't support multi-skill repos, install one at a time:

```bash
pi install ./iii-architecture-diagram
pi install ./iii-infographic
pi install ./iii-slides
pi install ./iii-playground
```

Activate with `$iii-architecture-diagram`, `$iii-infographic`, `$iii-slides`, or `$iii-playground`, or via slash commands `/iii-diagram`, `/iii-infographic`, `/iii-diff-review`, `/iii-plan-review`, `/iii-project-recap`, `/iii-slides`, `/iii-playground` after restarting Pi.

Generated outputs go next to the source code by default; the skills themselves don't enforce a fixed output directory. Open in a browser when possible.

The skills have no runtime dependencies. The architecture skill optionally renders SVG to PNG via `rsvg-convert` or ImageMagick; the infographic and slides skills only need a browser.
