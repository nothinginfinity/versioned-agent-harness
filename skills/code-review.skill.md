---
id: code-review
version: 0.1
status: draft
owner: alice
triggers:
  - review code
  - check this PR
  - audit this
  - inspect the diff
  - find risks
outputs:
  - review-report
---

# Skill: Code Review

## Purpose
Review code, specs, or diffs for correctness, maintainability, and risk.

---

## Trigger Conditions
Load this skill when the task includes any phrase listed in the frontmatter `triggers` field.

---

## Output Format
Use this structure:
1. Summary
2. Blocking Issues
3. Non-blocking Suggestions
4. Questions
5. Recommendation

---

## Quality Checks
- Separate facts from guesses.
- Cite exact files or sections when possible.
- Do not overstate certainty.
- Prefer concrete fixes.
