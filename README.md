# overwhelmed

A Claude Code skill for when a project becomes a hairball and you can't see which strand to grab.

You say *"I'm lost in this project"* — it externalizes the whole thing as a **mermaid map**, then hands you **one concrete next action**. State persists in a per-project `PROJECT_MAP.md`, so you can park ideas without losing them and resume a later session without re-explaining.

Built for ADHD brains: small working memory, starting is the hardest step, buried wins don't register. Self-contained — no dependency on other skills.

## What it does

| Trigger | Result |
|---|---|
| `/overwhelmed` or language like "lost", "too many pieces", "where do I start" | Soft prompt → mermaid map (capped) + one next action |
| `/overwhelmed park <thing>` | Captures the thing, routes it to the right area of the map, returns you to work |
| `/overwhelmed next` | Surfaces the single highest-leverage next step |
| `/overwhelmed resume` | Re-orients from saved state without re-explaining the project |

Auto-detect only ever offers a one-line soft prompt — it never takes over until you say yes.

## Install

Drop the skill into your personal skills folder so it works in every project:

```bash
cp -r skills/overwhelmed ~/.claude/skills/
```

Or per-project only:

```bash
cp -r skills/overwhelmed /path/to/project/.claude/skills/
```

Then in Claude Code, type `/overwhelmed` — or just say you're overwhelmed.

## How it works

- **Map caps** (15–20 nodes, 3–5 chunks) keep the map a *handle*, not a second hairball. See [skills/overwhelmed/references/mermaid-caps.md](skills/overwhelmed/references/mermaid-caps.md).
- **State** lives in `PROJECT_MAP.md` at the project root — human-editable, survives sessions. Sample: [skills/overwhelmed/examples/PROJECT_MAP.example.md](skills/overwhelmed/examples/PROJECT_MAP.example.md).
- **Park, don't lose** — anything you mention but aren't doing now gets routed to the matching map area, never dropped.

## Repo layout

```
.
├── README.md
├── LICENSE
└── skills/
    └── overwhelmed/
        ├── SKILL.md              # the skill
        ├── references/
        │   └── mermaid-caps.md   # node caps + complaint→diagram mapping
        └── examples/
            └── PROJECT_MAP.example.md
```

## License

MIT — see [LICENSE](LICENSE).
