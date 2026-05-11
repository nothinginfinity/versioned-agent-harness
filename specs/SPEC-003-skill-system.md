## SPEC-003 — Skill System
*version: 1.0 | status: draft | owner: alice | date: 2026-05-11*

---

## 1. Problem
Large boot prompts become bloated when every possible behavior is loaded at startup.

---

## 2. Goal
Define a lazy-loaded skill system for LLM harnesses.

---

## 3. Scope
**In scope**
- Skill file anatomy
- Skill triggers
- Skill metadata
- Skill output defaults
- Skill unloading guidance

**Out of scope**
- Automatic runtime loading implementation
- Model-specific tool calling

---

## 4. Design / Approach
A skill is a focused instruction module loaded only when relevant.

Example triggers:

| Task Type | Skill |
|-----------|-------|
| Write a spec | spec-writing.skill.md |
| Review code | code-review.skill.md |
| Route a task | routing.skill.md |

Skill anatomy:

```text
# Skill: [Name]

_version: X.Y | status: draft | owner: agent-id_

## Purpose
## Trigger Conditions
## Inputs
## Procedure
## Output Format
## Quality Checks
## Changelog
```

---

## 5. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Define skill metadata schema | alice | pending |
| T-002 | Create spec-writing skill | alice | pending |
| T-003 | Create code-review skill | alice | pending |
| T-004 | Create routing skill | alice | pending |

---

## 6. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | Should skills be composable? | jared | no |

---

## 7. Changelog

| Version | Date | Change |
|---------|------|--------|
| 1.0 | 2026-05-11 | Initial draft |
