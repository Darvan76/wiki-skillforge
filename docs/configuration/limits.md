# Stat Limits

Define hard caps for all gameplay multipliers to prevent imbalance.

---

## Configuration Table

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.Limits = {
    MaxWalkSpeedMultiplier = 1.25,
    MaxRunSpeedMultiplier = 1.25,
    MaxJumpMultiplier = 1.30,
    MaxDamageMultiplier = 1.20,
    MaxDamageResistance = 0.20,
    MaxMoneyMultiplier = 1.15,
    MaxXPMultiplier = 1.25
}
```

---

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `MaxWalkSpeedMultiplier` | float | `1.25` | Max walk speed boost (25%) |
| `MaxRunSpeedMultiplier` | float | `1.25` | Max run speed boost (25%) |
| `MaxJumpMultiplier` | float | `1.30` | Max jump power boost (30%) |
| `MaxDamageMultiplier` | float | `1.20` | Max damage dealt boost (20%) |
| `MaxDamageResistance` | float | `0.20` | Max damage reduction (20%) |
| `MaxMoneyMultiplier` | float | `1.15` | Max DarkRP money boost (15%) |
| `MaxXPMultiplier` | float | `1.25` | Max XP gain boost (25%) |

!!! warning "Balance matters"
    Setting limits too high can break server balance. Test thoroughly with your server's specific gameplay.

---

## How Limits Are Applied

Limits are enforced inside `STN_GetSkillEffectValue()` in `sh_effect_types.lua`. After calculating the total multiplier from all active skills, the value is clamped:

```lua
if effectType == "WalkSpeedMultiplier" and limits.MaxWalkSpeedMultiplier then
    totalBonus = math.min(totalBonus, limits.MaxWalkSpeedMultiplier)
end
```

---

## Examples

### High-power server (OP skills)

```lua
SkillTree.Config.Limits.MaxDamageMultiplier = 2.0
SkillTree.Config.Limits.MaxWalkSpeedMultiplier = 1.75
SkillTree.Config.Limits.MaxJumpMultiplier = 2.0
SkillTree.Config.Limits.MaxDamageResistance = 0.50
```

### Competitive server (tight limits)

```lua
SkillTree.Config.Limits.MaxDamageMultiplier = 1.10
SkillTree.Config.Limits.MaxWalkSpeedMultiplier = 1.10
SkillTree.Config.Limits.MaxRunSpeedMultiplier = 1.10
SkillTree.Config.Limits.MaxJumpMultiplier = 1.15
SkillTree.Config.Limits.MaxDamageResistance = 0.10
SkillTree.Config.Limits.MaxMoneyMultiplier = 1.05
SkillTree.Config.Limits.MaxXPMultiplier = 1.10
```
