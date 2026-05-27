# Harnesses

This folder contains versioned agent harness boot files.

Each harness defines a complete operating envelope for a specific agent role:
- Identity and purpose
- What to load on boot
- Responsibilities and boundaries
- First action
- Reference docs

## Boot Command Pattern

Harness files are designed to be used as **boot commands** — short named instructions pasted at the start of a Perplexity space, Claude project, ChatGPT project, or any agent session.

```
Run boot-mcp
Load: nothinginfinity/versioned-agent-harness → harnesses/alice/boot-mcp.md
```

Each harness file is self-contained, version-controlled, and references full doctrine docs rather than duplicating them.

## Registry

| Command | File | Agent | Purpose |
|---|---|---|---|
| `boot-alice` | `alice/boot-alice.md` | Alice (Perplexity) | Default Alice — GitHub build agent |
| `boot-mcp` | `alice/boot-mcp.md` | Alice (Perplexity) | AFO MCP builder space |
| `boot-social` | `alice/boot-social.md` | Alice (Perplexity) | Message OS Cloud Social MVP builder |
| `boot-toolsmith` | `alice/boot-toolsmith.md` | Alice (Perplexity) | Toolsmith belt manager |
| `boot-research` | `alice/boot-research.md` | Alice (Perplexity) | Research + spec drafting only |

## How to Add a New Harness

1. Create `harnesses/<agent>/<boot-name>.md`
2. Add a row to the registry table above
3. Follow the harness template in `harnesses/TEMPLATE.md`
4. Reference full docs rather than duplicating them
5. End every harness with a **first action**
