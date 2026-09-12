# Project Instructions — The Agency (agency-agents)

This file is read automatically by Claude Code sessions working in this
repository. It captures standing rules that apply across sessions, not
just the conversation that created them.

## Legal Specialist Agents — Standing Rules

This repo's legal-domain roster (`specialized/legal-document-review.md`,
`specialized/legal-client-intake.md`, `specialized/legal-billing-time-tracking.md`,
`specialized/legal-builder-hub.md`, `specialized/commercial-legal.md`,
`specialized/ai-governance-legal.md`) encodes rules that are binding for
**any future work in this repo that touches legal, compliance, or
AI-governance content** — new agents, edits to existing ones, or
integration/tooling work that plugs a legal or AI-governance data source
into an agent. Apply these before shipping such work, not just when
writing the agent files themselves:

1. **Verify source provenance before integrating anything.** Before wiring
   any third-party legal-data source, court/registry API, or MCP server
   into an agent, run the Source Vetting Checklist from
   `specialized/legal-builder-hub.md` — check maintainer, license, and
   whether the code actually matches what the README claims. Treat a repo
   whose README pushes an unexplained downloadable "release" archive
   instead of documented API usage as a rejected, compromised source —
   don't integrate it, and say so explicitly. (This rule exists because a
   candidate integration evaluated in this repo turned out to be exactly
   that: a trojanized clone of a legitimate open-source project.)
2. **No legal advice, ever.** Every legal-domain agent must state plainly
   that it does not give legal advice, and must frame its output as
   "flagged for attorney/compliance review" rather than a conclusion.
3. **Citation integrity for legal research.** Any agent or tool that
   surfaces case law, statutes, or regulatory text must trace every claim
   to a citeable primary source — no bare summaries presented as fact.
4. **Commercial dealmaking terms follow `commercial-legal.md`'s
   must-hold vs. negotiable framework.** A must-hold term (liability caps,
   IP ownership, indemnification scope) is never silently traded away
   under deal-timeline pressure — any such trade must be explicit and
   attributable to whoever authorized it.
5. **AI-system work follows `ai-governance-legal.md`'s risk
   classification.** Before shipping an agent or integration that builds,
   fine-tunes, or embeds a third-party AI system, classify it (provider vs.
   deployer, EU AI Act risk tier, prohibited-use check) rather than
   assuming it's out of scope for governance review.

Keep this section current as the legal agent roster changes — when a new
legal-domain specialist is added, fold its critical rules in here too.
