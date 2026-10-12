---
name: vault-gate
description: Run the monthly gate check on the decision vault and report what has drifted from the goals. Use when the user says "run the gate", "monthly review", "are we on track", or at the start of a new phase.
---

# Vault gate

A read-only audit against `vault/_rules.md`. Report problems; don't fix them unless the user asks.

## Checks, in this order

1. **Orphan tasks.** Tasks in `vault/tasks/` with an empty `goal`. Any result means the month failed the gate. List each one with its `source`.
2. **Tasks on inactive goals.** Tasks whose `goal` points to a goal that is missing or not `active`.
3. **Overdue P0s.** `priority: P0`, `status` not `done`, `due` before today. List only overdue ones here; tasks due soon are not overdue.
4. **Blocked chains.** Tasks with `status: blocked`, and what blocks them. Flag a blocker that is itself `done` or `settled`; the task may be unblocked.
5. **Notes without an implication.** Any note with an empty `implication`.
6. **Broken decision links.**
   - `superseded` with an empty `superseded_by`
   - `supersedes` pointing to a note that isn't `superseded`
   - `superseded_by` and `supersedes` that don't point back at each other
7. **Open questions by goal.** Count `kind: question`, `status: open` per goal. A goal with open questions and no task to answer them is worth flagging.
8. **Parking.** List what's in `vault/parking.md`, so the user can decide whether anything now has a goal.

## Then

Remind the user to update the phase in the "this phase" view of `bases/02-p0.base` if a new month has started.

## Report format

Start with one line: **Gate passed** (check 1 is empty) or **Gate failed: N orphan tasks**. Then one short section per check that found something. Skip checks with no findings.
