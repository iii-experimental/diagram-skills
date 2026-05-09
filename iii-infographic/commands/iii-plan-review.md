---
description: Generate an iii-styled plan review — plan claims vs codebase reality, every claim cited
---
Load the iii-infographic skill. Generate a plan review infographic for plan file: $1.

The page audits a plan (plan.md, design doc, RFC, or any forward-looking document) against the actual codebase. The binary axis is `--accent` (claim verified) vs `--signal` (claim already true / no work needed) with `--fg-3` for unverifiable / blocked claims.

Workflow:

1. Read `$1` end to end.
2. Enumerate every concrete claim — every file path, function name, count, threshold, behavior assertion, and named decision.
3. For each claim, verify against the code: grep the symbol, read the file, run the boot log, confirm the count.
4. Build the **verification fact-sheet** (`references/inventory.md`) with three columns: claim · evidence · status (verified / already-true / unverifiable).
5. Inventory the project as you would for a normal infographic — counts, ports, registries — so the page anchors the plan claims in the system as it exists today.

Section plan:

```
HEADER         · plan title + verification summary (N claims · M verified · K blocked)
§ 01  PLAN     · claim inventory table — claim · evidence · status
§ 02  SURFACE  · new functions/triggers the plan introduces vs ones already present
§ 03  STATE    · KV / schema changes the plan calls for vs current schema
§ 04  CORE     · the central architecture diagram of the plan
                 with current-state shaded and proposed-state in accent
§ 05  RISKS    · cards for unverifiable claims, conflicts with current code, ordering risks
§ 06  ORDER    · proposed sequence of changes (numbered cards or pipeline)
§ 07  TESTS    · what's testable now vs what needs new tests
§ 08  CITATIONS· every claim's source: plan line + code file:line
FOOTER         · canonical files panel + colophon
```

Use `references/sections.md` for component shapes. Walk `references/checklist.md` and `references/anti-patterns.md`.

Output: `<plan-stem>-review.html`.
