## SPEC-003 — Skill System
*version: 0.1 | status: draft | owner: alice | date: 2026-05-11*

---

## 1. Problem
Skills are often mixed into prompts as long static instructions, making them hard to reuse, audit, version, or selectively load.

---

## 2. Goal
Define a reusable, lazy-loadable skill system for agent harnesses using human-readable Markdown with machine-readable frontmatter.

---

## 3. Scope
**In scope**
- Skill file format
- YAML frontmatter contract
- Trigger model
- Output model
- Lazy-loading rules
- Skill auditing guidance

**Out of scope**
- Tool-specific adapters
- Skill execution engine internals
- Model fine-tuning

---

## 4. Design / Approach
A skill is a composable capability module that an agent loads only when relevant to a task.

### Skill format
Every skill is a Markdown file with required YAML frontmatter.

```yaml
---
id: code-review
version: 0.1
status: draft
owner: alice
triggers:
  - review code
  - inspect diff
outputs:
  - review-report
---
```

### Required frontmatter fields
- `id`
- `version`
- `status`
- `triggers`

### Recommended frontmatter fields
- `owner`
- `outputs`
- `quality_checks`

### Skill body sections
A skill body should usually contain:
1. Purpose
2. Trigger Conditions
3. Procedure
4. Output Format
5. Quality Checks
6. Changelog

### Lazy-loading rules
- Skills should not be loaded by default unless required by the harness.
- Trigger phrases are advisory hints, not the only invocation method.
- Agents may load a skill due to explicit user request, routing rules, or recognized task shape.
- Large skill libraries should remain modular to reduce context bloat.

### Auditability
Because skills are plain Markdown with frontmatter, changes are diffable, reviewable, and attributable to a human or agent owner.

---

## 5. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Standardize required frontmatter fields | alice | done |
| T-002 | Define body structure guidance | alice | done |
| T-003 | Clarify lazy-load behavior | alice | done |
| T-004 | Add skill quality rubric later | alice | pending |

---

## 6. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | Should skills support imports / composition later? | jared | no |
| Q-002 | Should trigger matching stay natural-language only? | jared | no |

---

## 7. Changelog

| Version | Date | Change |
|---------|------|--------|
| 0.1 | 2026-05-11 | Initial draft |
