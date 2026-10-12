---
name: vault-intake
description: File new input (meeting notes, a customer call, research, a Slack thread) into the decision vault. Use when the user pastes or points to new material and wants it filed, or says "file this", "update the vault", or "process these notes".
---

# Vault intake

Turn raw input into goal-linked tasks and notes, following `vault/_rules.md`. Read that file first. It is the source of truth; if this skill and `_rules.md` disagree, `_rules.md` wins.

## Before writing anything

1. Read `vault/_rules.md`.
2. Read every note in `vault/goals/` so you know which goals exist and which are `active`.
3. Skim the frontmatter of `vault/tasks/` and `vault/notes/` so you update existing notes instead of creating duplicates.

## Split the input into items

Each item is exactly one of:

| Item | Where it goes |
|---|---|
| Something someone will do, or proposes doing (even if nobody committed to it) | a task, or `parking.md` if no goal fits |
| How something works | a note, `kind: mechanism` |
| Something we don't know yet that could change the plan | a note, `kind: question` |
| A judgment we've made | a note, `kind: decision` |
| None of the above | nothing. List it under "Not filed" in your report |

## Tasks

- Fill `goal` only with a goal that exists in `vault/goals/`. Never invent a goal.
- If no goal fits, the task goes in `vault/parking.md` with its source, not in `tasks/`.
- `priority` comes from the goal, not from who asked. Don't infer it from other tasks under the same goal. Leave `priority` empty and list the task under "Needs you" unless the user told you the priority.
- Leave `owner` and `due` empty unless the input states them.
- Fill `source` with where the item came from.

## Notes

- Write `implication` as one sentence: what we will do, or not do, because of this.
- If you can't write an implication from the input, don't create the note. List the item under "Not filed — no implication" in your report.
- If a new item answers an open `question`, set that question to `settled`. If the answer is a judgment, also create a `decision` and add both to each other's `related`.

## Overturning a decision

When the input contradicts a `live` decision:

1. Never delete or rewrite the old decision.
2. Create the new decision with `supersedes: "[[old]]"` and `status: live`.
3. On the old decision, set `status: superseded` and `superseded_by: "[[new]]"`.
4. Check tasks that cite the old decision and list them in your report as "may need changes". Don't change them yourself.

## Never

- Invent facts, numbers, owners, dates, or goals not in the input. If something is missing, leave the field empty and say so.
- Delete any note.

## Report back

End with a short report:

- **Created**: file names
- **Updated**: file names and the fields that changed
- **Parked**: items moved to `parking.md`, and why
- **Not filed**: items with no implication, or noise
- **Needs you**: empty priorities, open questions this input touched, tasks that may need changes
