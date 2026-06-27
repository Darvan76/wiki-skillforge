# Examples

15 complete, copy-paste ready examples for common tasks.

---

## 1. Create a Custom Tree via Script

```lua
local treeData = {
    id = "my_server_tree",
    name = "My Server Tree",
    description = "A custom tree for my server",
    author = "Me",
    version = "1.0.0",
    branches = {
        core = {
            id = "core", name = "Core", description = "Core skills",
            color = "#7850ff", icon = "icon_combat.png"
        }
    },
    nodes = {
        speed_boost = {
            id = "speed_boost", name = "Speed Boost",
            description = "Increases movement speed",
            branch = "core", gridX = 0, gridY = 0,
            icon = "icon_runner.png", color = "#7850ff",
            maxRank = 5, cost = {1, 1, 2, 2, 3},
            requiredLevel = {1, 5, 10, 15, 20},
            requires = {},
            effectType = "WalkSpeedMultiplier",
            effectValue = {1.03, 1.06, 1.09, 1.12, 1.15}
        }
    }
}
SkillTree.SaveTree("my_server_tree", treeData)
```

---

## 2. Map a Job to a Tree

```lua
-- By name (recommended)
SkillTree.Config.JobTreesByName["Police Officer"] = "police_tree"

-- By TEAM enum
SkillTree.Config.JobTrees[TEAM_POLICE] = "police_tree"

-- By DarkRP category
SkillTree.Config.JobTreesByCategory["Government"] = "police_tree"

-- By custom callback
SkillTree.Config.JobTreesCallback = function(ply)
    if ply:Team() == TEAM_POLICE then return "police_tree" end
    return nil
end
```

---

## 3. Change Progression Mode

```lua
-- Global: shared level/points across all jobs
SkillTree.Config.JobProgression.Mode = "global"

-- Separate: each job has its own level/XP/points
SkillTree.Config.JobProgression.Mode = "separate"

-- Hybrid: global level, per-job XP
SkillTree.Config.JobProgression.Mode = "hybrid"
```

---

## 4. Register a Custom Job XP Action

```lua
SkillTree.RegisterJobXPAction("my_custom_action", {
    name = "Custom Action",
    defaultXP = 50,
    xpPerUnit = 5,
    unitName = "unit",
    cooldown = 30,
    maxXPPerMinute = 300,
    jobWhitelist = {"My Job"}
})
```

---

## 5. Give XP from a Third-Party Addon

```lua
-- Hook into a custom event
hook.Add("MyAddon_Event", "MyAddon_XP", function(ply, ...)
    SkillTree.AddJobXPByAction(ply, "my_custom_action")
end)

-- Or give raw XP
hook.Add("MyAddon_QuestComplete", "MyAddon_XP", function(ply)
    SkillTree.AddXP(ply, 200, "Quest completed!")
end)
```

---

## 6. Hook Player Level-Up

```lua
hook.Add("SkillTree_PlayerLeveledUp", "MyServer_LevelUp", function(ply, newLevel)
    ply:ChatPrint("Congratulations on reaching level " .. newLevel .. "!")
    if newLevel % 10 == 0 then
        ply:addMoney(1000)  -- Bonus $1000 every 10 levels
    end
end)
```

---

## 7. Register a Callback for a Custom Effect

```lua
SkillTree.RegisterCallback("My_HealthBonus", function(ply, treeID, skillID, rank, skillData)
    local value = skillData.effectValue and skillData.effectValue[rank] or 0
    ply:SetHealth(math.min(ply:Health() + value, ply:GetMaxHealth()))
end)
```

Then in the tree JSON:
```json
{
    "health_node": {
        "callback": "My_HealthBonus",
        "effectValue": [10, 20, 30]
    }
}
```

---

## 8. Restrict Skills by Job

```lua
SkillTree.Config.JobSkills["Medic"] = {
    AllowedSkills = {"medic_rookie", "defib_expert", "passive_regen"}
}
```

