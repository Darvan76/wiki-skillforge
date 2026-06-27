# Effect Types

Skillforge has **28 registered effect types** that nodes can apply — 23 passive and 5 active.

---

## Passive Effects

| Effect Type | Description | Value Type | Example Value |
|-------------|-------------|------------|---------------|
| `WalkSpeedMultiplier` | Multiplies walk speed | Multiplier | `1.10` (+10%) |
| `RunSpeedMultiplier` | Multiplies run speed | Multiplier | `1.10` (+10%) |
| `JumpPowerMultiplier` | Multiplies jump power | Multiplier | `1.15` (+15%) |
| `MaxHealthBonus` | Adds to max health | Additive | `25` (+25 HP) |
| `MaxArmorBonus` | Adds to max armor | Additive | `25` (+25 armor) |
| `DamageMultiplier` | Multiplies damage dealt | Multiplier | `1.10` (+10%) |
| `DamageResistance` | Reduces damage taken | Percentage | `0.10` (10%) |
| `DarkRPMoneyMultiplier` | Multiplies money earned | Multiplier | `1.15` (+15%) |
| `XPMultiplier` | Multiplies XP gained | Multiplier | `1.25` (+25%) |
| `SalaryMultiplier` | Multiplies DarkRP salary | Multiplier | `1.20` (+20%) |
| `FallDamageReduction` | Reduces fall damage | Percentage | `0.25` (25%) |
| `RecoilReduction` | Reduces weapon recoil | Percentage | `0.15` (15%) |
| `ReloadSpeedBonus` | Increases reload speed | Multiplier | `1.15` (+15%) |
| `AmmoCapacityBonus` | Increases ammo capacity | Additive | `30` (+30 ammo) |
| `ShopDiscount` | Reduces shop prices | Multiplier | `0.90` (10% off) |
| `PrinterMoneyBonus` | Increases printer money | Multiplier | `1.20` (+20%) |
| `LockpickSpeedBonus` | Increases lockpick speed | Multiplier | `1.25` (+25%) |
| `SpawnWithArmor` | Spawn with extra armor | Additive | `50` (+50 armor) |
| `CraftingSpeedBonus` | Increases crafting speed | Multiplier | `1.20` (+20%) |
| `JobActionXPMultiplier` | Job-specific XP multiplier | Multiplier | `1.30` (+30%) |
| `JobCooldownReduction` | Reduces job action cooldowns | Multiplier | `0.80` (20% less) |
| `JobMoneyMultiplier` | Job-specific money multiplier | Multiplier | `1.15` (+15%) |
| `PassiveRegen` | Passive HP regeneration per tick | Additive | `2` (2 HP/2s) |

---

## Active Effects

| Effect Type | Description | Default Value | Duration |
|-------------|-------------|---------------|----------|
| `Dash` | Short forward dash | Speed: 500 | Instant |
| `Shield` | Temporary damage shield | HP: 50 | 8s |
| `Berserker` | Temp damage & speed boost | Multiplier: 1.3x | 6s |
| `SpeedSurge` | Temporary speed boost | Multiplier: 1.5x | 10s |
| `DoubleXP` | Temporary double XP | Multiplier: 2x | 120s |
| `QuickHeal` | Instant health recovery | HP: 25 | Instant |
| `CustomFunction` | Custom Hook/Callback | — | — |

---

## Implementation Reference

```lua title="lua/skillforge/sh_effect_types.lua"
SkillTree.EffectTypes = {
    WalkSpeedMultiplier = "Multiplies walk speed",
    RunSpeedMultiplier = "Multiplies run speed",
    JumpPowerMultiplier = "Multiplies jump power",
    MaxHealthBonus = "Adds to max health",
    MaxArmorBonus = "Adds to max armor",
    DamageMultiplier = "Multiplies dealt damage",
    DamageResistance = "Reduces taken damage",
    DarkRPMoneyMultiplier = "Multiplies DarkRP money earned",
    XPMultiplier = "Multiplies XP gained",
    SalaryMultiplier = "Multiplies DarkRP salary",
    FallDamageReduction = "Reduces fall damage",
    RecoilReduction = "Reduces weapon recoil",
    ReloadSpeedBonus = "Increases reload speed",
    AmmoCapacityBonus = "Increases ammo capacity",
    ShopDiscount = "Reduces shop prices",
    PrinterMoneyBonus = "Increases printer money",
    LockpickSpeedBonus = "Increases lockpick speed",
    SpawnWithArmor = "Spawn with armor",
    CraftingSpeedBonus = "Increases crafting speed",
    JobActionXPMultiplier = "Multiplies XP from job actions",
    JobCooldownReduction = "Reduces job action cooldowns",
    JobMoneyMultiplier = "Multiplies money from job actions",
    PassiveRegen = "Passive slow HP regen",
    ArrestSpeedMultiplier = "Multiplies arrest speed",
    SearchSpeedMultiplier = "Multiplies search/confiscate speed",
    HealAmountMultiplier = "Multiplies HP restored when healing",
    ReviveSpeedMultiplier = "Multiplies revive speed",
    DrugDurationMultiplier = "Multiplies drug effect duration",
    FencePriceMultiplier = "Multiplies fence sell prices",
    CarryWeightBonus = "Adds carry weight capacity",
    Dash = "Short forward dash",
    Shield = "Temporary damage shield",
    Berserker = "Temporary damage and speed boost",
    QuickHeal = "Instant health recovery",
    SpeedSurge = "Temporary speed boost",
    DoubleXP = "Temporary double XP",
    CustomFunction = "Custom Hook/Callback"
}
```

---

## How Effects Are Applied

1. Player upgrades a node → `SkillTree.UpgradeSkill()` is called
2. `UpgradeSkill` calls `SkillTree.ApplySkillEffects(ply, treeID)`
3. `ApplySkillEffects` iterates all player's skills and:
   - Sets walk/run/jump speeds based on multipliers
   - Sets max health based on bonuses
   - Fires `SkillTree_ApplySkillEffect` hook for each skill
   - Runs any registered callbacks

```lua title="lua/skillforge/sv_effects.lua"
function SkillTree.ApplySkillEffects(ply, treeID)
    local walkMult = ply:STN_GetSkillEffectValue("WalkSpeedMultiplier")
    local runMult = ply:STN_GetSkillEffectValue("RunSpeedMultiplier")
    local jumpMult = ply:STN_GetSkillEffectValue("JumpPowerMultiplier")
    local maxHealthBonus = ply:STN_GetSkillEffectValue("MaxHealthBonus")

    ply:SetWalkSpeed(baseWalk * walkMult)
    ply:SetRunSpeed(baseRun * runMult)
    ply:SetJumpPower(baseJump * jumpMult)
    ply:SetMaxHealth(baseHealth + maxHealthBonus)

    -- Fire hook per skill
    hook.Run("SkillTree_ApplySkillEffect", ply, treeID, skillID, rank, node)
end
```

Effects are re-applied on:
- Skill upgrade/unlock
- Player spawn
- Job change
- Manual re-apply (`skilltree_reapply_effects` command)
