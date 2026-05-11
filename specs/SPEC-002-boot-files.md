## SPEC-002 — Boot Files
*version: 1.0 | status: draft | owner: alice | date: 2026-05-11*

---

## 1. Problem
LLM agents need consistent startup behavior. Without a boot file, each session depends on memory, chat history, or manual re-explanation.

---

## 2. Goal
Define the standard anatomy of a boot file for a versioned LLM harness.

---

## 3. Scope
**In scope**
- Agent identity
- Startup sequence
- Read/write policy
- Hard rules
- Skill loading rules
- Communication surfaces
- Changelog

**Out of scope**
- Vendor-specific system prompt syntax
- Tool API definitions
- Runtime sandboxing

---

## 4. Design / Approach
A boot file should answer:

```text
Who am I?
What do I read first?
What am I allowed to do?
What must I never do?
When do I load skills?
How do I communicate?
How do I report state?
```

Recommended boot file anatomy:

```text
# [Agent Name] Boot

_version: X.Y | agent: agent-id | last-updated: YYYY-MM-DD_

## 1. Identity
## 2. Startup Sequence
## 3. Tool / Permission Policy
## 4. Hard Rules
## 5. Skill Loading
## 6. Communication Surfaces
## 7. Output Defaults
## 8. Current Phase
## Changelog
```

---

## 5. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Finalize boot file anatomy | alice | pending |
| T-002 | Create example read-only boot file | alice | pending |
| T-003 | Create example write-capable boot file | alice | pending |

---

## 6. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | Should every boot file include a current phase field? | jared | no |

---

## 7. Changelog

| Version | Date | Change |
|---------|------|--------|
| 1.0 | 2026-05-11 | Initial draft |
