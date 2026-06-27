# Callbacks

Callbacks are developer-registered Lua functions that execute when a skill node is upgraded.

---

## How Callbacks Work

1. A tree node specifies a `callback` field (e.g. `"Custom_MoneyBoost"`)
2. The developer registers a callback function via `SkillTree.RegisterCallback`
3. When the skill is upgraded or effects are re-applied, the callback executes
4. Unknown/unregistered callback names are blocked for security

---

## Registration

```lua
SkillTree.RegisterCallback(callbackName, function)
```

| Param | Type | Description |
|-------|------|-------------|
| `callbackName` | string | Callback identifier (alphanumeric only) |
| `function` | function | Callback function |

### Callback Function Signature

```lua
function(ply, treeID, skillID, rank, skillData)
```

| Param | Type | Description |
|-------|------|-------------|
| `ply` | Player | Player who owns the skill |
| `treeID` | string | Active tree ID |
| `skillID` | string | Skill/node ID |
| `rank` | int | Current rank |
| `skillData` | table | Full node data |

---

## Built-in Callbacks

```lua title="lua/skillforge/sv_callbacks.lua"
SkillTree.RegisterCallback("Custom_MoneyBoost", function(ply, treeID, skillID, rank, skillData)
    local value = skillData.effectValue and skillData.effectValue[rank] or 1
    ply.STN_MoneyMultiplier = value
end)

SkillTree.RegisterCallback("Custom_ArrestBonus", function(ply, treeID, skillID, rank, skillData)
    local value = skillData.effectValue and skillData.effectValue[rank] or 1
    ply.STN_ArrestMultiplier = value
end)

SkillTree.RegisterCallback("Custom_ShopDiscount", function(ply, treeID, skillID, rank, skillData)
    local value = skillData.effectValue and skillData.effectValue[rank] or 1
    ply.STN_ShopDiscountMultiplier = value
end)

-- No-op callbacks (backwards compatibility)
SkillTree.RegisterCallback("Custom_SpeedBoost", function() end)
SkillTree.RegisterCallback("Custom_JumpBoost",  function() end)
SkillTree.RegisterCallback("Custom_ArmorBoost",  function() end)
```

---

## Custom Callback Example

```lua title="lua/autorun/skillforge_callbacks.lua"
-- Register a callback that gives the player health
SkillTree.RegisterCallback("My_HealOnUnlock", function(ply, treeID, skillID, rank, skillData)
    if rank == 1 then  -- Only on first unlock
        ply:SetHealth(math.min(ply:Health() + 50, ply:GetMaxHealth()))
    end
end)
```

Then reference it in a tree node:

```json
{
    "vitality_boost": {
        "name": "Vitality Boost",
        "callback": "My_HealOnUnlock",
        "effectType": "MaxHealthBonus",
        "effectValue": [10, 20, 30],
        ...
    }
}
```

---

## Security

Callbacks are protected against abuse. Unknown callback names are logged and blocked:

```lua title="lua/skillforge/sv_callbacks.lua"
function SkillTree.RunCallback(callbackName, ply, treeID, skillID, rank, skillData)
    if not SkillTree.HasCallback(callbackName) then
        SkillTree.Log.Add("security",
            "Blocked unknown callback '" .. callbackName .. "' on tree '" .. treeID .. "' skill '" .. skillID .. "'")
        return
    end

    local ok, err = pcall(SkillTree.CustomCallbacks[callbackName], ply, treeID, skillID, rank, skillData)
    if not ok then
        ErrorNoHalt("Error executing callback '" .. callbackName .. "': " .. tostring(err))
    end
end
```

!!! tip "Callback registration required"
    A callback must be registered via `SkillTree.RegisterCallback` before it can be used. Any callback name in a tree JSON that hasn't been registered will be silently blocked and logged as a security event.

---

## Related Functions

| Function | Description |
|----------|-------------|
| `SkillTree.RegisterCallback(name, func)` | Register a callback |
| `SkillTree.HasCallback(name)` | Check if callback exists |
| `SkillTree.RunCallback(name, ...)` | Execute a callback (usually called internally) |
