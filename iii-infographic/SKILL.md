---
name: iii-infographic
description: Generate a single-page, dense, engineering-poster site for an iii-based project. Reads like a printed system reference, not a marketing page. Six to eight numbered sections, real numbers from the code, cream-paper canvas (or warm dark) with ember-orange + signal-green carrying a binary semantic. Use when the user wants a reference asset (printable, citable) for an iii deployment, a worker, or any technical project sitting on the iii substrate (iii.dev). Also handles diff reviews, plan reviews, and project recaps in the same visual register.
license: Apache-2.0
metadata:
  version: "2.1"
  author: iii (https://iii.dev)
  brand: iii
---

# iii Infographic Skill

Generates a single-page, dense, engineering-poster site for an iii-based project. The output is one self-contained `index.html` (CSS and JS inline). The visual vocabulary is opinionated and consistent across iii projects so the same reader can scan two pages and immediately know where to look.

## When to use

- The project sits on iii primitives (workers, functions, triggers, state) and is worth mapping section by section.
- The audience is engineers, platform teams, or AI-evaluating reviewers, not buyers.
- The page should be a reference asset (printable, pinnable, citable), not a funnel.
- The codebase has real numbers worth showing: counts, ports, defaults, formulas, function signatures.
- The user wants a diff review, plan review, or project recap rendered in the iii editorial register.

## When NOT to use

- The page is a marketing campaign. Use the iii website's brand register instead.
- The deliverable is one diagram. Use `iii-architecture-diagram` instead.
- The deliverable is a talk deck. Use `iii-slides` instead.
- The system is small enough to explain in a paragraph; an infographic is overkill.

## Workflow

1. **Inventory + binary axis** — `references/inventory.md`. Capture every count, function, port. Pick the binary axis the project actually has.
2. **Verification fact-sheet** — every claim the page will make, cited to `file:line`. The fact-sheet is the source of truth during HTML generation.
3. **Plan sections** — `references/sections.md`. Six to eight numbered sections in canonical order.
4. **Open the scaffold** — `templates/index.html` ships with header + four sections wired up. Extend in place.
5. **Pull snippets** — `templates/section-snippets/*.html` for each remaining section.
6. **Walk the checklist** — `references/checklist.md`. Refuse to ship anything in `references/anti-patterns.md`.

## References

| File | Covers |
|---|---|
| `references/tokens.md` | Color, typography, density, color semantics |
| `references/inventory.md` | Project inventory, binary axis selection, verification fact-sheet |
| `references/sections.md` | §01–§08 information architecture, component library, snippet map |
| `references/checklist.md` | Pre-output gate |
| `references/anti-patterns.md` | Refuse-to-ship list |

Templates in `templates/index.html` + `templates/section-snippets/*.html`.

## Commands

| Command | Source | What it builds |
|---|---|---|
| `/iii-infographic <project-path>` | `commands/iii-infographic.md` | Full §01–§08 system reference page |
| `/iii-diff-review <git-ref>` | `commands/iii-diff-review.md` | Before/after infographic with iii vocabulary (no GitHub red/green) |
| `/iii-plan-review <plan-file>` | `commands/iii-plan-review.md` | Plan-vs-codebase audit, every claim cited |
| `/iii-project-recap` | `commands/iii-project-recap.md` | Snapshot of the project at HEAD for context-switching |

## iii context

For canonical iii primitive semantics (`iii.registerFunction`, `iii.registerTrigger`, worker registration, trigger types), see [iii.dev/docs](https://iii.dev/docs).
