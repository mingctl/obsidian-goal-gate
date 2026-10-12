# decision-vault

**A goal-gated work system for people who own outcomes.** Nothing gets on your list unless it moves a goal.

An Obsidian vault plus two agent skills (Claude Code and Codex). It's built for PMs, founders, and anyone pulled in five directions at once who needs to stay on what matters.

<!-- TODO: 30-second GIF: paste meeting notes → agent files a task, parks a distraction, supersedes an old decision -->

## Why

When you own outcomes, everyone has a request and every request sounds reasonable. Drift doesn't come from one bad choice. It comes from a hundred small yeses.

Most productivity systems catch drift after the fact: you review your week and notice you spent it on the wrong things. This one stops it at the door:

- **No goal, no task.** A task that can't name the goal it moves doesn't enter your list. It goes to `parking.md`. It isn't rejected; it just can't take time from a goal.
- **Goals are questions with a gate.** Not "improve reliability" but *"Can it run reliably?"*, answered when *3 external workloads run for 2 weeks*. You always know what done looks like.
- **Every note says "so what".** A note without a one-line `implication` isn't a note. That's a bookmark, not understanding.
- **You can see why you changed your mind.** Overturned judgments are never deleted. They're marked `superseded` and linked to what replaced them.
- **A monthly gate.** Once a month, check the orphan-tasks table. If it's empty, you didn't drift.

## The rules

The full rules are in [`vault/_rules.md`](vault/_rules.md). The short version:

**Goal**: a question, a gate, and a phase (the month it's the focus).

**Task**: has a required `goal`. Priority comes from the goal, never from whoever asked.

**Note**: one of three kinds, defined by how it changes over time:

| kind | Can it change? | status |
|---|---|---|
| `mechanism`: how something works | Doesn't expire | `live` |
| `question`: something you don't know yet | Gets closed | `open` → `settled` |
| `decision`: a judgment you've made | Gets overturned | `live` → `superseded` |

## Quickstart

1. Clone this repo and open `vault/` as a vault in Obsidian. The tables need the **Bases** core plugin enabled.
2. Open `00-HOME.md`. You'll see the example product **Kiln**, a fictional job scheduler. One task, *Slack integration*, breaks the rules on purpose so you can see the orphan check catch it.
3. Delete the Kiln notes in `goals/`, `tasks/`, and `notes/`, then write your own goals from `templates/goal.md`.

### With an agent

Run Claude Code or Codex from the repo root. `AGENTS.md` points both to the rules and the skills.

- **File new input:** paste meeting notes, a call summary, or research and say *"file this"*. The [`vault-intake`](.claude/skills/vault-intake/SKILL.md) skill sorts each item into a task, a note, parking, or nothing, and tells you what it couldn't decide.
- **Monthly gate:** say *"run the gate"*. The [`vault-gate`](.claude/skills/vault-gate/SKILL.md) skill reports orphan tasks, overdue P0s, stale blockers, notes without an implication, and broken decision links. It's read-only.

The agent never invents goals, owners, dates, or priorities, and never deletes a note.

## How it compares

| | [obsidian-claude-pkm](https://github.com/ballred/obsidian-claude-pkm) | [obsidian-mind](https://github.com/breferrari/obsidian-mind) | decision-vault |
|---|---|---|---|
| Scope | Your whole life: 3-year vision down to daily notes | Your career memory: work log, 1:1s, brag doc | One job's outcomes: a quarter, a few goals |
| How it handles drift | Reviews activity against goals after the fact | Not its focus | Blocks goal-less tasks at entry |
| Goals | Things to achieve | A North Star doc | Questions with a gate |
| Changing your mind | Not a focus | Decision records with a status | Superseded judgments stay linked to their replacements |

They're great at what they do. Pick this one if your problem is staying on the few things that matter at work.

## Structure

```
vault/
├── 00-HOME.md        dashboard embedding all tables
├── _rules.md         the rules (source of truth)
├── parking.md        everything without a goal
├── goals/  tasks/  notes/
├── bases/            7 Obsidian Bases views
└── templates/
.claude/skills/       vault-intake, vault-gate
AGENTS.md             entry point for Codex and Claude Code
```

## License

MIT
