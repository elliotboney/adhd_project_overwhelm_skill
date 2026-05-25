# Mermaid map caps & complaint→diagram mapping

Loaded on demand by the `map` action. These caps exist because of working-memory limits — a map past these sizes stops being a handle and becomes more hairball.

## Node caps

- **15–20 nodes maximum.** If reality has more, collapse detail into grouped nodes. The map is a handle, not the territory.
- **3–5 top-level chunks.** Not 8.
- Use `graph TD`. Group each chunk with a `subgraph`.
- Mark current position with `👉 you are here` on one node.
- Parked/blocked pieces go in a separate `Parked` subgraph or dimmed — never let them pull focus.
- Micro-steps in "Next 3" should each be startable in **3–10 min**. Pad time estimates **1.5–2×** — ADHD time-estimates run optimistic.

## Complaint → diagram type

Match the *shape* of the overwhelm to the diagram, not every complaint to a flowchart:

| What the user says | Diagram that fits |
|---|---|
| "too many pieces", "can't see the shape" (default) | `graph TD` with subgraph chunks |
| "can't decide", "don't know which to pick" | quadrant / 2×2 (impact vs effort) |
| "time disappears", "no idea where the hours go" | `timeline` or `gantt` |
| "no energy", "where is it all going" | pie / Sankey of where effort is spent |
| "what depends on what", "blocked" | `graph LR` dependency chain |

## Overwhelm→action pattern (from neurodivergent-visual-org)

When the user is paralyzed, the map's job is to lead to a first move, not to be complete:

1. Acknowledge the emotional-state node ("this feels like a lot" — one beat, don't dwell).
2. Brain-dump every piece into nodes (rough is fine).
3. Pick the **one tiniest first step** and surface only that.
4. Note the MVP line: "ship V1 of this and stop" — guard against scope creep.
