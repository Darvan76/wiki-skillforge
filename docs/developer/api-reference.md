# API Reference

Complete documentation of all public functions.

---

## XP & Leveling

### AddXP

```lua
SkillTree.AddXP(ply, amount, reason)
```

Award XP to a player. Applies multipliers, anti-exploit checks, and triggers level-up checks.

| Param | Type | Description |
|-------|------|-------------|
| `ply` | Player | Target player |
| `amount` | int | XP amount to award |
| `reason` | string | Display reason for XP gain |

**Source**: `sv_xp.lua:35`

### GiveSkillPoints

```lua
SkillTree.GiveSkillPoints(ply, amount, treeID)
```

Award skill points to a player.

| Param | Type | Description |
|-------|------|-------------|
| `ply` | Player | Target player |
| `amount` | int | Amount to add (can be negative) |
| `treeID` | string | (optional) Tree ID, defaults to active tree |

**Source**: `sv_xp.lua:11`

### CalcRequiredXP

```lua
SkillTree.CalcRequiredXP(level)
```

Calculate XP needed for a specific level.

| Param | Type | Description |
|-------|------|-------------|
| `level` | int | Target level |
| **Returns** | int | XP required |

**Formula**: `floor(BaseXP * GrowthMultiplier^(level-1))`

**Source**: `sh_effect_types.lua:224`

### CalcTotalXP

```lua
SkillTree.CalcTotalXP(level)
```

Calculate total XP accumulated to reach a level.

| Param | Type | Description |
|-------|------|-------------|
| `level` | int | Target level |
| **Returns** | int | Total XP |

**Source**: `sh_effect_types.lua:230`

---

## Skills

### UpgradeSkill

```lua
SkillTree.UpgradeSkill(ply, treeID, skillID)
```

Attempt to upgrade a skill for a player. Checks level, points, prerequisites, and job restrictions.

| Param | Type | Description |
|-------|------|-------------|
| `ply` | Player | Target player |
| `treeID` | string | Tree ID |
| `skillID` | string | Skill/node ID |

**Source**: `sv_core.lua:33`

### CanUpgradeSkill

```lua
local canUpgrade, reason = SkillTree.CanUpgradeSkill(ply, treeID, skillID)
```

Check if a skill can be upgraded without performing the upgrade.

| Param | Type | Description |
|-------|------|-------------|
| `ply` | Player | Target player |
| `treeID` | string | Tree ID |
| `skillID` | string | Skill/node ID |
| **Returns** | bool, string | Whether upgrade is possible, reason string |

**Source**: `sh_effect_types.lua:271`

### CanUnlockSkill

```lua
local canUnlock, reason = SkillTree.CanUnlockSkill(ply, skillID)
```

Shorthand for `CanUpgradeSkill` using the player's active tree.

**Source**: `sh_effect_types.lua:311`

### GetSkillNextRankCost

```lua
local cost = SkillTree.GetSkillNextRankCost(ply, skillID)
```

Get the skill point cost for the next rank.

**Source**: `sh_effect_types.lua:316`

### GetSkillNextRankLevel

```lua
local level = SkillTree.GetSkillNextRankLevel(ply, skillID)
```

Get the required level for the next rank.

**Source**: `sh_effect_types.lua:330`

---

## Trees

### GetTree

```lua
local tree = SkillTree.GetTree(treeID)
```

Get a loaded tree's data.

| Param | Type | Description |
|-------|------|-------------|
| `treeID` | string | Tree identifier |
| **Returns** | table | Tree data or nil |

**Source**: `sv_tree_loader.lua:12`

### GetNode

```lua
local node = SkillTree.GetNode(treeID, nodeID)
```

Get a specific node from a tree.

**Source**: `sv_tree_loader.lua:16`

### GetBranch

```lua
local branch = SkillTree.GetBranch(treeID, branchID)
```

Get a specific branch from a tree.

**Source**: `sv_tree_loader.lua:21`

### LoadTree

```lua
local treeData, err = SkillTree.LoadTree(treeID)
```

Load a tree from disk into memory.

**Source**: `sv_tree_loader.lua:100`

### SaveTree

