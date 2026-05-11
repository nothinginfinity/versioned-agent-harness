## SPEC-001 — Core Architecture
*version: 1.3 | status: draft | owner: alice | date: 2026-05-11*

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
- Memory steward pattern
- Advisory activation order (v1); executable orchestration (v2)

**Out of scope**
- A specific app implementation
- Vendor-specific LLM APIs
- Model training or fine-tuning
- Full security sandboxing
- Nested harness execution engine (deferred to v2)
- Automated agent spawning (deferred to v2)

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

A team harness defines shared project rules, memory, bulletin surfaces, activation order, and the memory steward. A child harness defines one agent's role inside that team.

See `harnesses/repo-copilot-team.harness.md` for the first real reference implementation of this model.

**v1 policy:** Schema supports parent/child references. Execution remains flat. Nested orchestration deferred to v2.

### Activation Order (v1: advisory)

Team harnesses may define `activation_order` — the recommended sequence for a human orchestrator to activate child agents in a session.

```yaml
activation_order:
  - harnesses/brainstorm-readonly.harness.md
  - harnesses/builder-agent.harness.md
  - harnesses/reviewer-agent.harness.md
```

Typical default order: **Brainstorm → Builder → Reviewer → Ops/Memory**. Task-specific workflows may override this. In v1 the field is advisory and human-executed. In v2 it becomes executable by an orchestration layer.

### Memory Steward Pattern

Shared memory has exactly one `memory_steward`. By default this is the orchestration agent.

```yaml
memory_steward: alice
shared_memory: spaces/gists/brain.json
```

**Rules:**
- Only the memory steward writes to `shared_memory`.
- Builder, reviewer, and brainstorm agents may **propose** memory updates via mail, inbox, or bulletin.
- Brainstorm (read-only) agents never write shared memory directly.
- Reviewer agents may propose corrections but do not commit them.
- Ops agents may write operational logs but not canonical project memory unless explicitly delegated.

This prevents drift, contradictions, and competing summaries from concurrent agents.

### Parent/Child Back-Reference (optional)

Child harnesses may declare an optional `parent_harness` field for traceability.

```yaml
parent_harness: harnesses/repo-copilot-team.harness.md
```

If a child harness is generic and reusable across multiple teams, `parent_harness` should be omitted or set to `null`. The team harness `children[]` list is always the canonical source of truth for membership.

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

### Boot File: Current Phase Field

Every active project harness boot file must include a `current_phase` field. Generic reusable templates may omit it.

```text
current_phase: Phase 1 — Core Specs
```

### Minimum Viable Harness (Small Business)

```text
business-assistant/
├── boot.md
├── memory.json
├── inbox.md
├── bulletin.md
└── skills/
    └── customer-support.skill.md
```

One boot file, one memory file, one inbox, one bulletin, at least one skill.

### Bulletin vs. Message Schemas

| Shape | Purpose | Has `to:` field? |
|-------|---------|------------------|
| message | Directed task or reply between agents or humans | Yes |
| bulletin | Shared delta feed for observers | No |

Both may derive from a shared `base-communication.schema.json` in a future version.

### Admin Harnesses

Stored under `harnesses/admin/` in the same repo for v1. Separate repo only when security or client isolation requires it.

---

## 5. Core Principles
1. **Harness over prompt.** The system prompt is only one part of the operating environment.
2. **Role-specific agents.** Each agent should have a clear identity and responsibility boundary.
3. **Lazy-loaded skills.** Skills load only when relevant.
4. **Read/write separation.** Observer agents can inspect without mutating work.
5. **Versioned behavior.** Instruction changes are committed, reviewed, and traceable.
6. **Human-readable first.** Markdown is the default control surface.
7. **Schema-backed where useful.** JSON schemas define machine-readable contracts.
8. **Team harnesses unlock coordination.** A parent harness + child harnesses turns one prompt into a coordinated team of role-bound agents operating from shared project law.
9. **One memory steward.** Shared memory has a single designated writer; all others propose.

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
| T-010 | Add activation_order, parent_harness, memory_steward to harness.schema.json | alice | done |
| T-011 | Add Principle 9 (one memory steward) | alice | done |

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
| Q-007 | Should v2 team harnesses define agent spawn order? | jared | yes | Yes, as advisory `activation_order` in v1 (human-executed); executable orchestration in v2. |
| Q-008 | Should child harnesses declare their parent team harness explicitly? | jared | yes | Optional `parent_harness` back-reference. Team harness `children[]` remains canonical. Generic/reusable child harnesses omit it. |
| Q-009 | When memory is shared, which agent is responsible for writing it? | jared | yes | One `memory_steward` (default: orchestration agent). Other agents propose updates; only steward writes. |

---

## 8. Changelog

| Version | Date | Change |
|---------|------|--------|
| 1.0 | 2026-05-11 | Initial draft |
| 1.1 | 2026-05-11 | Resolved Q-001–Q-006; team harness model, skill frontmatter, boot phase field, MVH, bulletin/message separation, admin placement |
| 1.2 | 2026-05-11 | T-008/T-009 done; cross-reference to repo-copilot-team.harness.md |
| 1.3 | 2026-05-11 | Resolved Q-007–Q-009; added activation_order, memory steward pattern, optional parent back-reference; added Principle 9; T-010/T-011 done |
