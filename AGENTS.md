# AGENTS.md

Guidance for any AI agent or human working **on** this repo (not using the skill — building it). This is the source of truth; `CLAUDE.md` points here.

## What this repo is

A single Claude Code skill, `overwhelmed`, that turns a tangled project into a visible mermaid map plus one concrete next action, with state persisted per-project in `PROJECT_MAP.md`. Built for ADHD working patterns. It is **self-contained** — it must not depend on any other skill.

## Layout

```
.
├── README.md                 # user-facing: what it is, install, usage
├── AGENTS.md                 # this file — guidance for working on the repo
├── CLAUDE.md                 # stub → points here
├── CONTRIBUTING.md           # how to propose changes
├── LICENSE                   # MIT
└── skills/
    └── overwhelmed/
        ├── SKILL.md          # the skill itself (the deliverable)
        ├── references/
        │   └── mermaid-caps.md   # node caps + complaint→diagram mapping
        └── examples/
            └── PROJECT_MAP.example.md   # canonical state-file format
```

`SKILL.md` is the product. Everything else supports it.

## Design invariants — do not break these

These were deliberate decisions. Changing them is a design change, not a tweak — raise it in an issue first.

1. **Self-contained.** No dependency on `i-have-adhd` or any other skill. The skill owns its own output discipline.
2. **Trigger model:** explicit `/overwhelmed` always works; language auto-detect only ever offers a one-line soft prompt and never takes over until the user says yes.
3. **First move is a map + one action.** Not a wall of text, not a questionnaire. Max 2 clarifying questions before a visible map appears.
4. **Map caps are load-bearing.** 15–20 nodes, 3–5 top-level chunks. A map past these stops being a handle and becomes a second hairball. See `references/mermaid-caps.md`.
5. **State lives in `PROJECT_MAP.md`** at the project root, one per project, human-editable, survives sessions. The skill owns the schema in `examples/PROJECT_MAP.example.md`.
6. **Park, don't lose.** Anything mentioned-but-not-being-done gets routed to the right map area, never dropped.
7. **Every activation ends with exactly one next action** startable in under 5 minutes.

## Where to put what

- **Standing behavior** (applies every time the skill runs) → `SKILL.md`. Keep it lean; it's a recurring token cost once loaded.
- **Detail loaded on demand** (caps, diagram-type tables, long reference) → `references/`. Link to it from `SKILL.md`.
- **Format targets / samples** → `examples/`.

Keep `SKILL.md` under ~150 lines. If it's growing, move detail to `references/`.

## Testing a change

There is no automated harness — this skill is verified by running it. See CONTRIBUTING.md for the full loop. Short version:

1. Copy the skill into your skills dir: `cp -r skills/overwhelmed ~/.claude/skills/`
2. In a deliberately messy project, run `/overwhelmed`, then `park`, `next`, `resume`.
3. Grade against the **Done when** block at the bottom of `SKILL.md` and the invariants above.

## Frontmatter notes

`SKILL.md` uses Claude Code frontmatter (`name`, `description`, `argument-hint`, `allowed-tools`). A VS Code agent linter may flag `allowed-tools` as unsupported — that's a different schema; it is valid for Claude Code and should stay.
