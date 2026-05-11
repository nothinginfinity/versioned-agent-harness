## SPEC-004 — Memory Layer
*version: 0.1 | status: draft | owner: alice | date: 2026-05-11*

---

## 1. Problem
Without a memory layer, agents rely on transient chat context and repeatedly rediscover project state. When multiple agents share state without ownership rules, memory drifts and becomes contradictory.

---

## 2. Goal
Define a stable memory layer for harnesses, including file roles, update rules, and the single-writer memory steward pattern.

---

## 3. Scope
**In scope**
- Canonical memory files
- Shared vs local memory
- Memory steward ownership
- Proposed-update workflow
- Session summaries and compressed memory
- Audit guidance

**Out of scope**
- Vector databases
- Embedding pipelines
- Search ranking internals
- External persistence systems

---

## 4. Design / Approach
Memory is the durable project state that survives beyond an individual chat session.

### Memory types
A harness may use multiple memory layers:
- **Shared project memory** — canonical state used across a team
- **Agent-local memory** — role-specific notes or short-term working state
- **Session summary memory** — compressed summary of a single run
- **Reference memory** — facts, glossary, mappings, or IDs

### Canonical shared memory
Shared memory should live in a single durable file such as:

```text
spaces/gists/brain.json
```

This file holds compressed state, decisions, open questions, and durable project memory.

### Memory steward
Shared memory has exactly one `memory_steward`.

**Rules:**
- Only the steward writes canonical shared memory.
- Other agents may propose memory changes.
- Proposals may travel via inbox, mail, or bulletin.
- Read-only agents never write shared memory directly.
- Reviewer agents may recommend corrections.

### Update workflow
Recommended pattern:
1. Agent completes meaningful work.
2. Agent proposes a memory delta.
3. Memory steward reviews the proposal.
4. Steward updates shared memory.
5. Update is reflected in Git history.

### Memory quality rules
Good memory should be:
- Compressed
- Durable
- Non-duplicative
- Specific
- Easy for humans to inspect

---

## 5. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Define memory types | alice | done |
| T-002 | Define steward update rules | alice | done |
| T-003 | Define proposal workflow | alice | done |
| T-004 | Add memory file examples later | alice | pending |

---

## 6. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | Should local memory also require a steward? | jared | no |
| Q-002 | Should memory deltas have a dedicated schema later? | jared | no |

---

## 7. Changelog

| Version | Date | Change |
|---------|------|--------|
| 0.1 | 2026-05-11 | Initial draft |
