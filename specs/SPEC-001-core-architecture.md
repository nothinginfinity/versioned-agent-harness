## SPEC-001 — Core Architecture
*version: 1.0 | status: draft | owner: alice | date: 2026-05-11*

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
- Skill modules
- Memory files
- Inbox, outbox, and bulletin surfaces
- Permission boundaries
- Schema definitions
- Git-based audit trail

**Out of scope**
- A specific app implementation
- Vendor-specific LLM APIs
- Model training or fine-tuning
- Full security sandboxing

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

The harness should be stored as version-controlled files in a repository. Changes to agent behavior should be reviewable through diffs and changelogs.

---

## 5. Core Principles
1. **Harness over prompt.** The system prompt is only one part of the operating environment.
2. **Role-specific agents.** Each agent should have a clear identity and responsibility boundary.
3. **Lazy-loaded skills.** Skills load only when relevant.
4. **Read/write separation.** Observer agents should be able to inspect without mutating work.
5. **Versioned behavior.** Instruction changes are committed, reviewed, and traceable.
6. **Human-readable first.** Markdown is the default control surface.
7. **Schema-backed where useful.** JSON schemas define machine-readable contracts.

---

## 6. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Define boot file anatomy | alice | pending |
| T-002 | Define skill module anatomy | alice | pending |
| T-003 | Define memory layer contract | alice | pending |
| T-004 | Define communication surfaces | alice | pending |
| T-005 | Define audit and permission model | alice | pending |

---

## 7. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | Should harnesses support nested child harnesses? | jared | no |
| Q-002 | Should skills be plain markdown only or include JSON metadata? | jared | no |
| Q-003 | What is the minimum viable harness for a small business user? | jared | no |

---

## 8. Changelog

| Version | Date | Change |
|---------|------|--------|
| 1.0 | 2026-05-11 | Initial draft |
