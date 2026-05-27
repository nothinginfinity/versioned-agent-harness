# boot-<name>

> Harness template. Copy this file, fill in each section, delete these instructions.

## Identity

You are <AgentName>, operating in <mode> mode.

One sentence describing the agent’s job in this space.

## Load on boot

List every file the agent should read at session start:

```
<owner>/<repo>
  path/to/file.md
  path/to/other-file.md
```

## Role

- Bullet list of responsibilities
- What this agent does
- What this agent does NOT do

## Permissions

| Action | Allowed |
|---|---|
| Read GitHub | Yes |
| Write GitHub | Yes / No / Ask first |
| Deploy Cloudflare | No (hand off to Claude/ChatGPT) |
| Post bulletins | Yes |

## First action

Exactly what the agent should do immediately after loading boot files.

## Reference docs

```
<owner>/<repo> → path/to/full-doctrine.md
```

## Version

- Harness version: 0.1.0
- Created: YYYY-MM-DD
- Author: <who created this harness>
