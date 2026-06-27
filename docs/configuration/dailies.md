# Daily Missions

Configure daily missions to keep players engaged.

---

## Configuration Table

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.Dailies = {
    ResetHour = 0,
    MissionsPerDay = 3,
    MissionPool = {
        { ID="kill_10_npcs", Type="kill_npcs", Target=10, Name="Hunter", Description="Eliminate 10 NPCs", Rewards={XP=200, Points=1} },
        { ID="play_60_mins", Type="play_time", Target=60, Name="Dedication", Description="Play for 60 minutes", Rewards={XP=300, Points=1} },
        { ID="earn_5000", Type="earn_money", Target=5000, Name="Entrepreneur", Description="Earn $5000", Rewards={XP=150, Points=0} }
    }
}
```

---

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `ResetHour` | int | `0` | Hour of day (UTC) to reset missions |
| `MissionsPerDay` | int | `3` | Number of missions assigned per day |
| `MissionPool` | array | 3 missions | Available mission definitions |

### Mission Fields

| Field | Type | Description |
|-------|------|-------------|
| `ID` | string | Unique identifier |
| `Type` | string | Mission type (`kill_npcs`, `play_time`, `earn_money`) |
| `Target` | int | Quantity to complete |
| `Name` | string | Display name |
| `Description` | string | Description shown to player |
| `Rewards.XP` | int | XP awarded on completion |
| `Rewards.Points` | int | Skill points awarded on completion |

---

## Examples

### Custom missions

```lua
SkillTree.Config.Dailies.MissionPool = {
    { ID="arrest_5", Type="arrest", Target=5, Name="Law Enforcer",
      Description="Arrest 5 criminals", Rewards={XP=500, Points=2} },
    { ID="heal_20", Type="heal", Target=20, Name="Field Medic",
      Description="Heal 20 HP worth of damage", Rewards={XP=300, Points=1} },
    { ID="steal_3_printers", Type="steal_printers", Target=3, Name="Printer Thief",
      Description="Steal 3 money printers", Rewards={XP=400, Points=1} },
    { ID="sell_10_weapons", Type="sell_weapons", Target=10, Name="Arms Dealer",
      Description="Sell 10 weapons", Rewards={XP=350, Points=1} },
    { ID="earn_10k", Type="earn_money", Target=10000, Name="Tycoon",
      Description="Earn $10,000", Rewards={XP=200, Points=1} },
}
```

### Reset at midnight UTC

```lua
SkillTree.Config.Dailies.ResetHour = 0
```

### Reset at 6 AM server time

```lua
SkillTree.Config.Dailies.ResetHour = 6
```

### More missions per day

```lua
SkillTree.Config.Dailies.MissionsPerDay = 5
```