```lua
local ok, err = SkillTree.SaveTree(treeID, treeData)
```

Save a tree to disk and load into memory.

| Param | Type | Description |
|-------|------|-------------|
| `treeID` | string | Tree identifier |
| `treeData` | table | Tree data |
| **Returns** | bool, string | Success, error message |

**Source**: `sv_tree_loader.lua:111`

### LoadTreesFromDisk

```lua
SkillTree.LoadTreesFromDisk()
```

Reload all trees from `data/skillforge/trees/`.

**Source**: `sv_tree_loader.lua:254`

### ValidateTree

```lua
local isValid, err = SkillTree.ValidateTree(treeData)
```

Validate a tree data structure.

**Source**: `sv_tree_validator.lua:45`

### GetActiveTreeForPlayer

```lua
local treeID = SkillTree.GetActiveTreeForPlayer(ply)
```

Determine which tree a player should use (7-level resolution).

**Source**: `sh_effect_types.lua:48`

---

## Effects

### ApplySkillEffects

```lua
SkillTree.ApplySkillEffects(ply, treeID)
```

Re-apply all skill effects to a player.

**Source**: `sv_effects.lua:47`

### UseAbility

```lua
SkillTree.UseAbility(ply, skillID)
```

Use an active ability skill.

**Source**: `sv_effects.lua:111`

### GetBuff

```lua
local buff = SkillTree.GetBuff(ply, buffName)
```

Get an active buff on a player.

**Source**: `sv_effects.lua:9`

### SetBuff

```lua
SkillTree.SetBuff(ply, buffName, value, duration)
```

Apply a temporary buff to a player.

**Source**: `sv_effects.lua:21`

### RemoveBuff

```lua
SkillTree.RemoveBuff(ply, buffName)
```

Remove a buff from a player.

**Source**: `sv_effects.lua:33`

---

## Admin & Permissions

### ResetPlayerTree

```lua
SkillTree.ResetPlayerTree(ply, treeID)
```

Reset all skills for a player in a tree, with cost/cooldown/refund checks.

**Source**: `sv_core.lua:92`

### IsAdmin

```lua
local isAdmin = SkillTree.IsAdmin(ply)
```

Check if a player has admin access.

**Source**: `sh_effect_types.lua:344`

### HasPermission

```lua
local hasPerm = SkillTree.HasPermission(ply, perm)
```

Check granular permission (SAM/ULX/CAM/fallback).

**Source**: `shared/sh_admin.lua:24`

---

## Data Persistence

### GetPlayerData

```lua
local data = SkillTree.GetPlayerData(ply, treeID)
```

Get player progression data.

**Source**: `server/sv_job_playerdata.lua:51`

### SavePlayerData

```lua
SkillTree.SavePlayerData(ply, treeID)
```

Save player progression data to SQLite.

---

## Utilities

| Function | Description | Source |
|----------|-------------|--------|
| `SkillTree.Lang(key, ...)` | Get localized string | `sh_language.lua:517` |
| `SkillTree.FormatNumber(num)` | Format number with commas | `sh_effect_types.lua:239` |
| `SkillTree.FormatTime(seconds)` | Format seconds as human-readable | `sh_effect_types.lua:245` |
| `SkillTree.ScreenScale(pixels)` | Resolution-independent scaling | `sh_effect_types.lua:258` |
| `SkillTree.LerpColor(fraction, a, b)` | Interpolate between two colors | `sh_effect_types.lua:262` |
| `SkillTree.SetActiveTree(treeID)` | Set the default active tree | `sv_tree_loader.lua:26` |
| `SkillTree.ExportTree(treeID)` | Export tree as JSON string | `sv_tree_loader.lua:152` |
| `SkillTree.ImportTree(jsonString)` | Import tree from JSON string | `sv_tree_loader.lua:160` |

---

## Logging

```lua
SkillTree.Log.Add(category, message)
```

Add a log entry.

| Param | Type | Description |
|-------|------|-------------|
| `category` | string | `"skill"`, `"reset"`, `"admin"`, `"level"`, `"security"`, `"xp"` |
| `message` | string | Log message |

**Source**: `sv_core.lua:11`
