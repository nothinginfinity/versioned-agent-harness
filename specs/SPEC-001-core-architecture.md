## SPEC-001 — Core Architecture
*version: 1.2 | status: draft | owner: alice | date: 2026-05-11*

---

## 1. Problem
LLM agents are often controlled by scattered prompts, hidden chat context, and informal instructions. This makes behavior difficult to reproduce, audit, update, or safely share across humans and projects.

---

## 2. Goal
Define a reusable version-controlled harness architecture that makes LLM agents portable, role-specific, inspectable, and auditable.

---

## 3. Scope
**In scope**
- Agent boot files
- Skill modules (Markdown + YAML frontmatter)
- Memory files
- Inbox, outbox, and bulletin surfaces
- Permission boundaries
- Schema definitions
- Git-based audit trail
- Parent/child harness references (v1 schema support, flat execution)

**Out of scope**
- A specific app implementation
- Vendor-specific LLM APIs
- Model training or fine-tuning
- Full security sandboxing
- Nested harness execution engine (deferred to v2)

---

## 4. Design / Approach
A harness is the operating envelope around an LLM agent.

```text
[Harness Boot File]
    ↓
[Startup Reads]
    ↓
[Memory + Inbox + Bulletin]
    ↓
[Skill Trigger Detection]
    ↓
[Lazy-Loaded Skill]
    ↓
[Role-Specific Work]
    ↓
[Output / Message / Commit / Verbal Report]
    ↓
[Audit Trail]
```

The harness is stored as version-controlled files in a repository. Changes to agent behavior are reviewable through diffs and changelogs.

### Team Harness Model (v1 schema, v2 execution)

Harnesses can be flat (single agent) or structured as a parent team harness with child agent harnesses.

```text
Team Harness
├── Builder Child Harness
├── Reviewer Child Harness
├── Ops Child Harness
└── Brainstorm Read-Only Child Harness
```

A team harness defines shared project rules, memory, and bulletin surfaces. A child harness defines one agent’s role inside that team. Example:

```yaml
id: podcast-pulse-team
type: team-harness
shared_memory: memory/project.json
shared_bulletin: bulletin.md
children:
  - harnesses/builder-agent.harness.md
  - harnesses/reviewer-agent.harness.md
  - harnesses/brainstorm-readonly.harness.md
```

See `harnesses/repo-copilot-team.harness.md` for the first real reference implementation of this model.

**v1 policy:** Schema supports parent/child references. Execution remains flat. Nested orchestration deferred to v2.

### Skill File Format

Skills are Markdown files with required YAML frontmatter.

```yaml
---
id: spec-writing
version: 0.1
status: draft
owner: alice
triggers:
  - write a spec
  - draft requirements
  - create implementation plan
outputs:
  - spec
---
# Skill: Spec Writing
## Purpose
...
```

This gives humans readable files and gives tools/agents machine-parseable metadata without a separate companion file.

### Boot File: Current Phase Field

Every active project harness boot file must include a `current_phase` field. Generic reusable templates may omit it.

```text
current_phase: Phase 1 — Core Specs
```

Rationale: the current phase tells the LLM what kind of decisions are appropriate, preventing out-of-phase work.

### Minimum Viable Harness (Small Business)

The smallest useful harness is:

```text
business-assistant/
├── boot.md
├── memory.json
├── inbox.md
├── bulletin.md
└── skills/
    └── customer-support.skill.md
```

One boot file, one memory file, one inbox, one bulletin, at least one skill. That is the unit of sale for a small business deployment.

### Bulletin vs. Message Schemas

Kept separate. They serve different purposes:

| Shape | Purpose | Has `to:` field? |
|-------|---------|------------------|
| message | Directed task or reply between agents or humans | Yes |
| bulletin | Shared delta feed for observers | No |

A message asks someone to do something. A bulletin tells observers what changed. Both schemas may derive from a shared `base-communication.schema.json` in a future version.

### Admin Harnesses

Stored under `harnesses/admin/` in the same repo for v1. Separate repo only when security or client isolation requires it.

---

## 5. Core Principles
1. **Harness over prompt.** The system prompt is only one part of the operating environment.
2. **Role-specific agents.** Each agent should have a clear identity and responsibility boundary.
3. **Lazy-loaded skills.** Skills load only when relevant.
4. **Read/write separation.** Observer agents should be able to inspect without mutating work.
5. **Versioned behavior.** Instruction changes are committed, reviewed, and traceable.
6. **Human-readable first.** Markdown is the default control surface.
7. **Schema-backed where useful.** JSON schemas define machine-readable contracts.
8. **Team harnesses unlock coordination.** A parent harness + child harnesses turns one LLM with one prompt into a coordinated team of role-bound agents operating from shared project law.

---

## 6. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Define boot file anatomy | alice | pending |
| T-002 | Define skill module anatomy | alice | pending |
| T-003 | Define memory layer contract | alice | pending |
| T-004 | Define communication surfaces | alice | pending |
| T-005 | Define audit and permission model | alice | pending |
| T-006 | Add team-harness type to harness.schema.json | alice | done |
| T-007 | Update skill files with YAML frontmatter | alice | done |
| T-008 | Create harnesses/admin/ folder | alice | done |
| T-009 | Create repo-copilot-team.harness.md reference example | alice | done |

---

## 7. Open Questions

| # | Question | Owner | Resolved | Decision |
|---|----------|-------|----------|----------|
| Q-001 | Should harnesses support nested child harnesses? | jared | yes | v1 schema supports parent/child references; execution remains flat. v2 adds orchestration. |
| Q-002 | Should skills be plain markdown only or include JSON metadata? | jared | yes | Skills use Markdown with required YAML frontmatter. |
| Q-003 | What is the minimum viable harness for a small business user? | jared | yes | boot.md + memory.json + inbox.md + bulletin.md + at least one skill. |
| Q-004 | Should every boot file include a current phase field? | jared | yes | Required for active project harnesses; optional for generic templates. |
| Q-005 | Should bulletin and message schemas stay separate? | jared | yes | Separate schemas. May share a base-communication.schema.json in a future version. |
| Q-006 | Should admin harnesses live in a separate repo? | jared | yes | Same repo under harnesses/admin/ for v1; separate repo only when security/client isolation requires it. |

---

## 8. Changelog

| Version | Date | Change |
|---------|------|--------|
| 1.0 | 2026-05-11 | Initial draft |
| 1.1 | 2026-05-11 | Resolved Q-001 through Q-006; added team harness model, skill frontmatter spec, boot phase field rule, MVH definition, bulletin/message separation rationale, admin harness placement |
| 1.2 | 2026-05-11 | Marked T-008 done; added T-009 (repo-copilot-team reference example, done); added SPEC-001 cross-reference to harnesses/repo-copilot-team.harness.md |
