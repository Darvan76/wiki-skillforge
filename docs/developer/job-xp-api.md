# Job XP API

Create custom XP actions for any job.

---

## Registering a Job XP Action

```lua
SkillTree.RegisterJobXPAction(actionID, data)
```

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| `actionID` | string | required | Unique action identifier |
| `data.name` | string | `actionID` | Display name |
| `data.defaultXP` | int | `0` | Flat XP awarded |
| `data.xpPerUnit` | int | `0` | XP per quantity unit |
| `data.unitName` | string | `""` | Unit label (e.g. "kg", "HP") |
| `data.cooldown` | int | `0` | Seconds between uses |
| `data.maxXPPerMinute` | int | `300` | Cap per minute |
| `data.jobWhitelist` | table | `nil` | Allowed job names (nil = any) |
| `data.antiFarm` | bool | `true` | Enable anti-farming |

---

## Giving XP via Actions

### AddJobXPByAction

```lua
SkillTree.AddJobXPByAction(ply, actionID, amountData)
```

This is the primary way to award job XP. It handles validation, cooldowns, anti-farm, and rate limits automatically.

| Param | Type | Description |
|-------|------|-------------|
| `ply` | Player | Target player |
| `actionID` | string | Registered action ID |
| `amountData` | table | Additional data (optional) |

### amountData fields

| Field | Type | Description |
|-------|------|-------------|
| `units` | int | Quantity for `xpPerUnit` |
| `kg` | int | Alias for units (garbage) |
| `hp` | int | Alias for units (healing) |
| `targetSteamID64` | string | Target for anti-farm tracking |

### AddJobXP

```lua
SkillTree.AddJobXP(ply, amount, reason, jobID, metadata)
```

Raw XP addition in a job context. Use `AddJobXPByAction` instead for most cases.

---

## Validation & Anti-Farm

`CanGiveJobXP` checks all of these automatically:

```lua
local canGive, err = SkillTree.CanGiveJobXP(ply, actionID, amount, metadata)
if not canGive then
    -- Reason: "Invalid player", "Player is AFK", "Unregistered action",
    --         "Action cooldown active", "Anti-farm cooldown active",
    --         "Minute XP cap reached"
    return
end
```

---

## Example: Custom Job XP Action

```lua title="lua/autorun/skillforge_job_actions.lua"
hook.Add("Initialize", "RegisterMyActions", function()
    -- Register a mining action for a "Miner" job
    SkillTree.RegisterJobXPAction("miner_mine_ore", {
        name = "Ore Mined",
        defaultXP = 30,
        xpPerUnit = 5,
        unitName = "ore",
        cooldown = 5,
        maxXPPerMinute = 400,
        jobWhitelist = {"Miner"}
    })

    -- Register a delivery action
    SkillTree.RegisterJobXPAction("miner_delivery", {
        name = "Ore Delivery",
        defaultXP = 100,
        cooldown = 60,
        jobWhitelist = {"Miner"}
    })
end)

-- Give XP when mining
function MineOre(ply, amount)
    -- Your mining logic
    SkillTree.AddJobXPByAction(ply, "miner_mine_ore", {
        units = amount
    })
end

-- Give XP on delivery
function DeliverOre(ply)
    SkillTree.AddJobXPByAction(ply, "miner_delivery")
end
```

---

## Default Registered Actions

These are registered automatically on `Initialize`:

```lua
-- Police
"police_arrest", "police_arrest_wanted", "police_confiscate_weapon", "police_confiscate_illegal"

-- Garbage Collector
"garbage_collected", "garbage_recycled", "garbage_bag_delivered", "garbage_route_completed"

-- Medic
"medic_heal", "medic_revive"

-- Criminal
"thief_lockpick", "thief_robbery", "thief_steal_printer"

-- Economy
"merchant_sell_weapon", "merchant_sell_ammo"

-- Food
"cook_food", "cook_sell"
```
