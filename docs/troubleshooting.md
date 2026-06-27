# Troubleshooting

Common issues and their solutions.

---

## Installation

### "Unknown command" when opening menu

**Cause**: The addon loader didn't execute.

**Solution**:
1. Verify that `lua/autorun/skillforge_loader.lua` exists
2. Check server console for Lua errors on startup
3. Ensure the addon is in the correct directory

### Trees not appearing

**Cause**: Default tree JSONs were not deployed.

**Solution**:
```
skilltree_reload_trees
```

If that doesn't work, manually check `data/skillforge/trees/` on the server — the files should be there.

### HUD not visible

**Cause**: HUD is disabled in config.

**Solution**:
```lua
SkillTree.Config.General.EnableHUD = true
```

---

## Configuration

### XP not being awarded

**Cause 1**: XP source is disabled.

**Solution**: Check your config:
```lua
SkillTree.Config.XP.Arrest.Enabled = true
```

**Cause 2**: Anti-exploit cap reached.

**Solution**: Check the player is not hitting `MaxXPPerMinute`.

**Cause 3**: Player is AFK.

**Solution**: Disable or increase AFK timeout:
```lua
SkillTree.Config.AntiExploit.AFKTimeout = 0  -- Disable AFK check
```

### Skills not unlocking

**Cause 1**: Level requirement not met.

**Solution**: Check the node's `requiredLevel` for the next rank.

**Cause 2**: Skill points insufficient.

**Solution**: Check the node's `cost` for the next rank.

**Cause 3**: Prerequisite not met.

**Solution**: Unlock the required nodes first.

**Cause 4**: Job restriction blocking.

**Solution**: Check if the job is in `JobSkills` without the skill ID.

---

## DarkRP

### Salary multiplier not working

**Cause**: The salary hook might be overridden by another addon.

**Solution**: Check hook priority or use `SkillTree_GetPlayerTree` to debug.

### Shop discount not applying

**Cause**: The hook `playerBoughtCustomEntity` may conflict with other discount addons.

**Solution**: Disable other discount addons or adjust the `ShopDiscount` effect.

### XP for job actions not working

**Cause**: The player's job might not match the `JobXP` config.

**Solution**:
1. Verify the exact job name: `SkillTree.DarkRP.GetJobName(ply)`
2. Check `SkillTree.Config.JobXP["Exact Job Name"]` exists

---

## Database

### Player data not saving

**Cause**: SQLite error or permission issue.

**Solution**:
1. Check server console for SQLite errors
2. Ensure `data/` directory is writable
3. Run `skilltree_save_all` to force a save

### "Table not found" errors

**Cause**: Database table wasn't created.

**Solution**: The tables are created automatically on first load. If they don't exist, delete `data/skillforge/` and restart.

---

## Editor

### "Invalid JSON" error on import

**Cause**: The exported JSON has a syntax error.

**Solution**: Validate the JSON with an online validator before importing.

### Canvas not loading

**Cause**: Browser/DHTML panel issues.

**Solution**: Close and reopen, or type `skilltree_reload_trees` and try again.

---

## Performance

### High CPU usage

**Cause**: Debug mode enabled in production.

**Solution**:
```lua
SkillTree.Config.General.Debug = false
```

### Large trees cause lag on sync

**Cause**: Compressed tree data might be large.

**Solution**: Reduce the number of nodes per tree, or increase `RateLimitNet`.

---

## Common Error Messages

| Error Message | Cause | Solution |
|---------------|-------|----------|
| "Not enough skill points!" | Insufficient points | Award points or level up |
| "Your level is too low!" | Level requirement unmet | Level up or modify requiredLevel |
| "Prerequisites not met!" | Missing required node | Unlock prerequisite first |
| "Wrong Job" | Skill not allowed for this job | Check JobSkills config |
| "Player is AFK" | AFK timeout hit | Disable AFK check in config |
| "Action cooldown active" | Too soon since last action | Wait or reduce cooldown |
| "Minute XP cap reached" | Hit MaxXPPerMinute | Wait or increase the cap |
| "Anti-farm cooldown active" | Same target too soon | Wait or reduce SameTargetCooldown |
