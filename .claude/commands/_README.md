# Roblox Archery Game Commands

## Required: Start Every Session Here

```
/start-session
```

This command establishes project context and must be run before any work begins.

---

## Available Commands

| Command | Description |
|---------|-------------|
| `/start-session` | Initialize session with project context and authority hierarchy |
| `/wrap-up` | End-of-session wrap-up - summarizes work, updates PROGRESS.md and NEXT_STEPS.md |

---

## Why This Matters

The Roblox Archery Game project has:
- A strict document authority hierarchy
- MCP-driven development workflow
- Server-authoritative security model
- Phased work order (Core → Security → Persistence → Progression → UI)

Running `/start-session` ensures Claude Code:
1. Understands what this project is
2. Knows the system of record (Roblox Studio via MCP)
3. Identifies current progress and next steps
4. Verifies Studio connection status

---

## Adding New Commands

Place new command files in this directory with `.md` extension.

Use YAML frontmatter for metadata:
```yaml
---
description: Brief description of what the command does
---
```

---

*Do not begin Roblox game development work without running `/start-session` first.*
