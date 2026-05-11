---
id: repo-copilot-team
version: 0.1
type: team-harness
mode: admin
status: draft
agent_role: project-orchestration-team
current_phase: Phase 3 — Inbox Architecture
shared_memory: spaces/gists/brain.json
shared_bulletin: spaces/brainstorm/bulletin.md
children:
  - harnesses/builder-agent.harness.md
  - harnesses/reviewer-agent.harness.md
  - harnesses/brainstorm-readonly.harness.md
---

# Team Harness: repo-copilot

*version: 0.1 | type: team-harness | mode: admin | status: draft*

---

## 1. Team Purpose

This team harness coordinates the LLM agents that build and maintain the `repo-copilot` system — a repo-native AI workspace framework. The team operates from shared memory and a shared bulletin surface, with each agent bound to a specific role and permission mode.

The repo-copilot team is the reference implementation that this entire architecture is extracted from.

---

## 2. Child Agents

| Agent | Harness File | Mode | Primary Responsibility |
|-------|-------------|------|------------------------|
| Alice (orchestration) | `harnesses/builder-agent.harness.md` | write-capable | Coordinates work, manages inbox, pushes files |
| Alice-Review | `harnesses/reviewer-agent.harness.md` | read-mostly | Audits specs, PRs, and architecture changes |
| Alice-Brainstorm | `harnesses/brainstorm-readonly.harness.md` | read-only | Plans, critiques, and proposes without writing |

> **v1 execution note:** Each child agent runs independently in its own session. A human (Jared) acts as the orchestration layer, routing tasks across agents via inbox messages. Automated orchestration is a v2 concern.

---

## 3. Shared Resources

| Resource | Path | Purpose |
|----------|------|---------|
| Shared memory | `spaces/gists/brain.json` | Compressed project state, decisions, open questions |
| Shared bulletin | `spaces/brainstorm/bulletin.md` | Delta feed surfaced to all agents, especially brainstorm |
| Boot instructions | `spaces/gists/G-000-alice-boot.md` | Alice’s full operating instructions |
| Skills registry | `spaces/gists/G-005-alice-skills.md` | Lazy-load triggers and skill routing rules |

---

## 4. Shared Rules

All agents on this team observe the following rules regardless of their individual harness:

1. **Read before writing.** No agent modifies files without first reading relevant context.
2. **Bundle writes.** All file changes in a turn go into a single `push_files` commit.
3. **Last action is a push.** If any files were modified, the last action of the turn must be `push_files`.
4. **Preserve changelogs.** Every spec and harness file that changes gets an updated changelog entry.
5. **Surface important changes to the bulletin.** Any decision, blocker, or architectural shift should produce a BLT-XXX entry in `shared_bulletin`.
6. **Full repo paths in `ref:` fields.** Bulletins and messages must cite exact file paths, not vague descriptions.
7. **Never describe code without pushing it.** Verbal-only code drafts are not valid output.

---

## 5. Communication Surfaces

| Surface | Path | Used by |
|---------|------|---------|
| Alice inbox | `spaces/alice/inbox.md` | Jared → Alice (master tasks) |
| Alice-Ops inbox | `spaces/alice/inbox-ops.md` | Jared → Alice-Ops |
| Alice-Review inbox | `spaces/alice/inbox-review.md` | Jared → Alice-Review |
| Internal mail | `spaces/alice/mail.md` | Agent ↔ Agent |
| Outbox | `spaces/alice/outbox.md` | Alice → external agents |
| Bulletin | `spaces/brainstorm/bulletin.md` | All agents → Brainstorm observer |

---

## 6. Escalation Rules

| Situation | Action |
|-----------|--------|
| A spec conflict or ambiguity blocks a task | Pause work, post BLT entry, surface to Jared via inbox |
| Two agents produce conflicting outputs | Alice (orchestration) holds, surfaces conflict in bulletin, waits for human resolution |
| A write-capable agent encounters a hard rule violation | Abort the write, report verbally, do not push partial state |
| A decision requires Jared’s sign-off | Post to Alice inbox with `priority: blocking` |

---

## 7. Audit Rules

- All committed files must include a version field and a changelog.
- Memory (`brain.json`) is updated at the end of sessions where meaningful decisions were made.
- Turn logs are written to `.github/turns/<session>/<cid>/turn.json`.
- Read-only agents acknowledge bulletin entries verbally in their session summary.
- Any change to a child harness file requires a changelog bump in that harness file and a BLT entry.

---

## 8. What This Example Demonstrates

This file is both a working harness *and* a teaching document. It shows:

- How a team harness references child harnesses
- How shared memory and bulletin are declared
- How child roles and permission modes are separated
- How shared rules apply team-wide, independent of individual harness mode
- How communication surfaces are structured for human-to-agent and agent-to-agent routing
- How escalation paths are explicit rather than assumed

The pattern here generalizes. Swap the child harnesses, memory path, and bulletin path, and you have a new team: PodcastPulse, DealScout, a small business assistant, a research team, or any other coordinated LLM deployment.

---

## 9. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | In v2, should the team harness also define agent spawn order? | jared | no |
| Q-002 | Should child harnesses declare their parent team harness explicitly? | jared | no |
| Q-003 | When memory is shared, which agent is responsible for writing it? | jared | no |

---

## 10. Changelog

| Version | Date | Change |
|---------|------|--------|
| 0.1 | 2026-05-11 | Initial draft — first reference implementation of team-harness pattern |
