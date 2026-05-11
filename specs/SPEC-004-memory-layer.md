## SPEC-004 — Memory Layer
*version: 1.0 | status: draft | owner: alice | date: 2026-05-11*

---

## 1. Problem
LLM sessions need durable project state without relying only on chat history.

---

## 2. Goal
Define a minimal memory layer for versioned LLM harnesses.

---

## 3. Scope
**In scope**
- Live memory file
- Note entries
- Decisions
- Open questions
- Current phase
- References to specs and artifacts

**Out of scope**
- Vector memory implementation
- Private user data storage policy
- Long-term database design

---

## 4. Design / Approach
The default memory file is JSON.

Recommended fields:

```json
{
  "schema_version": "1.0",
  "generated_at": "2026-05-11T00:00:00Z",
  "project": "example",
  "current_phase": "Phase 0",
  "last_spec_number": "SPEC-001",
  "decisions": [],
  "open_questions": [],
  "notes": []
}
```

Memory should be concise and durable. It should not replace specs, inboxes, or full logs.

---

## 5. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Define memory schema | alice | pending |
| T-002 | Define update rules | alice | pending |
| T-003 | Define when memory should be summarized | alice | pending |

---

## 6. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | Should memory be append-only or periodically compacted? | jared | no |

---

## 7. Changelog

| Version | Date | Change |
|---------|------|--------|
| 1.0 | 2026-05-11 | Initial draft |
