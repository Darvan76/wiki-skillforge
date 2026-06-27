# DarkRP Core Integration

The core DarkRP integration hooks into fundamental DarkRP systems to provide XP and effects.

---

## Enabling DarkRP

```lua
SkillTree.Config.General.EnableDarkRP = true
```

If DarkRP is not detected, the integration is safely skipped:

```lua title="lua/skillforge/sv_darkrp.lua"
if not SkillTree.Config.General.EnableDarkRP then return end
```

---

## Hooks

### Salary Multiplier

Multiplies the player's DarkRP salary based on the `SalaryMultiplier` skill effect.

```lua
hook.Add("playerGetSalary", "stn_darkrp_salary", function(ply, amount)
    local mult = ply:STN_GetSkillEffectValue("SalaryMultiplier")
    if mult and mult > 0 and mult ~= 1 then
        return false, "", math.floor(amount * mult)  -- Override salary
    end
end)
```

### Money Gain XP & Multiplier

Grants XP when a player earns money, and applies the `DarkRPMoneyMultiplier` effect.

```lua
hook.Add("playerWalletChanged", "stn_darkrp_money_xp", function(ply, amount, wallet)
    if amount <= 0 then return end  -- Only gains, not losses

    -- XP from money
    local xpGain = math.floor(amount * xpRate.XPPerMoney)
    SkillTree.AddXP(ply, xpGain, "Money Earned")

    -- Money multiplier bonus
    local bonus = math.floor(amount * (moneyMult - 1))
    ply:addMoney(bonus)
end)
```

### Arrest XP

Grants XP when a player arrests another player.

```lua
hook.Add("playerArrested", "stn_darkrp_arrest", function(criminal, time, arrester)
    SkillTree.AddXP(arrester, xpRate.Amount, "Arrest")
end)
```

### Job Change XP

Grants XP when a player tries a job for the first time.

```lua
hook.Add("OnPlayerChangedTeam", "stn_darkrp_jobchange", function(ply, oldTeam, newTeam)
    -- Reload player data for the new job's tree
    timer.Simple(0.5, function()
        SkillTree.DB_LoadPlayerActiveTree(ply)
    end)

    -- First-time job bonus
    if not ply.stnJobsPlayed[newTeam] then
        ply.stnJobsPlayed[newTeam] = true
        SkillTree.AddXP(ply, xpRate.Amount, "First Time Job")
    end
end)
```

### Shop Discount

Refunds money when a player buys from the DarkRP shop, based on the `ShopDiscount` effect.

```lua
hook.Add("playerBoughtCustomEntity", "stn_darkrp_discount_refund", function(ply, entTable, ent, price)
    local discount = ply:STN_GetSkillEffectValue("ShopDiscount")
    if discount and discount > 0 and discount ~= 1 then
        local refund = math.floor(price * (1 - discount))
        ply:addMoney(refund)
        SkillTree.Net.SendNotification(ply, "Discount applied: $" .. refund .. " refunded!", "success")
    end
end)
```

Also applies to vehicle purchases via `playerBoughtVehicle`.

### Heal XP

Grants XP when a player uses a medkit:

```lua
hook.Add("EntityUse", "stn_darkrp_heal_use", function(ply, ent)
    if ent:GetClass() == "med_kit" then
        SkillTree.AddXP(ply, xpRate.Amount, "Heal")
    end
end)
```

---

## Utility Functions

### Get Job Name

```lua
SkillTree.DarkRP.GetJobName(ply)  -- Returns current job name string
```

### Check Job Skill Allowed

```lua
SkillTree.DarkRP.CanUseSkill(ply, "combat_training")  -- Returns boolean
```

### Printer Money Bonus

```lua
SkillTree.DarkRP.ApplyPrinterBonus(ply, baseAmount)  -- Returns modified amount
```
