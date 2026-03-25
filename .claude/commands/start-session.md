---
description: Initialize Roblox Archery Game session with project context and authority hierarchy
---

# Roblox Archery Game Session Initialization

Before any work begins, establish project context by following this procedure.

## Step 1: Verify Working Directory (HARD FAIL)

Check the current working directory using `pwd`.

**REQUIRED:** Working directory MUST be `/home/jevenson/dev/_pet_projects/roblox` or a subdirectory.

If NOT in roblox project directory:
```
══════════════════════════════════════════════════════════════
 SESSION INITIALIZATION FAILED
══════════════════════════════════════════════════════════════
 Current directory is not within /home/jevenson/dev/_pet_projects/roblox

 To fix:
   cd /home/jevenson/dev/_pet_projects/roblox

 Then re-run /start-session
══════════════════════════════════════════════════════════════
```

**STOP. Do not continue until user changes directory.**

## Step 2: Load Authority Documents

Read the following files in order and provide a brief summary of each:

### 2a. BOOT.md
Read: `/home/jevenson/dev/_pet_projects/roblox/_ops/BOOT.md`

Summarize: Document authority hierarchy (which files take precedence)

### 2b. PROJECT_OPERATING_MODEL.md
Read: `/home/jevenson/dev/_pet_projects/roblox/_ops/PROJECT_OPERATING_MODEL.md`

Summarize: What this project is, what actions are allowed, system of record

### 2c. CLAUDE.md
Read: `/home/jevenson/dev/_pet_projects/roblox/CLAUDE.md`

Summarize: Tech stack, Luau conventions, MCP workflow, security model

## Step 3: Check Progress State

Look for progress/state files:

1. `/home/jevenson/dev/_pet_projects/roblox/_ops/PROGRESS.md` (completed work)
2. `/home/jevenson/dev/_pet_projects/roblox/_ops/NEXT_STEPS.md` (priorities)

**If PROGRESS.md exists:** Read and summarize last completed work.
**If NEXT_STEPS.md exists:** Read and show immediate priorities.

## Step 4: Check Roblox Studio Connection

Use MCP tool to verify Studio connection:
```
get_place_info
```

Report:
- Connection status (SUCCESS / FAILED)
- Place name (if connected)
- Place ID (if connected)

## Step 5: Print Session Ready Block

After completing all reads, output a structured summary:

```
═══════════════════════════════════════════════════════════════════════════════
 ROBLOX ARCHERY GAME SESSION READY
═══════════════════════════════════════════════════════════════════════════════
 Project:      Archery Legends
 Type:         Monetized Roblox Game
 Phase:        MVP
 CWD:          [current working directory]

 System of Record:  Roblox Studio (via MCP)
═══════════════════════════════════════════════════════════════════════════════
 STUDIO CONNECTION:
   Status:       [SUCCESS / FAILED / NOT CHECKED]
   Place Name:   [name or "N/A"]
   Place ID:     [id or "N/A"]
═══════════════════════════════════════════════════════════════════════════════
 PROGRESS STATE:
   Last Work:    [From PROGRESS.md or "No progress file found"]
   Next Steps:   [From NEXT_STEPS.md or "No next steps file found"]
═══════════════════════════════════════════════════════════════════════════════
 CURRENT ALLOWED LAYERS:

   ✅ SAFE:        Config tuning, UI polish, playtest
   ⚠️  CONTROLLED:  Core mechanics, DataStore logic
   🛑 HIGH RISK:   Security changes, production data
═══════════════════════════════════════════════════════════════════════════════
 ACTIVE CONSTRAINTS:

   • All code lives in Roblox Studio (not local files)
   • MCP tools for all Studio interactions
   • Server-authoritative security model
   • Work order: Core → Security → Persistence → Progression → UI
   • Always verify via playtest before marking complete
═══════════════════════════════════════════════════════════════════════════════
```

## Restrictions

This command:
- Does NOT create or modify game code
- Does NOT run playtests
- Only reads local documentation files
- Optionally checks Studio connection

## Post-Initialization

After this command completes, Claude Code may begin work.

If Studio connection FAILED, recommend checking:
1. Roblox Studio is running
2. robloxstudio-mcp plugin is installed and active
3. MCP server is connected
