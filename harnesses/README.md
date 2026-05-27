# Harnesses

This folder contains versioned agent harness boot files — **slash commands for agent development**.

Each harness defines a complete operating envelope for a specific agent in a specific mode:
- Identity and purpose
- What to load on boot
- Responsibilities and hard boundaries
- Permissions table
- First action
- Reference docs

---

## The Concept

Think of boot commands like slash commands in an IDE:

```
/deploy   → boot-deploy  (Claude)
/build    → boot-mcp     (Alice)
/plan     → boot-roadmap (ChatGPT)
/debug    → boot-debug   (Claude)
/research → boot-research (Alice)
/handoff  → boot-handoff (ChatGPT)
```

Each command activates a focused agent mode with the right instructions loaded, the right permissions set, and the right first action queued.

---

## How to Boot

Paste at the start of any agent session (Perplexity, Claude, ChatGPT):

```
Run boot-deploy
Load: nothinginfinity/versioned-agent-harness → harnesses/claude/boot-deploy.md
```

---

## Full Registry

### Alice (Perplexity) — GitHub build agent

| Command | File | Purpose |
|---|---|---|
| `boot-alice` | `alice/boot-alice.md` | Default — reads bulletin + inbox, general build work |
| `boot-mcp` | `alice/boot-mcp.md` | AFO MCP builder — design + commit Worker MCPs |
| `boot-social` | `alice/boot-social.md` | Message OS Cloud Social MVP v0.3 builder |
| `boot-toolsmith` | `alice/boot-toolsmith.md` | Toolsmith belt manager + tool inventory |
| `boot-research` | `alice/boot-research.md` | Research + spec drafting, read-mostly mode |

### Claude (Anthropic) — Cloudflare deploy + ops agent

| Command | File | Purpose |
|---|---|---|
| `boot-claude` | `claude/boot-claude.md` | Default — reads handoffs, deploys pending Workers |
| `boot-deploy` | `claude/boot-deploy.md` | Focused deploy — one Worker from Alice handoff to live |
| `boot-d1` | `claude/boot-d1.md` | D1 database ops — create, migrate, query |
| `boot-debug` | `claude/boot-debug.md` | MCP runtime debugging — diagnose + patch live Workers |
| `boot-ops` | `claude/boot-ops.md` | General CF ops — KV, R2, routes, cron, secrets |

### ChatGPT (OpenAI) — roadmap + spec + coordination agent

| Command | File | Purpose |
|---|---|---|
| `boot-chatgpt` | `chatgpt/boot-chatgpt.md` | Default — reads bulletins, proposes next priorities |
| `boot-roadmap` | `chatgpt/boot-roadmap.md` | Roadmap planning — prioritize, sequence, estimate |
| `boot-spec` | `chatgpt/boot-spec.md` | Spec authoring — full implementation-ready specs |
| `boot-validate` | `chatgpt/boot-validate.md` | Schema + output validation |
| `boot-handoff` | `chatgpt/boot-handoff.md` | Handoff coordination — route work to Alice/Claude/Jared |

---

## Agent Roles at a Glance

```
Alice (Perplexity)
  → GitHub reads/writes
  → Spec + source authoring
  → Docs, schemas, changelogs
  → Commits + handoff to Claude

Claude (Anthropic)
  → Cloudflare Worker deploy
  → D1 / KV / R2 / secrets
  → Runtime debugging
  → Smoke tests post-deploy

ChatGPT (OpenAI)
  → Roadmaps + prioritization
  → Detailed spec authoring
  → Schema + output validation
  → Handoff routing + coordination

Jared
  → Decisions + approvals
  → Adding secrets/API keys
  → Custom domain confirmation
  → Final smoke test sign-off
```

---

## How to Add a New Harness

1. Copy `TEMPLATE.md`
2. Fill in all sections
3. Save as `harnesses/<agent>/boot-<name>.md`
4. Add a row to the registry table above
5. Commit — the new command is immediately available
