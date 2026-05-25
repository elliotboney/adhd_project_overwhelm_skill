# overwhelmed

A Claude Code skill for when a project turns into a hairball and you can't see which strand to grab.

I built this because "where do I even start" is where my projects go to die. You say *"I'm lost in this project"* and it does two things: draws the whole thing as a **mermaid map**, then hands you **one** concrete next action. That's it. The map lives in a per-project `PROJECT_MAP.md`, so you can park ideas without losing them and pick up a later session without re-explaining anything.

Built around three facts about an ADHD brain: working memory is small, starting is the hardest step, and buried wins don't register. Self-contained — no other skills required.

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

## Inspiration

These shaped the design. Each solves a different slice of the problem — worth a look if `overwhelmed` isn't your slice:

- [JackReis/neurodivergent-visual-org](https://github.com/JackReis/neurodivergent-visual-org) — mermaid diagrams with cognitive caps; the complaint→diagram mapping and node limits here come from it.
- [Leonw98/adhd-claude-skill](https://github.com/Leonw98/adhd-claude-skill) — outcome-locked focus sessions and smart-routed parking lot.
- [dsx0511/adhd-copilot](https://github.com/dsx0511/adhd-copilot) — "thread checkpoint" for runaway research threads + an adaptive per-user profile.
- [ravila4/claude-adhd-skills](https://github.com/ravila4/claude-adhd-skills) — time-aware hooks, nudges, and Obsidian-backed journaling.
- [ryantreb/workflow_skills](https://github.com/ryantreb/workflow_skills) — an exec-assistant briefing: one "start here" action, focus capped at 3.
- [nextor2k/hyperfocus](https://github.com/nextor2k/hyperfocus) — output formatting modes and a re-inject-every-turn hook.
- [jdpolasky/ai-chief-of-staff](https://github.com/jdpolasky/ai-chief-of-staff) — a `/start`↔`/wrap` loop over a persistent markdown vault.

## More ADHD + AI resources

Didn't inform this skill, but worth your time if you're wiring up an AI workflow around an ADHD brain:

- [XargsUK/awesome-adhd](https://github.com/XargsUK/awesome-adhd) — big curated list of ADHD apps, tools, and books. Start here to mine more.
- [dicktracey909/awesome-adhd-tools](https://github.com/dicktracey909/awesome-adhd-tools) — tighter list of tools built *for* ADHD brains, not adapted from neurotypical ones.
- [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) — a Claude Code skill that keeps Claude from burying the answer; output-shaping companion to this one.
- [SebastianElvis/octopus](https://github.com/SebastianElvis/octopus) — a Claude Code frontend "for ADHD developers" that runs parallel sessions on a dispatch board.
- [Illyism/sidejot](https://github.com/Illyism/sidejot) — low-friction capture plus a Pomodoro assistant in one.

Non-GitHub: [Goblin Tools](https://goblin.tools) breaks any task into micro-steps — the same "one next action" idea as a web app.

## License

MIT — see [LICENSE](LICENSE).
