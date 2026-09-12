---
name: agent-scaffolder
description: Walks through creating a new agent definition for this repo (right division, valid frontmatter, required sections) so it passes scripts/lint-agents.sh and scripts/check-divisions.sh. Use when the user wants to add a new agent to the roster.
---

# Agent Scaffolder

You are helping someone add a new agent definition to this repo's roster, so
it's correct on the first pass through CI.

## 1. Confirm scope and check for overlap

Before writing anything: read `divisions.json`'s division list, then browse
the filenames (and a few `description` frontmatter fields) in the division
that looks closest. If an existing agent already covers this scope, say so —
suggest extending it instead of adding a near-duplicate. New agents should be
narrow, specific specialists, not generalists that overlap an existing one.

## 2. Pick the division

- If it fits one of the divisions already listed in `divisions.json`, use
  that directory.
- If it genuinely doesn't fit anywhere, `specialized/` is the catch-all.
- Proposing a **new** division is a bigger change than adding one agent:
  it requires a directory, a `divisions.json` entry (label/icon/color), and
  adding it to `AGENT_DIRS` in both `scripts/convert.sh` and
  `scripts/lint-agents.sh` — `scripts/check-divisions.sh` enforces all of
  these agree. Only go this route if the user actually wants a new division;
  otherwise steer them to an existing one or `specialized/`.

## 3. Name the file

Filename convention: `<division>-<kebab-case-role>.md`, e.g.
`engineering-database-reliability-engineer.md`. Look at a few existing
filenames in the target division to match the pattern.

## 4. Write the frontmatter

Required fields (missing any of these is a lint ERROR):

```yaml
---
name: Agent Name
description: "One-line description of the agent's specialty and focus"
color: colorname or "#hexcode"
---
```

Recommended, not required: `emoji` (single emoji), `vibe` (one-line
personality hook). If the agent genuinely depends on an external service to
function, add a `services:` list (`name`, `url`, `tier`) — but the agent must
still stand on its own as a persona and workflow if you stripped the API
calls out; don't wrap a vendor's quickstart guide in an agent costume.

Write `description` the way the roster does elsewhere: state the specialty
*and* the boundary — what this agent is not, if it could be confused with a
neighboring one. That boundary is what makes `agent-roster-navigator`
actually able to pick between two similar agents later.

## 5. Write the body

Follow the two-group structure `scripts/convert.sh` relies on to split
agents into tool-specific formats — get this wrong and the agent still
lints, but renders badly for tools that split persona from operations:

**Persona** (who the agent is) — headers should map here:
- `## Identity & Memory` (role, personality, background)
- `## Communication Style`
- `## Critical Rules` (boundaries/constraints)

**Operations** (what the agent does):
- `## Core Mission`
- `## Technical Deliverables` (concrete code/templates/outputs)
- `## Workflow Process` (step-by-step)
- `## Success Metrics` (specific, measurable — "under 3 seconds on 3G", not
  "fast")
- `## Advanced Capabilities`

`scripts/lint-agents.sh` requires `Identity`, `Core Mission`, and
`Critical Rules` sections (as WARNings, not hard failures) and expects at
least 50 words of body content plus at least one header mapping to each
group — check `sed -n '30,50p' scripts/lint-agents.sh` for the exact header
matching if a header isn't being recognized.

Give the agent a real, specific voice — "I default to finding 3-5 issues and
require visual proof", not "I am a helpful assistant." Vague personas are
what `CONTRIBUTING.md`'s design guidelines call out first.

## 6. Validate before opening a PR

```bash
./scripts/lint-agents.sh <division>/<new-file>.md
./scripts/check-divisions.sh   # only needed if you touched divisions.json
```

Fix every ERROR; treat WARNings as worth addressing unless there's a good
reason not to (e.g. a deliberately short agent). Then follow the normal PR
process in `CONTRIBUTING.md`.
