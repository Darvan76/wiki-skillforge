# Job XP Configuration

Configure how each job earns XP for specific actions. This is separate from the global XP config and allows fine-grained control per job.

---

## Configuration Table

```lua title="lua/skillforge/shared/sh_job_config.lua"
SkillTree.Config.JobXP = {
    ["Civil Protection"] = {
        ArrestPlayer = {
            Enabled = true,
            XP = 100,
            Cooldown = 30,
            PreventFarmSamePlayer = true,
            MaxXPPerMinute = 300,
            Reason = "Arrested player"
        },
        ArrestWantedPlayer = {
            Enabled = true,
            XP = 150,
            Cooldown = 60,
            PreventFarmSamePlayer = true,
            MaxXPPerMinute = 400,
            Reason = "Arrested wanted player"
        },
        ConfiscateWeapon = {
            Enabled = true,
            XP = 20,
            Cooldown = 10,
            MaxXPPerMinute = 200,
            Reason = "Confiscated weapon"
        },
        ConfiscateIllegalEntity = {
            Enabled = true,
            XP = 30,
            Cooldown = 10,
            MaxXPPerMinute = 200,
            Reason = "Confiscated contraband"
        }
    },
    -- ... more jobs
}
```

---

## Parameters per Action

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `Enabled` | bool | `true` | Enable this XP action |
| `XP` | int | varies | XP awarded per action |
| `XPPerKG` | int | varies | XP per unit (garbage, HP, etc.) |
| `Cooldown` | int | varies | Seconds between actions |
| `PreventFarmSamePlayer` | bool | `false` | Anti-farm for same target |
| `MaxXPPerMinute` | int | varies | Cap per minute |
| `Reason` | string | varies | Display reason for XP gain |

---

## All Default Job XP Configs

### Police Chief

```lua
["Police Chief"] = {
    ArrestPlayer = { Enabled = true, XP = 120, Cooldown = 30, PreventFarmSamePlayer = true, MaxXPPerMinute = 300 },
    ArrestWantedPlayer = { Enabled = true, XP = 180, Cooldown = 60, PreventFarmSamePlayer = true, MaxXPPerMinute = 400 }
}
```

### Garbage Collector

```lua
["Garbage Collector"] = {
    GarbageCollectedPerKG =  { Enabled = true, XPPerKG = 5, MaxXPPerMinute = 200 },
    GarbageRecycledPerKG =   { Enabled = true, XPPerKG = 10, MaxXPPerMinute = 300 },
    GarbageBagDelivered =    { Enabled = true, XP = 50, Cooldown = 5 },
    GarbageRouteCompleted =  { Enabled = true, XP = 200, Cooldown = 300 }
}
```

### Medic

```lua
["Medic"] = {
    HealPlayer =  { Enabled = true, XPPerHP = 1, MaxXPPerMinute = 250, PreventSelfFarm = true },
    RevivePlayer = { Enabled = true, XP = 150, Cooldown = 45 }
}
```

### Thief

```lua
["Thief"] = {
    LockpickSuccess = { Enabled = true, XP = 50, Cooldown = 20 },
    RobberyCompleted = { Enabled = true, XP = 200, Cooldown = 180 },
    StealPrinter =    { Enabled = true, XP = 75, Cooldown = 60 }
}
```

### Gun Dealer

```lua
["Gun Dealer"] = {
    SellWeapon = { Enabled = true, XP = 50, Cooldown = 15, PreventFarmSamePlayer = true },
    SellAmmo =   { Enabled = true, XP = 15, Cooldown = 5 }
}
```

### Cook

```lua
["Cook"] = {
    CookFood = { Enabled = true, XP = 20, Cooldown = 5 },
    SellFood = { Enabled = true, XP = 30, Cooldown = 10 }
}
```

---

## Examples

### Double police XP

```lua
SkillTree.Config.JobXP["Civil Protection"] = {
    ArrestPlayer = { Enabled = true, XP = 200, Cooldown = 30 },
    ArrestWantedPlayer = { Enabled = true, XP = 300, Cooldown = 60 },
    ConfiscateWeapon = { Enabled = true, XP = 40, Cooldown = 10 }
}
```

### Disable criminal XP

```lua
SkillTree.Config.JobXP["Thief"] = {
    LockpickSuccess = { Enabled = false },
    RobberyCompleted = { Enabled = false },
    StealPrinter = { Enabled = false }
}
```

### Add a new job

```lua
SkillTree.Config.JobXP["My Custom Job"] = {
    MyAction = { Enabled = true, XP = 75, Cooldown = 20 }
}
```
