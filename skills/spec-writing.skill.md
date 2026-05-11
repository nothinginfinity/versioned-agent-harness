---
id: spec-writing
version: 0.1
status: draft
owner: alice
triggers:
  - write a spec
  - draft a SPEC
  - define requirements
  - turn this into an implementation plan
  - create a project spec
outputs:
  - spec
---

# Skill: Spec Writing

## Purpose
Turn ideas into structured, actionable specifications.

---

## Trigger Conditions
Load this skill when the task includes any phrase listed in the frontmatter `triggers` field.

---

## Output Format
Every spec should include:
1. Problem
2. Goal
3. Scope (in-scope and out-of-scope)
4. Design / Approach
5. Tasks (atomic, with owner and status)
6. Open Questions
7. Changelog

---

## Quality Checks
- Problem comes before solution.
- Scope includes both in-scope and out-of-scope sections.
- Tasks are atomic and assignable.
- Open questions are explicit and attributed.
- Changelog is updated on every revision.
