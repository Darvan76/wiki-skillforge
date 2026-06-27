# XP Sources

Configure all the ways players can earn XP in your server.

---

## Configuration Table

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.XP = {
    Playtime = { Enabled = true, Amount = 10, Interval = 300 },
    PlayerKill = { Enabled = true, Amount = 50, Cooldown = 120, PreventFarmSamePlayer = true },
    NPCKill = { Enabled = true, Amount = 15, Cooldown = 5 },
    DarkRPMoneyEarned = { Enabled = true, XPPerMoney = 0.01, MaxXPPerMinute = 100 },
    Arrest = { Enabled = true, Amount = 40, Cooldown = 60 },
    Heal = { Enabled = true, Amount = 20, Cooldown = 30 },
    Sell = { Enabled = true, Amount = 25, Cooldown = 15 },
    JobFirstTime = { Enabled = true, Amount = 100 }
}
```

---

## Source Details

### Playtime

XP awarded periodically for being online.

| Parameter | Default | Description |
|-----------|---------|-------------|
| `Enabled` | `true` | Enable playtime XP |
| `Amount` | `10` | XP awarded per interval |
| `Interval` | `300` | Seconds between each award |

### Player Kill

XP for killing other players.

| Parameter | Default | Description |
|-----------|---------|-------------|
| `Enabled` | `true` | Enable kill XP |
| `Amount` | `50` | XP per kill |
| `Cooldown` | `120` | Seconds between kills (per player) |
| `PreventFarmSamePlayer` | `true` | Anti-farming cooldown per victim |

### NPC Kill

XP for killing NPCs.

| Parameter | Default | Description |
|-----------|---------|-------------|
| `Enabled` | `true` | Enable NPC kill XP |
| `Amount` | `15` | XP per NPC kill |
| `Cooldown` | `5` | Seconds between NPC kills |

### DarkRP Money

XP earned from gaining money in DarkRP.

| Parameter | Default | Description |
|-----------|---------|-------------|
| `Enabled` | `true` | Enable money XP |
| `XPPerMoney` | `0.01` | XP per dollar earned |
| `MaxXPPerMinute` | `100` | Maximum XP per minute from money |

### Arrest

XP for arresting players.

| Parameter | Default | Description |
|-----------|---------|-------------|
| `Enabled` | `true` | Enable arrest XP |
| `Amount` | `40` | XP per arrest |
| `Cooldown` | `60` | Seconds between arrest XP |

### Heal

XP for healing other players.

| Parameter | Default | Description |
|-----------|---------|-------------|
| `Enabled` | `true` | Enable heal XP |
| `Amount` | `20` | XP per heal action |
| `Cooldown` | `30` | Seconds between heal XP |

### Sell

XP for selling items to other players.

| Parameter | Default | Description |
|-----------|---------|-------------|
| `Enabled` | `true` | Enable sell XP |
| `Amount` | `25` | XP per sale |
| `Cooldown` | `15` | Seconds between sell XP |

### Job First Time

XP bonus for trying a job for the first time.

| Parameter | Default | Description |
|-----------|---------|-------------|
| `Enabled` | `true` | Enable first-time job XP |
| `Amount` | `100` | XP awarded once per job |

---

## Examples

### Disable NPC kill XP

```lua
SkillTree.Config.XP.NPCKill.Enabled = false
```

### More XP for arrests, less for kills

```lua
SkillTree.Config.XP.Arrest.Amount = 80
SkillTree.Config.XP.PlayerKill.Amount = 25
SkillTree.Config.XP.PlayerKill.Cooldown = 300
```

### Money grind server

```lua
SkillTree.Config.XP.DarkRPMoneyEarned.XPPerMoney = 0.05
SkillTree.Config.XP.DarkRPMoneyEarned.MaxXPPerMinute = 500
```

### Disable all passive XP

```lua
SkillTree.Config.XP.Playtime.Enabled = false
SkillTree.Config.XP.NPCKill.Enabled = false
```
