# Allowed Skills

Restrict which skills each job can unlock.

---

## Configuration Table

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.JobSkills = {
    ["Citizen"] = { AllowedSkills = SkillTree.Config.DefaultRPGSkillIDs },
    ["Civil Protection"] = { AllowedSkills = SkillTree.Config.DefaultRPGSkillIDs },
    ["Gangster"] = { AllowedSkills = SkillTree.Config.DefaultRPGSkillIDs },
    ["Medic"] = { AllowedSkills = SkillTree.Config.DefaultRPGSkillIDs },
    ["Cook"] = { AllowedSkills = SkillTree.Config.DefaultRPGSkillIDs },
    ["Mayor"] = { AllowedSkills = SkillTree.Config.DefaultRPGSkillIDs }
}
```

---

## How It Works

When a player tries to unlock a skill, the system checks:

```lua title="lua/skillforge/sv_darkrp.lua"
function SkillTree.DarkRP.CanUseSkill(ply, skillID)
    local jobName = team.GetName(ply:Team())
    local jobConfig = SkillTree.Config.JobSkills[jobName]
    if not jobConfig then return true end
    if not jobConfig.AllowedSkills then return true end
    return table.HasValue(jobConfig.AllowedSkills, skillID)
end
```

If a job has no entry in `JobSkills`, all skills are allowed.

---

## Default Allowed Skills

The default `DefaultRPGSkillIDs` includes all skill IDs from:
- The RPG core tree (48 skills across 8 branches)
- Job-specific trees (police, medic, criminal, garbage, economy)

```lua
SkillTree.Config.DefaultRPGSkillIDs = {
    "combat_training", "sidearm_drills", "rifle_control",
    "iron_body", "armor_fitting", "spawn_plating",
    "urban_runner", "sprint_training", "parkour_basics",
    "street_sense", "quiet_approach",
    "tech_literacy", "scanner_mind", "printer_tuning",
    "side_hustle", "salary_negotiation", "market_eye",
    -- ... 48+ total
}
```

---

## Examples

### Medic-only skills

```lua
SkillTree.Config.JobSkills["Medic"] = {
    AllowedSkills = {
        "medic_rookie", "defib_expert",
        "passive_regen", "quick_heal",
        "heal_boost", "revive_speed"
    }
}
```

### Police-only skills with shared RPG core

```lua
SkillTree.Config.JobSkills["Civil Protection"] = {
    AllowedSkills = {
        "police_training", "efficient_arrest", "wanted_hunter",
        "crime_scene", "forensic_eye",
        "riot_gear", "bullet_resist", "shock_absorption",
        "tactical_response", "city_runner"
    }
}
```

### Block all skills for a job

```lua
SkillTree.Config.JobSkills["Mayor"] = {
    AllowedSkills = {}
}
```

### Allow all skills (default behavior)

Just omit the job from `JobSkills` or don't set `AllowedSkills`:

```lua
SkillTree.Config.JobSkills["Citizen"] = {} -- All skills allowed
```
