---
name: skill-scaffolder
description: Walks through adding a new Claude Skill to this repo's skills/ directory, keeping it consistent with the ones already there and distinct from an agent definition. Use when the user wants to add a new skill (not agent) to the repo.
---

# Skill Scaffolder

You are helping someone add a new skill to `skills/` in this repo. This
directory is small and deliberately curated — read `skills/README.md` first
for how it differs from the per-division agent directories (`engineering/`,
`marketing/`, etc.) before scaffolding anything.

## 1. Check it's actually a skill, not an agent

A **skill** here is a task-focused instruction set with no persona: it
doesn't have an identity, memory, or communication style, and it isn't meant
to be "activated" as a character. If what's being proposed is really a
specialist persona (e.g. "a skill that acts like a database expert"), it
belongs in a division directory instead — point to `agent-scaffolder` for
that.

A skill is a good fit here when it's a **repeatable procedure** Claude should
follow when triggered — e.g. "how to review a PR against this repo's style
rules", "how to pick an agent from the roster", "how to scaffold a new X".

## 2. Check for overlap

Read the table in `skills/README.md` and skim the existing `SKILL.md` files.
If an existing skill already covers this, extend it rather than adding a
near-duplicate with a slightly different name.

## 3. Pick a name and scope

- Directory name: kebab-case, verb-or-noun-phrase describing the procedure
  (e.g. `agent-scaffolder`, not `helper` or `utils`).
- Keep the scope to one sentence. If the description needs "and" twice to
  summarize it, it's probably two skills.

## 4. Create the files

```
skills/<skill-name>/SKILL.md
```

```markdown
---
name: <skill-name>
description: <specific, one-two sentences: what it does AND when to use it>
---

# <Human-readable title>

<Numbered or headed steps Claude should actually follow. Be concrete about
what to read, what to check, and what "done" looks like — not vague advice.>
```

The `description` is what a host uses to decide whether to trigger the skill
at all — a vague one ("helps with the repo") under-triggers. State the
concrete situation that should invoke it, the way the existing skills'
descriptions do.

## 5. Register it

Add a row to the table in `skills/README.md`:

```markdown
| [`<skill-name>/`](<skill-name>/SKILL.md) | <what it does, one line> |
```

## 6. Sanity-check

- `name` in the frontmatter matches the directory name exactly.
- The skill doesn't need `divisions.json`, `scripts/check-divisions.sh`,
  `scripts/convert.sh`, or `scripts/lint-agents.sh` changes — those only
  govern the division/agent directories, not `skills/`. If you find yourself
  editing any of those files for a plain skill addition, stop and re-check
  step 1 — it likely means what's being added is actually an agent.
- The instructions body is something you could hand to a fresh Claude
  session with zero other context and have it produce the right outcome.
