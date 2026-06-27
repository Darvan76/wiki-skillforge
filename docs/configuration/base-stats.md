# Base Stats

Configure the base movement and health values that skills modify.

---

## Configuration Table

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.BaseStats = {
    WalkSpeed  = 200,
    RunSpeed   = 400,
    JumpPower  = 200,
    MaxHealth  = 100,
    MaxArmor   = 100,
}
```

---

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `WalkSpeed` | int | `200` | Base walk speed |
| `RunSpeed` | int | `400` | Base run speed |
| `JumpPower` | int | `200` | Base jump power |
| `MaxHealth` | int | `100` | Base max health |
| `MaxArmor` | int | `100` | Base max armor |

---

## Why These Matter

These values serve as the foundation for all skill effect calculations. When a skill grants a `WalkSpeedMultiplier` of `1.25`, the actual speed becomes:

```lua
local baseWalk = SkillTree.Config.BaseStats.WalkSpeed or 200
ply:SetWalkSpeed(baseWalk * walkMult)
-- 200 * 1.25 = 250 walk speed
```

!!! warning "Server compatibility"
    Some DarkRP jobs or other addons may modify base speeds. Adjust these values to match your server's baseline.

---

## Examples

### MTA-style movement (faster)

```lua
SkillTree.Config.BaseStats.WalkSpeed = 250
SkillTree.Config.BaseStats.RunSpeed = 500
SkillTree.Config.BaseStats.JumpPower = 250
```

### Realistic movement (slower)

```lua
SkillTree.Config.BaseStats.WalkSpeed = 150
SkillTree.Config.BaseStats.RunSpeed = 300
SkillTree.Config.BaseStats.JumpPower = 150
```

### Higher health pool

```lua
SkillTree.Config.BaseStats.MaxHealth = 150
SkillTree.Config.BaseStats.MaxArmor = 150
```
