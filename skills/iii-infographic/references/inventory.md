# Inventory + binary axis + verification

Two passes before you write any HTML. Skipping these is how invented metrics ship.

## 1. Inventory the project

Skim, in order:

- `README.md`, `AGENTS.md`, top-level architecture docs.
- The entrypoint (`src/index.ts`, `main.rs`, `app/main.py`) and read the boot/init log lines verbatim. **Numbers in the page must match the boot log.**
- The state/schema module.
- The retrieval / processing core, if there is one.
- The function registry and trigger registry (look for `iii.registerFunction`, `iii.registerTrigger`, `RegisterFunction::new_async`).

Capture, on a scratchpad:

- All registered functions with their signatures.
- All registered triggers (HTTP / queue / cron / event) with their parameters.
- All persistence scopes / KV keys / streams with their shape.
- All external surfaces with port numbers and exact counts.
- All env flags that change behavior.
- Any formula, threshold, weight that's hard-coded.

**Never invent metrics.** If a number isn't in the code or a doc, it doesn't go on the page.

## 2. Identify the binary axis

The page uses ONE accent (ember-orange) and ONE signal (green). Pick a binary axis the project actually has, and bind:

- **`--accent` (ember-orange)** — composable / opt-in / requires a worker / paid path.
- **`--signal` (green)** — built-in / always-on / default / free path.

| Project type | Axis (signal vs accent) |
|---|---|
| iii memory / agent tooling | free path vs paid path (synthetic vs LLM/embedding) |
| iii API worker | sync vs async · function vs queue trigger |
| iii build / CI worker | local vs remote · cached vs fresh |
| iii database / state worker | committed vs in-flight · durable vs ephemeral |
| iii distributed system | leader vs follower · primary vs replica |

State the binding in the legend. **Color without semantic is a fail.**

## 3. Build a verification fact-sheet

Before generating HTML, produce a structured table of every claim the page will make:

- Every quantitative figure: line counts, file counts, function counts, test counts, port numbers.
- Every function, type, and module name you will reference.
- Every behavior description: what code does, what changed, before vs. after.
- For each, cite the source: the git command output that produced it, or the file:line where you read it.

Verify each claim against the code. If something cannot be verified, mark it as uncertain rather than stating it as fact. **The fact-sheet is the source of truth during HTML generation. Don't deviate from it.**

This step is the difference between a page the maintainer trusts and a page the maintainer rewrites.

## 4. Read the boot log

Every infographic ends with a §08 BOOT section. Capture the boot log verbatim — the project's own startup output is the most authoritative count source available. If a number on the page disagrees with the boot log, the boot log wins.
