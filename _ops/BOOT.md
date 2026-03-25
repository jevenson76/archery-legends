# Roblox Archery Game - Boot File

**Purpose:** Establishes the single authoritative entrypoint and document precedence for the Roblox Archery Game project.

---

## Document Authority Hierarchy

This project uses a strict authority hierarchy. Claude Code MUST treat documents in the following order of authority:

### 1. PROJECT_OPERATING_MODEL.md
Defines what this project is and what actions are allowed.

### 2. CLAUDE.md (Project Root)
Defines technical stack, conventions, verification methods.

### 3. GAME_DESIGN_DOCUMENT.md (docs/)
Defines game mechanics, monetization, engagement systems.

### 4. PROGRESS.md
Tracks completed work and current state.

### 5. NEXT_STEPS.md
Defines immediate priorities and blockers.

### 6. RUNBOOKS/
Defines execution procedures for common operations.

---

## Classification of Other Documents

- **docs/engagement-psychology.md**: Reference material for retention mechanics
- **docs/mvp-task-list.md**: Historical task planning (superseded by NEXT_STEPS.md)
- **builds/**: Build library exports (generated, not design authority)

---

## Session Protocol

At the start of every session, Claude Code must:

1. Read `_ops/BOOT.md` first
2. Follow the document hierarchy defined above
3. Defer to higher-authority documents when conflicts arise
4. Check PROGRESS.md and NEXT_STEPS.md for current state

---

*This file is the authoritative entrypoint for the Roblox Archery Game project.*
