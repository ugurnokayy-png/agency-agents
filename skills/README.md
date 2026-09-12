# 🧩 Skills

This directory holds standalone **Claude Skills** — folders containing a `SKILL.md`
(name + description frontmatter, plus an instructions body) that Claude loads on
demand, per the [Agent Skills](https://www.anthropic.com/news/agent-skills) format.

## How this differs from the rest of the repo

Everywhere else in this repo (`engineering/`, `marketing/`, `security/`, …) holds
**agent definitions**: full personas with identity, memory, and a mission, meant to
be run as a subagent. `scripts/convert.sh` can *render* those agent files into
`SKILL.md` format for tools that want it (see `tools.json`'s `"skill-md"` entries
for Osaurus and Antigravity) — but that's a generated, gitignored artifact of an
agent, not a skill in its own right.

The skills in *this* directory are different: they're hand-written, task-focused
instruction sets — not personas — meant to be used directly by Claude Code or any
other Agent-Skills-compatible host. They're not divisions (see `divisions.json` and
`scripts/check-divisions.sh`) and aren't scanned or converted by `scripts/convert.sh`.

## Contents

| Skill | What it does |
|---|---|
| [`agent-roster-navigator/`](agent-roster-navigator/SKILL.md) | Given a task, searches this repo's agent roster and recommends which agent(s) fit, plus how to invoke them in the tool you're using. |
| [`agent-scaffolder/`](agent-scaffolder/SKILL.md) | Walks through creating a new, lint-clean agent definition in the right division, following `CONTRIBUTING.md`'s conventions. |
| [`skill-scaffolder/`](skill-scaffolder/SKILL.md) | Walks through adding a new skill to this directory, keeping it consistent with the ones already here. |

## Format

Each skill is a directory containing a `SKILL.md`:

```
skills/
  <skill-name>/
    SKILL.md
```

```markdown
---
name: <skill-name>
description: <one or two sentences: what it does and when to use it>
---

<Instructions body — the actual guidance Claude follows when the skill is invoked.>
```

Keep `name` a kebab-case slug matching the directory name, and make `description`
specific enough that a host can decide when to trigger the skill from its
one-line summary alone — vague descriptions ("helps with agents") under-trigger.

## Adding a new skill

See [`skill-scaffolder/SKILL.md`](skill-scaffolder/SKILL.md) — it's the skill for
this, so following it also demonstrates how it works. In short: pick a scope
narrow enough to describe in one sentence, avoid duplicating an existing agent's
persona (that belongs in a division directory instead), and add a row to the table
above.
