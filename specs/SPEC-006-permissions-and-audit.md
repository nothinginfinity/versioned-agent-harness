## SPEC-006 — Permissions and Audit
*version: 1.0 | status: draft | owner: alice | date: 2026-05-11*

---

## 1. Problem
LLM agents need explicit permission boundaries and auditable behavior, especially when multiple humans and agents are involved.

---

## 2. Goal
Define read/write modes, audit rules, and traceability expectations for harnessed agents.

---

## 3. Scope
**In scope**
- Read-only mode
- Write-capable mode
- Commit discipline
- Changelogs
- Turn logs
- Acknowledgement flows

**Out of scope**
- Full sandbox implementation
- Security certification
- Identity provider integration

---

## 4. Design / Approach
Permission modes:

| Mode | Meaning |
|------|---------|
| read-only | Can inspect and reason, cannot modify |
| draft-only | Can produce copy-paste drafts, cannot write |
| write-capable | Can modify repo files within rules |
| admin | Can modify harness definitions and permissions |

Audit expectations:
- Every harness file includes version and changelog.
- Every spec includes status and changelog.
- Every write-capable turn should produce a clear commit.
- Important state changes should update memory or bulletin surfaces.
- Read-only agents should verbally acknowledge reviewed bulletin entries.

---

## 5. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Define permission mode schema | alice | pending |
| T-002 | Define audit checklist | alice | pending |
| T-003 | Define write-capable turn rules | alice | pending |

---

## 6. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | Should admin harnesses be separated into a different repo? | jared | no |

---

## 7. Changelog

| Version | Date | Change |
|---------|------|--------|
| 1.0 | 2026-05-11 | Initial draft |
