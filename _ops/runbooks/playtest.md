# Runbook: Playtest Verification

## Purpose
Standard procedure for verifying code changes via Roblox Studio playtest.

## Prerequisites
- Roblox Studio open with Archery Legends place
- MCP connection active (verify with `get_place_info`)

## Procedure

### 1. Pre-Playtest Check
```
get_script_source instancePath="[script you just edited]"
```
Verify the edit applied correctly before testing.

### 2. Start Playtest
```
start_playtest mode="play"
```
- Use `mode="play"` for full client+server simulation (default)
- Use `mode="run"` for server-only testing (faster, no character)

### 3. Monitor Output
```
get_playtest_output
```
Poll every few seconds. Look for:
- `[ERROR]` — Critical, must fix
- `[WARN]` — Review, may be intentional
- `print()` — Debug output from scripts

### 4. Test Features
Manually verify:
- [ ] Player spawns correctly
- [ ] Bow aiming works
- [ ] Arrows fire and hit target
- [ ] Score updates on HUD
- [ ] Round ends after 10 arrows
- [ ] XP/currency awarded

### 5. Stop Playtest
```
stop_playtest
```
Returns final output buffer.

## Success Criteria
- Zero `[ERROR]` messages
- Feature works as intended
- No visual glitches

## Common Issues

| Error | Cause | Fix |
|-------|-------|-----|
| `attempt to index nil` | WaitForChild missing | Add `:WaitForChild()` |
| `ServerScriptService is not valid` | Client accessing server | Check script location |
| `Request was throttled` | DataStore rate limit | Add debounce |
| Script doesn't run | Disabled or wrong parent | Check Enabled property |

## Post-Playtest
1. Fix any errors
2. Re-run playtest until clean
3. Update PROGRESS.md with verification status
