## SPEC-006 — Permissions and Audit
*version: 0.1 | status: draft | owner: alice | date: 2026-05-11*

---

## 1. Problem
Without clear permission boundaries, agent systems can overreach, modify state unsafely, or leave unclear responsibility for changes. Without audit structures, teams cannot reconstruct why behavior changed.

---

## 2. Goal
Define permission modes and audit expectations for versioned agent harnesses.

---

## 3. Scope
**In scope**
- Harness modes
- Read/write separation
- Admin role boundaries
- Git-based audit trail
- Changelog expectations
- Turn-level audit guidance

**Out of scope**
- OS sandboxing
- Credential management systems
- Secret storage design
- Enterprise compliance frameworks

---

## 4. Design / Approach
A harness should make it obvious what an agent is allowed to do and how its actions can be reviewed later.

### Permission modes
Recommended harness modes:
- `read-only`
- `draft-only`
- `write-capable`
- `admin`

### Mode semantics
- **read-only** — may inspect, analyze, and propose, but never mutate files or canonical memory
- **draft-only** — may draft outputs for approval but not commit final changes
- **write-capable** — may create/update approved files within role boundaries
- **admin** — may modify harness definitions, repo structure, permissions, and control surfaces

### Audit expectations
- All significant file changes should be committed through Git.
- Harness, spec, and skill files should include changelogs.
- Shared memory updates should be attributable to the memory steward.
- Important decisions should be surfaced through a bulletin or durable note.
- Turn logs may be stored for high-audit environments.

### Human review
The harness model assumes humans remain responsible for policy and approval boundaries, especially for admin changes and architecture shifts.

---

## 5. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Define permission modes | alice | done |
| T-002 | Document mode semantics | alice | done |
| T-003 | Define audit expectations | alice | done |
| T-004 | Add turn-log example later | alice | pending |

---

## 6. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | Should admin actions require explicit dual approval later? | jared | no |
| Q-002 | Should audit severity levels be standardized? | jared | no |

---

## 7. Changelog

| Version | Date | Change |
|---------|------|--------|
| 0.1 | 2026-05-11 | Initial draft |
