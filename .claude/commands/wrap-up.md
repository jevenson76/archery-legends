---
description: End-of-session wrap-up - summarizes work, updates PROGRESS.md and NEXT_STEPS.md
---

# Roblox Archery Game Session Wrap-Up

Run this command at the end of a development session to capture progress and set up the next session.

## Step 1: Summarize Session Work

Review the conversation history and identify:
1. What was implemented or fixed
2. What playtests were run and results
3. Any blockers encountered
4. Decisions made

## Step 2: Update PROGRESS.md

Append a new entry to `/home/jevenson/dev/_pet_projects/roblox/_ops/PROGRESS.md`:

```markdown
### [DATE]: [Brief Title]

**Status:** [COMPLETE / IN PROGRESS / BLOCKED]

[Summary of work done]

| Component | Change |
|-----------|--------|
| [Script/System] | [What changed] |

**Playtest:** [Zero errors / X errors / Not tested]
```

## Step 3: Update NEXT_STEPS.md

Update `/home/jevenson/dev/_pet_projects/roblox/_ops/NEXT_STEPS.md`:

1. Mark completed items with ✓
2. Add any new tasks discovered
3. Update "Immediate Priority" section if needed
4. Note any blockers in "Blockers" section

## Step 4: Update STATUS.md

Update `/home/jevenson/dev/_pet_projects/roblox/STATUS.md`:

1. Update "Last Updated" date
2. Update component status table
3. Update "Next Immediate Tasks" if changed

## Step 5: Git Commit (Optional)

If significant changes were made:

```bash
cd /home/jevenson/dev/_pet_projects/roblox && git add -A && git status
```

Suggest a conventional commit message based on work done.

## Step 6: Print Session Summary

Output a structured summary:

```
═══════════════════════════════════════════════════════════════════════════════
 SESSION WRAP-UP COMPLETE
═══════════════════════════════════════════════════════════════════════════════
 Date:         [DATE]
 Duration:     [Approximate session time]

 COMPLETED:
   • [Item 1]
   • [Item 2]

 IN PROGRESS:
   • [Item if any]

 NEXT SESSION:
   • [Priority 1]
   • [Priority 2]

 BLOCKERS:
   • [None / List blockers]

 FILES UPDATED:
   • _ops/PROGRESS.md
   • _ops/NEXT_STEPS.md
   • STATUS.md
═══════════════════════════════════════════════════════════════════════════════
```

## Notes

- Always run playtest before wrap-up to ensure code is stable
- Don't leave sessions with broken code
- Update MANUAL_STEPS.md if new manual tasks were discovered
