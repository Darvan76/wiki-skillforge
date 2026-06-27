# Achievements

Create custom achievements that reward players for reaching milestones.

---

## Configuration Table

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.Achievements = {
    { ID="first_level", Name="First Steps", Description="Reach level 2",
      Condition={Type="level", Value=2}, Rewards={XP=50} },
    { ID="level_10", Name="Getting Serious", Description="Reach level 10",
      Condition={Type="level", Value=10}, Rewards={XP=200, Points=1} }
}
```

---

## Achievement Fields

| Field | Type | Description |
|-------|------|-------------|
| `ID` | string | Unique identifier |
| `Name` | string | Display name |
| `Description` | string | Shown in the achievements panel |
| `Condition.Type` | string | Condition type (`level` currently) |
| `Condition.Value` | int | Target value to reach |
| `Rewards.XP` | int | XP awarded on completion |
| `Rewards.Points` | int | Skill points awarded on completion |

---

## Examples

### Level milestones

```lua
SkillTree.Config.Achievements = {
    { ID="first_level", Name="First Steps", Description="Reach level 2",
      Condition={Type="level", Value=2}, Rewards={XP=50} },
    { ID="level_10", Name="Getting Serious", Description="Reach level 10",
      Condition={Type="level", Value=10}, Rewards={XP=200, Points=1} },
    { ID="level_25", Name="Veteran", Description="Reach level 25",
      Condition={Type="level", Value=25}, Rewards={XP=500, Points=3} },
    { ID="level_50", Name="Elite", Description="Reach level 50",
      Condition={Type="level", Value=50}, Rewards={XP=1000, Points=5} },
    { ID="level_100", Name="Legend", Description="Reach the maximum level",
      Condition={Type="level", Value=100}, Rewards={XP=5000, Points=10} },
}
```

### Generous rewards

```lua
SkillTree.Config.Achievements = {
    { ID="level_5", Name="Apprentice", Description="Reach level 5",
      Condition={Type="level", Value=5}, Rewards={XP=100, Points=2} },
    { ID="level_20", Name="Expert", Description="Reach level 20",
      Condition={Type="level", Value=20}, Rewards={XP=500, Points=5} },
    { ID="level_50", Name="Master", Description="Reach level 50",
      Condition={Type="level", Value=50}, Rewards={XP=2000, Points=15} },
}
```
