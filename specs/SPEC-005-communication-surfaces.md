## SPEC-005 — Communication Surfaces
*version: 1.0 | status: draft | owner: alice | date: 2026-05-11*

---

## 1. Problem
Agents and humans need structured places to exchange messages without mixing instructions, specs, and state.

---

## 2. Goal
Define standard communication surfaces for LLM harnesses.

---

## 3. Scope
**In scope**
- Inbox
- Outbox
- Internal mail
- Bulletin
- Message status
- Priority
- References

**Out of scope**
- Email server implementation
- Chat UI implementation
- Real-time messaging protocol

---

## 4. Design / Approach
Recommended surfaces:

| Surface | Purpose |
|---------|---------|
| inbox.md | Human or upstream agent tasks |
| outbox.md | Agent messages to external agents |
| mail.md | Internal agent-to-agent messages |
| bulletin.md | Read-only delta feed for observers |

Bulletin entries should use full repo paths in `ref:`.

Example:

```text
id: BLT-001
from: alice
date: 2026-05-11
status: unread
priority: normal
ref: spaces/gists/G-000-alice-boot.md | spaces/specs/SPEC-002-title.md
subject: short title
body: >
  Why this matters. Keep under 10 lines.
```

---

## 5. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Define message schema | alice | pending |
| T-002 | Define bulletin schema | alice | pending |
| T-003 | Define acknowledgement flow | alice | pending |

---

## 6. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | Should bulletin and message schemas be separate? | jared | no |

---

## 7. Changelog

| Version | Date | Change |
|---------|------|--------|
| 1.0 | 2026-05-11 | Initial draft |
