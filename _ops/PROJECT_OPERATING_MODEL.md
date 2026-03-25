# Roblox Archery Game - Project Operating Model

**Document Created:** 2026-03-25
**Status:** AUTHORITATIVE
**Project Root:** `/home/jevenson/dev/_pet_projects/roblox`

---

## System Identity

**This is a monetized Roblox game development project, not a web application.**

---

## Architecture Layers

| Layer | Technology | Role |
|-------|------------|------|
| **Game Logic** | Luau (Server Scripts) | Core mechanics, security, persistence |
| **Client Experience** | Luau (Client Scripts) | Input, camera, UI |
| **Shared Systems** | Luau (ModuleScripts) | Config, physics, types |
| **Persistence** | Roblox DataStore | Player progress, currency, inventory |
| **Monetization** | MarketplaceService | Game passes, developer products |
| **Build Integration** | robloxstudio-mcp | Direct Studio manipulation via MCP |

---

## Code Sovereignty

**Roblox Studio is the system of record for game state.**

Local files in this repo are:
- Design documents (docs/)
- Build library exports (builds/)
- Operational tracking (_ops/)

All game code MUST live in Roblox Studio hierarchy:
- `ServerScriptService/` - Server scripts
- `ReplicatedStorage/` - Shared modules, remotes, assets
- `StarterPlayerScripts/` - Client scripts
- `StarterGui/` - UI

---

## Development Workflow

**All code changes flow through MCP to Roblox Studio.**

```
1. Design/plan change
       ↓
2. Use MCP tools to read current state (get_script_source, get_file_tree)
       ↓
3. Write/edit code via MCP (set_script_source, edit_script_lines)
       ↓
4. Verify with MCP (get_script_source to confirm)
       ↓
5. Test with MCP (start_playtest → get_playtest_output → stop_playtest)
       ↓
6. Fix errors and re-test until clean
       ↓
7. Update PROGRESS.md
```

---

## Claude Code Operating Role

**Claude Code is acting as a game developer and systems architect, not a web developer.**

---

## Mandatory Work Order

Claude Code must always work in this order:

```
1. Core mechanics (shooting, scoring)
       ↓
2. Server security (validation, anti-cheat)
       ↓
3. Data persistence (DataStore)
       ↓
4. Progression systems (XP, levels)
       ↓
5. Monetization hooks
       ↓
6. UI polish (LAST)
```

---

## Change Request Validation

**If a requested change attempts to modify UI before core mechanics are stable, redirect to core work first.**

### Valid Request Flow

```
User: "Add a new bow skin to the shop"
       ↓
Claude: "Is the shop system implemented?"
       ↓
Claude: "Is inventory persistence working?"
       ↓
Claude: "Is the purchase flow secure?"
       ↓
[Only then proceed to skin implementation]
```

### Invalid Request (Redirect)

```
User: "Make the UI look prettier"
       ↓
Claude: "STOP - Core mechanics first."
       ↓
Claude: "First: Is the shooting mechanic complete?"
       ↓
Claude: "First: Is scoring working?"
       ↓
[Redirect to core work]
```

---

## Project Purpose

| This Project IS | This Project IS NOT |
|-----------------|---------------------|
| Monetized Roblox game | Web application |
| MCP-driven development | Manual Studio editing |
| Solo developer build | Team project |
| MVP-focused | Feature-complete |
| Engagement-optimized | Casual prototype |

---

## Reference Documents

All changes must comply with:

| Document | Purpose | Authority |
|----------|---------|-----------|
| `CLAUDE.md` | Tech stack, conventions, verification | Defines HOW to build |
| `docs/game-design-document.md` | Game mechanics, monetization | Defines WHAT to build |
| `docs/engagement-psychology.md` | Retention mechanics | Defines WHY we build it |
| `_ops/PROGRESS.md` | Completed work | Defines WHERE we are |
| `_ops/NEXT_STEPS.md` | Priorities | Defines WHERE we go next |

---

## Enforcement

Before ANY code generation:

- [ ] Check NEXT_STEPS.md for current priority
- [ ] Verify core mechanics are stable before UI work
- [ ] Use MCP tools (not manual editing)
- [ ] Test via playtest before marking complete
- [ ] Update PROGRESS.md after changes

**Violations of this operating model will result in rework.**

---

## Document History

| Date | Author | Change |
|------|--------|--------|
| 2026-03-25 | Claude Code | Initial creation (mirrored from ATL structure) |
