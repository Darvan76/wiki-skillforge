# Hooks

Skillforge fires **11 custom hooks** that you can hook into.

---

## Hook Reference

### SkillTree_PlayerGainedXP

```lua
hook.Add("SkillTree_PlayerGainedXP", "MyIdentifier", function(ply, amount, reason)
```

| Param | Type | Description |
|-------|------|-------------|
| `ply` | Player | Player who gained XP |
| `amount` | int | XP amount (after multipliers) |
| `reason` | string | Reason for XP gain |

**Fired**: After XP is awarded and anti-exploit checks pass.
**Source**: `sv_xp.lua:92`

---

### SkillTree_PlayerLeveledUp

```lua
hook.Add("SkillTree_PlayerLeveledUp", "MyIdentifier", function(ply, newLevel)
```

| Param | Type | Description |
|-------|------|-------------|
| `ply` | Player | Player who leveled up |
| `newLevel` | int | New level number |

**Fired**: After level-up calculation and points awarded.
**Source**: `sv_xp.lua:145`

---

### SkillTree_PlayerUnlockedSkill

```lua
hook.Add("SkillTree_PlayerUnlockedSkill", "MyIdentifier", function(ply, treeID, skillID, rank, skillData)
```

| Param | Type | Description |
|-------|------|-------------|
| `ply` | Player | Player who unlocked the skill |
| `treeID` | string | Active tree ID |
| `skillID` | string | Unlocked skill ID |
| `rank` | int | New rank (1) |
| `skillData` | table | Full skill node data |

**Fired**: The first time a skill is unlocked (rank 0 → 1).
**Source**: `sv_core.lua:77`

---

### SkillTree_PlayerUpgradedSkill

```lua
hook.Add("SkillTree_PlayerUpgradedSkill", "MyIdentifier", function(ply, treeID, skillID, oldRank, newRank, skillData)
```

| Param | Type | Description |
|-------|------|-------------|
| `ply` | Player | Player who upgraded |
| `treeID` | string | Active tree ID |
| `skillID` | string | Upgraded skill ID |
| `oldRank` | int | Previous rank |
| `newRank` | int | New rank |
| `skillData` | table | Full skill node data |

**Fired**: On subsequent upgrades (rank 1 → 2, etc.).
**Source**: `sv_core.lua:79`

---

### SkillTree_PlayerResetSkill

```lua
hook.Add("SkillTree_PlayerResetSkill", "MyIdentifier", function(ply, treeID, skillID, nodeData)
```

**Fired**: Per-skill during a reset operation.
**Source**: `sv_core.lua:134`

---

### SkillTree_ApplySkillEffect

```lua
hook.Add("SkillTree_ApplySkillEffect", "MyIdentifier", function(ply, treeID, skillID, rank, nodeData)
```

**Fired**: Per-skill when effects are applied (spawn, upgrade, re-apply).
**Source**: `sv_effects.lua:93`

---

### SkillTree_EffectsApplied

```lua
hook.Add("SkillTree_EffectsApplied", "MyIdentifier", function(ply, treeID)
```

**Fired**: After all skill effects have been applied.
**Source**: `sv_effects.lua:102`

---

### SkillTree_ActiveSkillUsed

```lua
hook.Add("SkillTree_ActiveSkillUsed", "MyIdentifier", function(ply, treeID, skillID, rank, nodeData)
```

**Fired**: When a player uses an active ability.
**Source**: `sv_effects.lua:166`

---

### SkillTree_GetPlayerTree

```lua
hook.Add("SkillTree_GetPlayerTree", "MyIdentifier", function(ply)
    -- Return a tree ID string to override, or nil to fall through
end)
```

**Fired**: First in the tree resolution chain. Return a tree ID to override all other mappings.
**Source**: `sh_effect_types.lua:63`

---

### SkillTree_PlayerGainedJobXP

```lua
hook.Add("SkillTree_PlayerGainedJobXP", "MyIdentifier", function(ply, amount, reason, jobName)
```

**Fired**: After job-specific XP is awarded.
**Source**: `server/sv_job_xp.lua:213`

---

### SkillTree_PlayerHealed

```lua
hook.Add("SkillTree_PlayerHealed", "MyIdentifier", function(healer, target, amount)
```

**Fired**: Heal event from DarkRP or custom healing systems.
**Source**: `integrations/sv_darkrp_medic.lua:9`

---

## Complete Hook Usage Example

```lua
-- Log all XP gains
hook.Add("SkillTree_PlayerGainedXP", "MyXPLogger", function(ply, amount, reason)
    print(ply:Nick() .. " gained " .. amount .. " XP (" .. reason .. ")")
end)

-- Give money on level up
hook.Add("SkillTree_PlayerLeveledUp", "MyLevelUpReward", function(ply, newLevel)
    if DarkRP then
        ply:addMoney(newLevel * 100)
    end
end)

-- Custom tree assignment
hook.Add("SkillTree_GetPlayerTree", "MyTreeAssigner", function(ply)
    if ply:GetUserGroup() == "vip" then
        return "vip_tree"
    end
    return nil  -- Fallback to normal mapping
end)
```
