# Claude Harnesses

Boot commands for Claude (Anthropic) agent sessions.

Claude’s primary role in the AFO ecosystem is **Cloudflare deployment, MCP runtime debugging, D1/KV/R2 operations, and tool orchestration**. Claude has direct access to Cf-multipart, D1 Admin, and can execute SQL, deploy Workers, and manage bindings.

---

## Registry

| Command | File | Purpose |
|---|---|---|
| `boot-claude` | `boot-claude.md` | Default Claude — deployment + CF ops agent |
| `boot-deploy` | `boot-deploy.md` | Cloudflare Worker deploy mode — deploy + bind + domain |
| `boot-d1` | `boot-d1.md` | D1 database ops — create, migrate, query |
| `boot-debug` | `boot-debug.md` | MCP runtime debugging — diagnose + patch live Workers |
| `boot-ops` | `boot-ops.md` | General CF ops — KV, R2, routes, cron, secrets |

---

## How to Boot

Paste at the start of any Claude project or session:

```
Run boot-deploy
Load: nothinginfinity/versioned-agent-harness → harnesses/claude/boot-deploy.md
```
