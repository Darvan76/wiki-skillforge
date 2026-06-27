# Configuration Overview

Skillforge offers **~150+ configurable parameters** organized into logical sections. All configuration lives under `SkillTree.Config` in `lua/skillforge/sh_config.lua`.

---

## Quick Reference

| Section | Key Table | Purpose | Variables |
|---------|-----------|---------|-----------|
| [General](general.md) | `SkillTree.Config.General` | Core behavior | 9 |
| [Theme](theme.md) | `SkillTree.Config.Theme` | Visual appearance | 9 |
| [Leveling](leveling.md) | `SkillTree.Config.Leveling` | XP & level formulas | 4 |
| [XP Sources](xp-sources.md) | `SkillTree.Config.XP` | XP gain sources | 7 (sub-tables) |
| [Anti-Exploit](anti-exploit.md) | `SkillTree.Config.AntiExploit` | Abuse prevention | 4 |
| [Stat Limits](limits.md) | `SkillTree.Config.Limits` | Max multipliers | 7 |
| [Reset System](reset-system.md) | `SkillTree.Config.Reset` | Skill reset settings | 5 |
| [Prestige](prestige.md) | `SkillTree.Config.Prestige` | Prestige mechanics | 4 |
| [Dailies](dailies.md) | `SkillTree.Config.Dailies` | Daily missions | 3 |
| [Achievements](achievements.md) | `SkillTree.Config.Achievements` | Achievement definitions | Array |
| [Base Stats](base-stats.md) | `SkillTree.Config.BaseStats` | Base movement/health | 5 |

---

## How to Configure

### Method 1: Direct config edit

Edit `lua/skillforge/sh_config.lua` directly on the server.

```lua
-- Before loading, override any default
SkillTree.Config.General.MaxLevel = 50
SkillTree.Config.Leveling.GrowthMultiplier = 1.10
```

### Method 2: Autorun file (recommended)

Create an autorun file that runs **after** Skillforge loads:

```lua title="lua/autorun/skillforge_config_override.lua"
local function SetupConfig()
    -- Wait for SkillTree to be available
    if not SkillTree or not SkillTree.Config then
        timer.Simple(1, SetupConfig)
        return
    end

    SkillTree.Config.General.MaxLevel = 150
    SkillTree.Config.General.OpenCommand = "!arbol"
    SkillTree.Config.Theme.PrimaryColor = Color(255, 100, 50)
    SkillTree.Config.XP.Arrest.Amount = 60
    SkillTree.Config.AntiExploit.MaxXPPerMinute = 800
    SkillTree.Config.Reset.CostMoney = 100000
end
SetupConfig()
```

!!! tip "Autorun is safer"
    Using an autorun file makes updates easier — your custom config survives addon reinstallation.

---

## Configuration Hierarchy

```
SkillTree.Config
├── General           → Core settings (command, key, max level, debug)
├── Theme             → Colors, animations, sounds
├── Leveling          → XP formula: BaseXP * GrowthMultiplier^(n-1)
├── XP                → Individual XP sources with cooldowns
├── AntiExploit       → Rate limits and security
├── Limits            → Hard caps on multipliers
├── Reset             → Skill reset cost and cooldowns
├── Prestige          → Prestige system (overlay)
├── Dailies           → Daily mission system
├── Achievements      → Achievement definitions
├── Admin             → Admin rank whitelist
├── BaseStats         → Base walk/run/jump/health/armor
├── ActiveTrees       → Job → Tree mappings (legacy)
├── JobSkills         → Per-job skill restrictions
├── JobProgression    → Global / Separate / Hybrid mode
├── JobTrees          → TEAM-based mapping
├── JobTreesByName    → Name-based mapping
├── JobTreesByCategory → Category-based mapping
├── JobXP             → Per-job XP configuration
└── Language          → Locale selection
```

## Related sections

- [Job System → Progression Modes](../job-system/progression-modes.md)
- [Job System → Job XP Config](../job-system/job-xp-config.md)
- [Player Experience → HUD](../player-experience/hud.md)
- [Player Experience → Level-Up FX](../player-experience/level-up-fx.md)
