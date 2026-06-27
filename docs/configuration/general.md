# General Settings

Controls the core behavior of the addon.

---

## Configuration Table

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.General = {
    OpenCommand = "!skills",
    OpenKey = KEY_F6,
    MaxLevel = 100,
    EnableDarkRP = true,
    EnableHUD = true,
    EnableAdminPanel = true,
    EnableDailies = true,
    EnableAchievements = true,
    SaveInterval = 300,
    DefaultSkillPoints = 0,
    SkillPointsPerLevel = 1,
    Debug = false
}
```

---

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `OpenCommand` | string | `"!skills"` | Chat command to open the skill menu |
| `OpenKey` | constant | `KEY_F6` | Keyboard key to toggle the menu |
| `MaxLevel` | int | `100` | Maximum achievable level |
| `EnableDarkRP` | bool | `true` | Enable DarkRP integration hooks |
| `EnableHUD` | bool | `true` | Show the on-screen HUD |
| `EnableAdminPanel` | bool | `true` | Enable the HTML admin panel |
| `EnableDailies` | bool | `true` | Enable daily mission system |
| `EnableAchievements` | bool | `true` | Enable achievement system |
| `SaveInterval` | int | `300` | Auto-save interval in seconds |
| `DefaultSkillPoints` | int | `0` | Skill points given to new players |
| `SkillPointsPerLevel` | int | `1` | Base skill points earned per level |
| `Debug` | bool | `false` | Enable debug logging |

---

## Examples

### Custom command and key

```lua
SkillTree.Config.General.OpenCommand = "!arbol"
SkillTree.Config.General.OpenKey = KEY_F5
```

### Disable HUD but keep everything else

```lua
SkillTree.Config.General.EnableHUD = false
```

### Faster auto-save

```lua
SkillTree.Config.General.SaveInterval = 60  -- Save every 60 seconds
```

### Start new players with 5 skill points

```lua
SkillTree.Config.General.DefaultSkillPoints = 5
```
