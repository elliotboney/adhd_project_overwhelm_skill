# Contributing to `overwhelmed`

Thanks for wanting to improve this. It's a small skill with strong opinions — the goal is to keep it sharp, not to grow it. Read the **Design invariants** in [AGENTS.md](AGENTS.md) before you start; most rejected PRs are ones that quietly break one.

## Ground rules

- **Smaller is better.** This skill helps overwhelmed people. Every line added to `SKILL.md` is context the model carries every turn. If a change makes the skill longer, it needs to earn its place.
- **Don't re-litigate the locked decisions** (trigger model, map-first, per-project state file, self-contained) without opening an issue first. They're in AGENTS.md with rationale.
- **Detail goes in `references/`, not `SKILL.md`.** Keep the main file lean.

## Workflow

1. **Fork** this repo and clone your fork.
2. **Branch:** `git checkout -b fix-short-description` or `feat-short-description`.
3. Make your change. Keep the diff focused — one concern per PR.
4. **Test it** (see below). A PR that hasn't been run against a real overwhelm scenario will be asked to.
5. **Open a PR** against `main`. Describe what changed, why, and which scenarios you tested.

For anything bigger than a wording fix — a new sub-action, a changed default, a new diagram type — **open an issue first** so we can agree on the shape before you build it.

## Testing your change

There's no automated harness. The skill is verified by running it.

1. Install your working copy:
   ```bash
   cp -r skills/overwhelmed ~/.claude/skills/
   ```
   (Re-copy after each edit — Claude Code live-reloads skills in `~/.claude/skills/`.)

2. Open Claude Code in a deliberately tangled project — many half-finished pieces, no obvious starting point.

3. Run the full loop and check each against the criteria:

   | Step | What to verify |
   |---|---|
   | Say "I'm lost in this project" | Soft prompt appears, doesn't take over |
   | `/overwhelmed` | Map + one next action land in one turn; map respects 15–20 node / 3–5 chunk caps |
   | `/overwhelmed park <thing>` | Item routed to the right map area, you're returned to work |
   | `/overwhelmed next` | One concrete step, startable in <5 min |
   | `/overwhelmed resume` (new session) | Re-orients from `PROJECT_MAP.md` without you re-explaining |

4. Confirm the **Done when** block at the bottom of `SKILL.md` still holds, and no [design invariant](AGENTS.md) regressed.

## Proposing a new sub-action

`overwhelmed` has four: `map`, `next`, `park`, `resume`. If you want a fifth:

1. Open an issue describing the overwhelm situation it solves that the existing four don't.
2. If accepted, add it under `## Actions` in `SKILL.md` with numbered steps, and add a row to the test table above.
3. Keep it consistent: reads/writes `PROJECT_MAP.md`, ends with one action, no walls of text.

## PR checklist

- [ ] Diff is focused on one concern
- [ ] `SKILL.md` still under ~150 lines (new detail moved to `references/`)
- [ ] Ran the test loop above against a real messy project
- [ ] No design invariant from AGENTS.md broken
- [ ] Skill stays self-contained (no dependency on other skills)
