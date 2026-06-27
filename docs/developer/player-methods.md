# Player Methods

Skillforge adds 8 methods to the Player metatable, all prefixed with `STN_`.

---

## Method Reference

### STN_GetLevel

```lua
local level = ply:STN_GetLevel()
```

Returns the player's current level (default: `1`).

**Source**: `sh_effect_types.lua:137`

---

### STN_GetXP

```lua
local xp = ply:STN_GetXP()
```

Returns the player's current XP.

**Source**: `sh_effect_types.lua:141`

---

### STN_GetXPRequired

```lua
local xpRequired = ply:STN_GetXPRequired()
```

Returns the XP required for the next level.

**Source**: `sh_effect_types.lua:145`

---

### STN_GetSkillPoints

```lua
local points = ply:STN_GetSkillPoints()
```

Returns the player's available skill points.

**Source**: `sh_effect_types.lua:149`

---

### STN_GetAllSkills

```lua
local skills = ply:STN_GetAllSkills()
```

Returns a table of all unlocked skills: `{ [skillID] = rank, ... }`.

On the server, reads from `SkillTree.PlayerData`. On the client, reads from the NW variable `stn_skills`.

**Source**: `sh_effect_types.lua:153`

---

### STN_GetSkillRank

```lua
local rank = ply:STN_GetSkillRank(skillID)
```

Returns the rank of a specific skill (0 if not owned).

| Param | Type | Description |
|-------|------|-------------|
| `skillID` | string | Skill identifier |
| **Returns** | int | Current rank (0 = locked) |

**Source**: `sh_effect_types.lua:166`

---

### STN_HasSkill

```lua
local hasSkill = ply:STN_HasSkill(skillID)
```

Returns `true` if the player has at least rank 1 of the skill.

**Source**: `sh_effect_types.lua:171`

---

### STN_GetSkillEffectValue

```lua
local value = ply:STN_GetSkillEffectValue(effectType)
```

Returns the combined effect value from all skills of a given type.

For multipliers, starts at `1` and multiplies all matching effects together. For additives, starts at `0` and adds all matching effects. Results are clamped to config limits.

| Param | Type | Description |
|-------|------|-------------|
| `effectType` | string | Effect type (e.g. `"WalkSpeedMultiplier"`) |
| **Returns** | number | Combined effect value |

```lua
-- Example: Get total XP multiplier
local xpMult = ply:STN_GetSkillEffectValue("XPMultiplier")
-- Returns 1.25 if player has +25% XP boost
```

**Source**: `sh_effect_types.lua:175`

---

## Example Usage

```lua
-- Give a bonus if player has a specific skill
hook.Add("playerArrested", "MyArrestBonus", function(criminal, time, arrester)
    if arrester:STN_HasSkill("efficient_arrest") then
        local rank = arrester:STN_GetSkillRank("efficient_arrest")
        local bonus = rank * 10
        arrester:addMoney(bonus)
    end
end)

-- Display player stats
function ShowPlayerStats(ply)
    print("Level: " .. ply:STN_GetLevel())
    print("XP: " .. ply:STN_GetXP() .. " / " .. ply:STN_GetXPRequired())
    print("Skill Points: " .. ply:STN_GetSkillPoints())
    print("Has combat_training: " .. tostring(ply:STN_HasSkill("combat_training")))
end
```
