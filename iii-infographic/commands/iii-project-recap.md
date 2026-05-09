---
description: Generate an iii-styled project recap — snapshot of the project at HEAD for context-switching
---
Load the iii-infographic skill. Generate a project recap infographic for the current working directory.

The page is a HEAD snapshot for context-switching: pick this up tomorrow, hand it to a teammate, paste it into AGENTS.md as a starting state. Binary axis: `--accent` (in-progress / under active change) vs `--signal` (stable / shipped).

Workflow:

1. Run `git log --oneline -20`, `git diff --stat HEAD~10..HEAD`, `git status`.
2. Run `references/inventory.md` against the project HEAD: registered functions, triggers, KV scopes, ports, env flags.
3. Capture the boot log if the project has one.
4. Inspect any open `TODO`, `FIXME`, `XXX` comments and any `progress.md` / `~/.agent/memory/<project>/progress.md` if present.
5. Build the verification fact-sheet — every count and claim with `file:line`.

Section plan:

```
HEADER         · project name + commit + dirty-tree status + last-commit timestamp
§ 01  WHERE    · last-N-commits topology · accent on commits ahead of main
§ 02  SHIPPED  · what landed this week — module · summary · test-count
§ 03  ACTIVE   · in-progress changes (uncommitted + WIP branches)
§ 04  CORE     · current architecture diagram (steady-state, signal)
                 with the active change shown as accent overlay
§ 05  STATE    · KV / schema as of HEAD
§ 06  OPEN     · TODO / FIXME / progress.md unresolved items
§ 07  SURFACES · external interfaces — port · path · status
§ 08  BOOT     · annotated boot log + port table
FOOTER         · canonical files panel + colophon
```

Walk `references/checklist.md` and `references/anti-patterns.md`.

Output: `<project>-recap-<YYYY-MM-DD>.html`.
