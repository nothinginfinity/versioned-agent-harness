# boot-list

> Run this at the start of any agent session to see all available boot commands.

## What to say

```
Run boot-list
Load: nothinginfinity/versioned-agent-harness → harnesses/boot-list.md
```

Or just say: **"boot list"** and Alice/Claude/ChatGPT will load this file and print the full registry below.

---

## All Boot Commands

### 💚 Alice — Perplexity (GitHub build agent)

| Command | What it does |
|---|---|
| `boot-alice` | Default Alice — reads bulletin + inbox, general build work |
| `boot-mcp` | AFO MCP builder — design + commit AFO-style Cloudflare Worker MCPs |
| `boot-social` | Message OS Cloud Social MVP v0.3 builder |
| `boot-toolsmith` | Toolsmith belt manager + tool inventory |
| `boot-research` | Research + spec drafting, read-only mode |

### 🟦 Claude — Anthropic (Cloudflare deploy + ops agent)

| Command | What it does |
|---|---|
| `boot-claude` | Default Claude — reads handoffs, deploys pending Workers |
| `boot-deploy` | Focused deploy — one Worker from Alice handoff → live on Cloudflare |
| `boot-d1` | D1 database ops — create, migrate, query |
| `boot-debug` | MCP runtime debugging — diagnose + patch broken live Workers |
| `boot-ops` | General CF ops — KV, R2, cron, routes, secrets |

### 🟧 ChatGPT — OpenAI (roadmap + spec + coordination agent)

| Command | What it does |
|---|---|
| `boot-chatgpt` | Default ChatGPT — reads bulletins, proposes next 3 priorities |
| `boot-roadmap` | Roadmap planning — Done / In Progress / Next / Backlog / Blockers |
| `boot-spec` | Spec authoring — full implementation-ready spec for any MCP or product |
| `boot-validate` | Schema + output validation — verify tool shapes, SQL, JSON contracts |
| `boot-handoff` | Handoff coordination — route work to Alice / Claude / Jared |

### 🟥 Shared (any agent)

| Command | What it does |
|---|---|
| `boot-list` | ⭐ This file — print all available boot commands |

---

## How to use a boot command

Paste this at the start of any session:

```
Run boot-deploy
Load: nothinginfinity/versioned-agent-harness → harnesses/claude/boot-deploy.md
```

Swap `claude/boot-deploy.md` for any path in the registry above.

### Quick path reference

```
harnesses/alice/boot-alice.md
harnesses/alice/boot-mcp.md
harnesses/alice/boot-social.md
harnesses/alice/boot-toolsmith.md
harnesses/alice/boot-research.md

harnesses/claude/boot-claude.md
harnesses/claude/boot-deploy.md
harnesses/claude/boot-d1.md
harnesses/claude/boot-debug.md
harnesses/claude/boot-ops.md

harnesses/chatgpt/boot-chatgpt.md
harnesses/chatgpt/boot-roadmap.md
harnesses/chatgpt/boot-spec.md
harnesses/chatgpt/boot-validate.md
harnesses/chatgpt/boot-handoff.md

harnesses/boot-list.md
```

---

## Version

- Last updated: 2026-05-27
- Maintained by: Alice
- Source: `nothinginfinity/versioned-agent-harness`

> When new boot commands are added, Alice updates this file. Always load `boot-list` to get the current list.
