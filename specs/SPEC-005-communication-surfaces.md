## SPEC-005 — Communication Surfaces
*version: 0.1 | status: draft | owner: alice | date: 2026-05-11*

---

## 1. Problem
Agent systems become opaque when communication is hidden inside chat logs or informal notes. Without clear surfaces, humans cannot audit who asked what, what changed, or which messages require action.

---

## 2. Goal
Define explicit communication surfaces for harnesses, separating directed messages from shared bulletins and making agent collaboration reviewable.

---

## 3. Scope
**In scope**
- Inbox, outbox, mail, and bulletin surfaces
- Directed vs broadcast communication
- Human-to-agent and agent-to-agent routing
- Basic communication patterns
- Message vs bulletin separation

**Out of scope**
- Realtime chat systems
- Notification delivery infrastructure
- External ticketing integrations

---

## 4. Design / Approach
Communication surfaces are durable files that allow tasks, updates, and coordination to be inspected outside ephemeral chats.

### Surface types
- **Inbox** — directed work queue for an agent
- **Outbox** — outgoing requests to another party or system
- **Mail** — agent-to-agent or human-to-agent directed communication
- **Bulletin** — shared delta feed for observers and team visibility

### Message vs bulletin
Keep `message` and `bulletin` schemas separate.

| Type | Purpose | Directed? |
|------|---------|-----------|
| message | Ask, reply, delegate, escalate | Yes |
| bulletin | Announce change, note blocker, surface decision | No |

### Routing guidance
- Human-assigned tasks usually enter an inbox.
- Agent replies may use mail.
- Important changes should be surfaced to the bulletin.
- Broadcast decision logs should not be hidden in direct messages.

### Desired properties
Communication surfaces should be:
- Human-readable
- Timestamped where useful
- Easy to grep
- Linkable by file path or entry ID
- Durable enough for audit

---

## 5. Tasks

| ID | Task | Owner | Status |
|----|------|-------|--------|
| T-001 | Define surface taxonomy | alice | done |
| T-002 | Clarify directed vs broadcast semantics | alice | done |
| T-003 | Document routing rules | alice | done |
| T-004 | Add message / bulletin examples later | alice | pending |

---

## 6. Open Questions

| # | Question | Owner | Resolved |
|---|----------|-------|----------|
| Q-001 | Should inbox items have priority levels standardized later? | jared | no |
| Q-002 | Should bulletins support categories/tags in v2? | jared | no |

---

## 7. Changelog

| Version | Date | Change |
|---------|------|--------|
| 0.1 | 2026-05-11 | Initial draft |
