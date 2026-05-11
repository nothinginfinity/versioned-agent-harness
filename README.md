# Versioned Agent Harness

**Versioned Agent Harness is a repo-native framework for defining, coordinating, and auditing LLM agents through version-controlled boot files, skills, memory, schemas, communication surfaces, permissions, and workflows.**

---

## What is this?

This is a spec-first repo for creating reusable operating harnesses for large language model agents.

A prompt tells an LLM what to do.

A harness defines the environment around the LLM:

```text
Agent boots
→ reads versioned instructions
→ loads memory
→ checks inbox / bulletin surfaces
→ lazy-loads skills when needed
→ performs role-specific work
→ writes or reports according to permissions
→ leaves an auditable trail
```

The goal is to make LLM behavior:
- portable
- inspectable
- reproducible
- role-specific
- project-specific
- auditable through Git

---

## Why it matters

Most LLM workflows fail because context, instructions, permissions, and responsibilities are scattered across chats.
Versioned Agent Harness turns LLM coordination into a repo-native system.
Instead of giving every model the same giant prompt, each agent receives a harness that defines:
- identity
- responsibilities
- boot sequence
- read/write boundaries
- skill triggers
- memory files
- communication surfaces
- output rules
- audit requirements

---

## Core Concepts

| Concept | Meaning |
|---------|---------|
| Harness | The full operating envelope around an LLM agent |
| Boot file | The agent’s startup instructions and role definition |
| Skill | A lazy-loaded instruction module for a specific task |
| Memory | Durable compressed project state |
| Bulletin | Read-only delta feed for observers or brainstorm agents |
| Inbox / Outbox | Structured communication surfaces between humans and agents |
| Schema | Machine-readable contract for harness data |
| Audit trail | Git history, changelogs, turn logs, and status markers |

---

## Example Harness Types

| Harness | Purpose |
|---------|---------|
| Brainstorm Read-Only | Observe, critique, plan, and propose without writing |
| Builder Agent | Execute scoped implementation tasks |
| Reviewer Agent | Audit code, specs, and architecture |
| Ops Agent | Perform maintenance, routing, cleanup, and workflow tasks |
| Data Agent | Process feeds, documents, or knowledge stores |

---

## Repo Structure

```text
versioned-agent-harness/
├── specs/       # architecture specs
├── harnesses/   # example agent harness files
├── skills/      # reusable skill modules
├── schemas/     # JSON schemas for harness objects
├── examples/    # reference patterns
├── docs/        # explanation, use cases, product framing
└── roadmap.md
```

---

## Status

Phase 0 — scaffold.
See [roadmap.md](./roadmap.md).
