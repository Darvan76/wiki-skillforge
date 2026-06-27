# Leveling System

Controls XP requirements, skill points, and bonus point distribution.

---

## Configuration Table

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.Leveling = {
    MaxLevel = 100,
    BaseXP = 100,
    GrowthMultiplier = 1.15,
    SkillPointsPerLevel = 1,
    BonusPointsEveryXLevels = {
        Enabled = true,
        Every = 10,
        Amount = 2
    }
}
```

---

## XP Formula

The XP required for each level follows an exponential curve:

```lua title="lua/skillforge/sh_effect_types.lua"
function SkillTree.CalcRequiredXP(level)
    local base = SkillTree.Config.Leveling.BaseXP or 100
    local mult = SkillTree.Config.Leveling.GrowthMultiplier or 1.15
    return math.floor(base * (mult ^ (level - 1)))
end
```

### XP Requirements by Level

| Level | XP Required | Total XP | Points Earned |
|-------|-------------|----------|---------------|
| 1 | 100 | 0 | 0 |
| 2 | 115 | 100 | 1 |
| 3 | 132 | 215 | 2 |
| 4 | 152 | 347 | 3 |
| 5 | 175 | 499 | 4 |
| 10 | 352 | 2,030 | 11 (9 + 2 bonus) |
| 25 | 3,291 | 27,215 | 28 |
| 50 | 76,607 | 408,923 | 55 |
| 100 | 4,197,892 | 26,737,438 | 121 |

---

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `MaxLevel` | int | `100` | Maximum achievable level |
| `BaseXP` | int | `100` | XP needed for level 1→2 |
| `GrowthMultiplier` | float | `1.15` | Exponential growth rate |
| `SkillPointsPerLevel` | int | `1` | Base points earned per level-up |
| `BonusPointsEveryXLevels.Enabled` | bool | `true` | Enable bonus point milestones |
| `BonusPointsEveryXLevels.Every` | int | `10` | Level interval for bonus points |
| `BonusPointsEveryXLevels.Amount` | int | `2` | Bonus points awarded at each milestone |

---

## Examples

### Fast progression (casual server)

```lua
SkillTree.Config.Leveling.BaseXP = 50
SkillTree.Config.Leveling.GrowthMultiplier = 1.10
SkillTree.Config.Leveling.SkillPointsPerLevel = 2
SkillTree.Config.Leveling.BonusPointsEveryXLevels = {
    Enabled = true,
    Every = 5,
    Amount = 3
}
```

### Slow progression (hardcore server)

```lua
SkillTree.Config.Leveling.MaxLevel = 50
SkillTree.Config.Leveling.BaseXP = 200
SkillTree.Config.Leveling.GrowthMultiplier = 1.20
SkillTree.Config.Leveling.SkillPointsPerLevel = 1
SkillTree.Config.Leveling.BonusPointsEveryXLevels.Enabled = false
```

### Disable bonus points

```lua
SkillTree.Config.Leveling.BonusPointsEveryXLevels.Enabled = false
```
