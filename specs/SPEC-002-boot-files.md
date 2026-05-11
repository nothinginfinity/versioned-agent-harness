## SPEC-002 — Boot Files
*version: 0.1 | status: draft | owner: alice | date: 2026-05-11*

---

## 1. Problem
LLM agents often begin work from implicit context, hidden system prompts, or inconsistent startup routines. Without a defined boot contract, behavior drifts across sessions and becomes hard to audit or reproduce.

---

## 2. Goal
Define a standard boot file format and startup read sequence for versioned agent harnesses.

---

## 3. Scope
**In scope**
- Boot file purpose and anatomy
- Required and optional frontmatter fields
- Startup read ordering
- Active-project vs generic-template rules
- Parent/team context references
- Phase awareness

**Out of scope**
- Skill internals
- Memory schema internals
- Communication message formats
- Runtime orchestration engine

---

## 4. Design / Approach
A boot file is the first durable instruction surface an agent reads before acting. It establishes identity, mode, startup reads, permissions, and the current project phase.

### Required boot metadata
Every active harness boot file should provide:

```yaml
---
id: alice-builder
version: 0.1
type: agent-harness
mode: write-capable
status: active
agent_role: builder
current_phase: Phase 1 — Core Specs
startup_reads:
  - spaces/gists/G-000-alice-boot.md
  - spaces/gists/brain.json
  - spaces/alice/inbox.md
skills:
  - skills/spec-writing.skill.md
communication_surfaces:
  - spaces/alice/inbox.md
  - spaces/alice/mail.md
---
```

### Boot sections
After frontmatter, a boot file should contain:
1. Agent identity
2. Operating purpose
3. Core rules
4. Startup read policy
5. Write permissions
6. Escalation rules
7. Changelog

### Startup read ordering
Recommended startup sequence:
1. Read the primary boot gist / operating instructions.
2. Read live memory.
3. Read inbox or task surface.
4. Read bulletin surfaces if relevant.
5. Load skills only when needed.

This keeps expensive context modular and makes the boot flow auditable.

### Generic vs active harnesses
- **Generic templates** may omit `current_phase` and `parent_harness`.
- **Active project harnesses** must include `current_phase`.
- **Reusable child harnesses** should omit `parent_harness` unless bound to a specific team copy.

### Team context
If a child harness is team-bound, it may include:

```yaml
parent_harness: harnesses/repo-copilot-team.harness.md
```

The team harness remains canonical via `children[]`.

---

## 5. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Define required boot frontmatter fields | alice | done |
| T-002 | Define startup read ordering | alice | done |
| T-003 | Document generic vs active harness rules | alice | done |
| T-004 | Add boot file example to repo docs later | alice | pending |

---

## 6. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | Should startup reads support priority levels later? | jared | no |
| Q-002 | Should boot files declare allowed tools directly or by reference? | jared | no |

---

## 7. Changelog

| Version | Date | Change |
|---------|------|--------|
| 0.1 | 2026-05-11 | Initial draft |
