---
description: Generate an iii-styled diff review infographic — before/after architecture comparison with code review
---
Load the iii-infographic skill. Generate a diff review infographic for git ref: $1 (defaults to `main` if no arg).

**Important: render in the iii editorial register, not GitHub red/green.** The binary axis here is `--accent` (changed / new) vs `--signal` (kept / removed cleanly). State this binding in the legend.

Scope detection on `$1`:
- Branch name: working tree vs that branch
- Commit hash: that commit (`git show <hash>`)
- `HEAD`: uncommitted only (`git diff` and `git diff --staged`)
- PR number `#42`: `gh pr diff 42`
- Range `abc..def`: range diff
- No argument: `main`

Data gathering:
- `git diff --stat <ref>` for file-level overview
- `git diff --name-status <ref>` for new/modified/deleted (separate src vs tests)
- Line counts before/after for key files
- New public surface: grep added lines for `export` / `function` / `class` / `interface` / `def` / `func` / `pub` (adapt to language)
- Read every changed file in full
- Check `CHANGELOG.md` and `README.md` for matching updates

Run the **verification fact-sheet** procedure from `references/inventory.md` before generating HTML. Every claim cited.

Section plan (deviate from canonical §01–§08 only as the diff demands):

```
HEADER         · ref summary + line/file totals + housekeeping (changelog/docs badges)
§ 01  SCOPE    · changed files topology (signal = kept, accent = changed)
§ 02  SURFACE  · new public API table — symbol · file · kind · line
§ 03  FLOW     · before/after pipeline diagrams stacked, accent on the changed branch
§ 04  CORE     · the central change: one diagram + the rationale paragraph
§ 05  STATE    · schema/state changes (added/removed columns/keys)
§ 06  REVIEW   · structured Good / Bad / Ugly / Questions cards
§ 07  DECISIONS· decision log: what was decided + why (one card per decision)
§ 08  TESTS    · before/after test counts + coverage delta
FOOTER         · canonical files panel + colophon
```

Read `references/sections.md` for component shapes (cards, formula blocks are not used here, data tables are).

Walk `references/checklist.md` and `references/anti-patterns.md` before declaring done.

Output: `<project>-diff-<ref>.html`.
