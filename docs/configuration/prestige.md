# Prestige System

Allow players to reset their progress for permanent bonuses.

---

## Configuration Table

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.Prestige = {
    Enabled = true,
    MaxPrestige = 10,
    ResetSkills = true,
    BonusSkillPoints = 3,
    XPMultiplierPerPrestige = 0.02
}
```

---

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `Enabled` | bool | `true` | Enable prestige system |
| `MaxPrestige` | int | `10` | Maximum prestige level |
| `ResetSkills` | bool | `true` | Reset all skills on prestige |
| `BonusSkillPoints` | int | `3` | Bonus points awarded per prestige |
| `XPMultiplierPerPrestige` | float | `0.02` | XP multiplier increase per prestige |

---

## How Prestige Works

1. Player reaches max level
2. Player chooses to prestige
3. Skills are reset (optional)
4. Player gains bonus skill points
5. Player receives a permanent XP multiplier

### XP Multiplier Formula

```
Total XP Bonus = 1 + (prestige_level * XPMultiplierPerPrestige)

At prestige 10 with 0.02 per level:
Total = 1 + (10 * 0.02) = 1.20 → +20% XP
```

---

## Examples

### Hardcore prestige

```lua
SkillTree.Config.Prestige.MaxPrestige = 5
SkillTree.Config.Prestige.BonusSkillPoints = 1
SkillTree.Config.Prestige.XPMultiplierPerPrestige = 0.05
```

### Casual prestige

```lua
SkillTree.Config.Prestige.MaxPrestige = 20
SkillTree.Config.Prestige.BonusSkillPoints = 5
SkillTree.Config.Prestige.XPMultiplierPerPrestige = 0.01
```

### Disable prestige

```lua
SkillTree.Config.Prestige.Enabled = false
```
