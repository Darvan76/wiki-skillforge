# Criminal Integration

Automated XP hooks and public API for criminal jobs.

---

## How It Works

The criminal integration hooks into DarkRP's lockpick system and provides APIs for robberies and printer theft.

## Hooks

### Lockpick XP

Grants XP when a player successfully lockpicks a door or keypad:

```lua title="lua/skillforge/integrations/sv_darkrp_criminal.lua"
hook.Add("lockpickUnlocked", "stn_criminal_lockpick_xp", function(ply, ent)
    SkillTree.AddJobXPByAction(ply, "thief_lockpick", {
        entityClass = ent:GetClass(),
        entityID = ent:EntIndex()
    })
end)
```

---

## Public API

### Report Robbery Completed

Call this when a robbery is completed (ATM hack, bank vault, etc.):

```lua
SkillTree.ReportRobberyCompleted(ply, moneyStolen)

-- Example:
function CompleteRobbery(ply, amount)
    ply:addMoney(amount)
    SkillTree.ReportRobberyCompleted(ply, amount)
end
```

### Report Printer Stolen

Call this when a player steals another player's money printer:

```lua
SkillTree.ReportStealPrinter(ply, printer)

-- Example:
function StealPrinter(ply, printer)
    printer:Setowning_ent(ply)
    SkillTree.ReportStealPrinter(ply, printer)
end
```

---

## XP Actions

| Action ID | Description | Default XP | Cooldown |
|-----------|-------------|------------|----------|
| `thief_lockpick` | Lockpick a door | 50 | 15s |
| `thief_robbery` | Complete a robbery | 200 | 120s |
| `thief_steal_printer` | Steal a printer | 75 | 30s |

---

## Example: Bank Robbery Integration

```lua
-- Connect your bank robbery system to Skillforge
function BankRobbery_Complete(ply)
    local moneyStolen = 5000
    ply:addMoney(moneyStolen)

    SkillTree.ReportRobberyCompleted(ply, moneyStolen)
    SkillTree.AddXP(ply, 100, "Bank Robbery")
end
```

---

## Related Configuration

```lua
SkillTree.Config.JobXP["Thief"] = {
    LockpickSuccess = { Enabled = true, XP = 50, Cooldown = 20 },
    RobberyCompleted = { Enabled = true, XP = 200, Cooldown = 180 },
    StealPrinter = { Enabled = true, XP = 75, Cooldown = 60 }
}

SkillTree.Config.JobXP["Mob Boss"] = {
    KeypadBypass = { Enabled = true, XP = 60, Cooldown = 30 },
    RaidCompleted = { Enabled = true, XP = 300, Cooldown = 300 }
}
```
