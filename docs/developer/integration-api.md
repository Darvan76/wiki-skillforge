# Integration API

Public API functions for integrating custom systems with Skillforge.

---

## Police Integration

```lua
-- Report a weapon confiscation
SkillTree.ReportWeaponConfiscated(ply, target, weaponClass)

-- Report contraband confiscation
SkillTree.ReportIllegalEntityConfiscated(ply, ent)
```

Source: `integrations/sv_darkrp_police.lua`

---

## Medic Integration

```lua
-- Report a player revive
SkillTree.ReportPlayerRevived(healer, target)
```

Source: `integrations/sv_darkrp_medic.lua`

---

## Criminal Integration

```lua
-- Report a completed robbery
SkillTree.ReportRobberyCompleted(ply, moneyStolen)

-- Report a stolen money printer
SkillTree.ReportStealPrinter(ply, printer)
```

Source: `integrations/sv_darkrp_criminal.lua`

---

## Economy Integration

```lua
-- Report a weapon sale
SkillTree.ReportWeaponSold(dealer, buyer, weaponClass)

-- Report an ammo sale
SkillTree.ReportAmmoSold(dealer, buyer, ammoType)

-- Report food cooked
SkillTree.ReportFoodCooked(cook, foodClass)

-- Report food sold
SkillTree.ReportFoodSold(cook, buyer, foodClass)
```

Source: `integrations/sv_darkrp_economy.lua`

---

## Garbage Integration

```lua
-- Report garbage collected (in kg)
SkillTree.ReportGarbageCollected(ply, kg)

-- Report garbage recycled (in kg)
SkillTree.ReportGarbageRecycled(ply, kg)

-- Report garbage bag delivered
SkillTree.ReportGarbageDelivered(ply, bagWeight)

-- Report route completed
SkillTree.ReportGarbageRouteCompleted(ply, routeID)
```

Source: `integrations/sv_garbage_example.lua`

---

## DarkRP Utilities

```lua
-- Get the player's current job name
local jobName = SkillTree.DarkRP.GetJobName(ply)

-- Check if a skill is allowed for the player's job
local allowed = SkillTree.DarkRP.CanUseSkill(ply, skillID)

-- Apply printer money bonus
local finalAmount = SkillTree.DarkRP.ApplyPrinterBonus(ply, baseAmount)
```

Source: `sv_darkrp.lua`

---

## Complete Integration Example

```lua title="lua/autorun/skillforge_custom_integration.lua"
-- Integrate a custom job system
local function InitIntegration()
    if not SkillTree then
        timer.Simple(1, InitIntegration)
        return
    end

    -- Register custom XP action
    SkillTree.RegisterJobXPAction("my_custom_job_action", {
        name = "Custom Action",
        defaultXP = 50,
        cooldown = 30,
        maxXPPerMinute = 300,
        jobWhitelist = {"My Custom Job"}
    })

    -- Hook into custom events
    hook.Add("MyCustomJobEvent", "SkillforgeXP", function(ply, target)
        local metadata = {}
        if IsValid(target) and target:IsPlayer() then
            metadata.targetSteamID64 = target:SteamID64()
        end
        SkillTree.AddJobXPByAction(ply, "my_custom_job_action", metadata)
    end)
end
InitIntegration()
```
