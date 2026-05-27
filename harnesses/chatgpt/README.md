# ChatGPT Harnesses

Boot commands for ChatGPT (OpenAI) agent sessions.

ChatGPT’s primary role in the AFO ecosystem is **roadmapping, spec authoring, schema validation, composer output testing, and handoff coordination**. ChatGPT is the strategic planning and validation layer.

---

## Registry

| Command | File | Purpose |
|---|---|---|
| `boot-chatgpt` | `boot-chatgpt.md` | Default ChatGPT — roadmap + spec + handoff coordination |
| `boot-roadmap` | `boot-roadmap.md` | Roadmap planning mode — prioritize, sequence, estimate |
| `boot-spec` | `boot-spec.md` | Spec authoring mode — write detailed product/technical specs |
| `boot-validate` | `boot-validate.md` | Schema + output validation mode |
| `boot-handoff` | `boot-handoff.md` | Handoff coordination — read bulletins, route work to agents |

---

## How to Boot

Paste at the start of any ChatGPT project or session:

```
Run boot-roadmap
Load: nothinginfinity/versioned-agent-harness → harnesses/chatgpt/boot-roadmap.md
```