---

## 9. Custom Stat Limits

```lua
SkillTree.Config.Limits.MaxDamageMultiplier = 1.50  -- 50% max damage
SkillTree.Config.Limits.MaxWalkSpeedMultiplier = 1.50  -- 50% max speed
SkillTree.Config.Limits.MaxDamageResistance = 0.50  -- 50% max resistance
```

---

## 10. Custom Anti-Exploit

```lua
SkillTree.Config.AntiExploit.MaxXPPerMinute = 1000
SkillTree.Config.AntiExploit.AFKTimeout = 600  -- 10 minutes
SkillTree.Config.AntiExploit.SameTargetCooldown = 600  -- 10 minutes
```

---

## 11. Custom XP Formula

```lua
-- Faster progression
SkillTree.Config.Leveling.BaseXP = 50
SkillTree.Config.Leveling.GrowthMultiplier = 1.10

-- Slower, more grindy
SkillTree.Config.Leveling.BaseXP = 200
SkillTree.Config.Leveling.GrowthMultiplier = 1.20

-- More skill points per level
SkillTree.Config.Leveling.SkillPointsPerLevel = 2
```

---

## 12. Configure Prestige

```lua
SkillTree.Config.Prestige.MaxPrestige = 5
SkillTree.Config.Prestige.BonusSkillPoints = 5
SkillTree.Config.Prestige.XPMultiplierPerPrestige = 0.05  -- 5% per prestige
```

---

## 13. Expensive Reset

```lua
SkillTree.Config.Reset.CostMoney = 100000
SkillTree.Config.Reset.Cooldown = 604800  -- 1 week
SkillTree.Config.Reset.RefundPercentage = 50  -- Only 50% refund
```

---

## 14. Custom Integration - Bank Robbery

```lua
-- In your bank robbery addon:
function BankRobbery_Complete(ply)
    local stolen = 5000
    ply:addMoney(stolen)

    -- Report to Skillforge
    if SkillTree and SkillTree.ReportRobberyCompleted then
        SkillTree.ReportRobberyCompleted(ply, stolen)
    end
end
```

---

## 15. Complete Server Setup

```lua title="lua/autorun/skillforge_server_setup.lua"
local function Setup()
    if not SkillTree then timer.Simple(1, Setup) return end

    -- Progression: separate per job
    SkillTree.Config.JobProgression.Mode = "separate"

    -- Custom XP formula
    SkillTree.Config.Leveling.BaseXP = 80
    SkillTree.Config.Leveling.GrowthMultiplier = 1.12
    SkillTree.Config.Leveling.SkillPointsPerLevel = 2

    -- XP sources
    SkillTree.Config.XP.Playtime.Interval = 120
    SkillTree.Config.XP.Arrest.Amount = 60
    SkillTree.Config.XP.PlayerKill.Amount = 30

    -- Anti-exploit
    SkillTree.Config.AntiExploit.MaxXPPerMinute = 800

    -- Limits
    SkillTree.Config.Limits.MaxDamageMultiplier = 1.30
    SkillTree.Config.Limits.MaxWalkSpeedMultiplier = 1.35

    -- Theme - server branding
    SkillTree.Config.Theme.PrimaryColor = Color(0, 180, 100)
    SkillTree.Config.Theme.SecondaryColor = Color(0, 220, 150)

    -- Language
    SkillTree.Config.Language = "en"

    -- Custom achievements
    SkillTree.Config.Achievements = {
        { ID="level_5", Name="Apprentice", Description="Reach level 5",
          Condition={Type="level", Value=5}, Rewards={XP=100, Points=2} },
        { ID="level_25", Name="Veteran", Description="Reach level 25",
          Condition={Type="level", Value=25}, Rewards={XP=500, Points=5} },
        { ID="level_50", Name="Master", Description="Reach level 50",
          Condition={Type="level", Value=50}, Rewards={XP=2000, Points=15} },
    }
end
Setup()
```
