---
name: overwhelmed
description: Externalize a project that has become a hairball into a visible map plus one concrete next action. Use when the user says they are "overwhelmed", "lost", "stuck", "drowning", "buried", "spinning", "don't know where to start", "can't see the shape", "too many pieces/things/tabs", "spending too many cycles", or asks to "map this project" / "zoom out" / "what's next". Sub-actions: map (default), next, park, resume.
argument-hint: "[map|next|park <thing>|resume]"
allowed-tools: Read Write Edit Bash(date *)
---

# overwhelmed

The user is buried in a project and can't see its shape. Your job: externalize the hairball as a visible map, then hand them ONE next action. Nothing more.

Output discipline while this skill is active: no preamble, no recap, no closing pleasantries. Lead with the map or the action. Keep prose to a minimum — the map carries the load, not paragraphs.

## Hard rules (anti-overwhelm)

1. **Max 2 questions before you produce a visible map.** If you don't have enough, make assumptions, draw the map anyway, and flag the assumptions in one line.
2. **Never reply with a wall of text when overwhelm is the trigger.** A map or a list. Not paragraphs.
3. **Every activation ends with exactly ONE next action** the user can start in under 5 minutes.
4. **Park, don't lose.** Anything the user mentions but isn't doing now gets captured in `PROJECT_MAP.md`, never dropped.

## Soft-prompt on auto-detect

When this skill loads because the user's *language* matched (not because they typed `/overwhelmed`), do NOT take over. Surface one line and wait:

> Sounds like **[project]** is a hairball. Want me to map it? `[Y]` map · `[N]` no · `[R]` resume saved map

Only proceed once they say yes. If they typed the command explicitly, skip the prompt and go straight to the action.

## State file: `PROJECT_MAP.md`

One file per project, at the project root. This skill owns it. It survives between sessions so the map never has to be rebuilt from scratch. See [examples/PROJECT_MAP.example.md](examples/PROJECT_MAP.example.md) for the full filled-in format.

Get the current date with `date +%Y-%m-%d` before writing timestamps.

If `PROJECT_MAP.md` exists when the skill activates, read it first — the map, the locked outcome, the parked items. Use it. Don't rebuild what's already there.

Schema (sections, in order): `# Project Map: <name>` · `_Updated: <date>_` · `## One outcome (this session)` · `## The map` (a mermaid block) · `## Next 3 actions` · `## Parked`.

## Actions

Route on `$ARGUMENTS`. No argument, or `map`, → **map** (the default).

### map  (default)

The whole point of the skill. Steps:

1. Gather the pieces. Pull from: what the user just said, `PROJECT_MAP.md` if it exists, and obvious project files. Ask **at most 2** clarifying questions, only if you genuinely can't see the major chunks.
2. Draw a mermaid map. **Follow the caps and complaint→diagram mapping in [references/mermaid-caps.md](references/mermaid-caps.md).** Mark where they are now with `👉`.
3. Below the map, force focus: write/confirm the **one-outcome sentence** for this session.
4. Surface **one next action** (the top of "Next 3").
5. Write all of it to `PROJECT_MAP.md`.

Output shape after the map: the map, then one line of outcome, then one line of next action. Stop.

### next

Surface the single highest-leverage next action and, optionally, the next 3.

1. Read `PROJECT_MAP.md`.
2. Rank against the locked outcome. The #1 action is the one that moves the outcome most for the least starting friction.
3. State it as one concrete step (command / file / path), startable in <5 min.
4. Refresh "Next 3 actions" in the file.

### park &lt;thing&gt;

Capture-without-committing. The user names something they don't want to do now but can't afford to forget.

1. Read `PROJECT_MAP.md`.
2. Route the item to the map area it belongs to (match against existing chunks/keywords — don't just dump it in whatever's open).
3. Append to `## Parked` with today's date and the routed area.
4. Confirm in one line: `Parked: "<thing>" → <area>. Back to <current action>.` Then return to what they were doing. Do not expand on the parked item.

### resume

Re-orient at the start of a session without re-explaining the project.

1. Read `PROJECT_MAP.md`.
2. Output, briefly: the locked outcome (if any), the map, and the top next action. Surface any parked items as a short list so they're not forgotten.
3. Ask one thing: continue the locked outcome, or re-map?

## When the map isn't the problem

If, after one map, the user is still stuck, the problem is usually focus, not visibility. Drop the map and force the single outcome sentence: *"What is the one outcome that would make this session a win?"* Lock it to the file. Then `next`.

## Done when

- A visible map + one next action landed within one turn.
- The user can park something and find it later.
- A later session can `resume` from the file without the user re-explaining.
