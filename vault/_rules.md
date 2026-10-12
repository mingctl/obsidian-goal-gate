---
type: meta
---
# Rules

Three note types. Every field below is required unless marked optional.

## Goal

Each goal is a **question** the product has to answer, with a gate that says when it is answered.

```yaml
type: goal
id: G1
phase: 2026-10                # the month this goal is the focus
question: Can it run reliably?
revenue_gate: 3 external workloads running for 2 weeks
status: active                # active / done / dropped
```

## Task

```yaml
type: task
goal: G1              # REQUIRED. If you can't fill it, the task doesn't exist yet. It goes to parking.md.
phase: 2026-10
priority: P0          # P0 / P1 / P2 / P3
status: todo          # todo / doing / blocked / done / parked
owner:
due:
blocked_by: []        # ["[[Another task]]"]
source:               # where this came from: meeting, customer call, roadmap review
```

### Three hard rules

1. A task with an empty `goal` does not go in `tasks/`. It goes in `parking.md`.
2. `priority` is set by the goal, never by whoever asked for it.
3. On each monthly gate day, open `03-orphan-tasks.base` first. The month is on track only if that table is empty.

## Note

```yaml
type: note
kind: mechanism       # mechanism / question / decision
goal: [G1, G2]        # one or more
status: live          # see lifecycle table below
implication:          # one sentence: so what do we do, or not do
supersedes:           # decision only
superseded_by:        # decision only
related: []
```

### The three kinds differ by lifecycle

| kind | Can it change? | status flow |
|---|---|---|
| `mechanism`: how something works | Doesn't expire | always `live` |
| `question`: an open question | Gets closed | `open` → `settled` |
| `decision`: a judgment we've made | Gets overturned | `live` → `superseded` |

### Two hard rules

1. **If you can't write the `implication`, it isn't a note.** No goal, no place in `notes/`. That's a bookmark, not understanding.
2. **Overturning a decision never deletes the old one.** Set the old one to `superseded` and fill `superseded_by`. Fill `supersedes` on the new one. `07-live-decisions.base` shows only the `live` ones.
