# Boot Command System

The boot command system is the primary way to activate a specific agent harness at the start of a Perplexity space, Claude project, ChatGPT project, or any LLM session.

---

## Concept

Instead of pasting a giant custom prompt into every new space, you paste one short boot command. The agent reads the named harness file from GitHub and loads its full operating envelope from there.

This means:
- Instructions are **version-controlled** — update the harness file once, all future sessions get the new version
- Each space is **role-specific** — MCP builder, social MVP builder, researcher, etc.
- Context is **composable** — a harness references other docs rather than duplicating them
- The system is **auditable** — Git history shows when instructions changed and why

---

## How to Boot a Space

Paste this at the start of any new Perplexity space (or agent session):

```
Run boot-mcp
Load: nothinginfinity/versioned-agent-harness → harnesses/alice/boot-mcp.md
```

Or for the default Alice build space:

```
Run boot-alice
Load: nothinginfinity/versioned-agent-harness → harnesses/alice/boot-alice.md
```

---

## Available Boot Commands

| Command | File | Purpose |
|---|---|---|
| `boot-alice` | `harnesses/alice/boot-alice.md` | Default Alice — reads bulletin + inbox, general build work |
| `boot-mcp` | `harnesses/alice/boot-mcp.md` | AFO MCP builder — design + commit Worker MCPs |
| `boot-social` | `harnesses/alice/boot-social.md` | Message OS Cloud Social MVP v0.3 builder |
| `boot-toolsmith` | `harnesses/alice/boot-toolsmith.md` | Toolsmith belt manager + tool inventory |
| `boot-research` | `harnesses/alice/boot-research.md` | Research + spec drafting, read-mostly mode |

---

## Harness File Structure

Every harness file contains:

```
# boot-<name>

## Identity       — who the agent is in this space
## Load on boot   — what GitHub files to read first
## Role           — responsibilities + what NOT to do
## Permissions    — read/write/deploy boundaries
## First action   — exactly what to do after loading
## Reference docs — full doctrine files
## Version        — semver + author + date
```

---

## Adding a New Boot Command

1. Copy `harnesses/TEMPLATE.md`
2. Fill in all sections
3. Save as `harnesses/<agent>/boot-<name>.md`
4. Add a row to `harnesses/README.md` registry
5. Add a row to `docs/boot-command-system.md` table above
6. Commit — the new command is immediately available to all spaces

---

## Source of Truth

Boot commands in this repo are the **canonical source**. The mirror in `nothinginfinity/agent-bridge/shared/boot/` is a convenience copy for Alice’s primary working repo.

When updating harnesses, update both:
- `nothinginfinity/versioned-agent-harness/harnesses/alice/`
- `nothinginfinity/agent-bridge/shared/boot/`

---

## Future Harness Types

```
harnesses/claude/     — Claude-specific harnesses (deploy, D1, CF ops)
harnesses/chatgpt/    — ChatGPT-specific harnesses (roadmap, specs, schema)
harnesses/shared/     — Agent-agnostic harnesses (any model can use)
```

As the system grows, each agent gets its own folder with role-specific boot commands.
