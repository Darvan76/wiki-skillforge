# Job-Tree Mapping

Skillforge provides **4 ways** to map DarkRP jobs to skill trees, resolved in a specific priority order.

---

## Resolution Order

```lua title="lua/skillforge/sh_effect_types.lua"
function SkillTree.GetActiveTreeForPlayer(ply)
    -- 1. Custom Hook override
    local hookTree = hook.Run("SkillTree_GetPlayerTree", ply)
    if hookTree then return hookTree end

    -- 2. Custom callback in config
    if SkillTree.Config.JobTreesCallback then
        local tree = SkillTree.Config.JobTreesCallback(ply)
        if tree then return tree end
    end

    -- 3. TEAM enum mapping
    if SkillTree.Config.JobTrees[teamID] then
        return SkillTree.Config.JobTrees[teamID]
    end

    -- 4. Job Name mapping
    if SkillTree.Config.JobTreesByName[jobName] then
        return SkillTree.Config.JobTreesByName[jobName]
    end

    -- 5. Category mapping
    if SkillTree.Config.JobTreesByCategory[category] then
        return SkillTree.Config.JobTreesByCategory[category]
    end

    -- 6. UserGroup mapping
    if cfg.ByUserGroup[ply:GetUserGroup()] then
        return cfg.ByUserGroup[ply:GetUserGroup()]
    end

    -- 7. Default fallback
    return cfg.Default or "darkrp_default"
end
```

---

## Method 1: By Job Name (Recommended)

```lua title="lua/skillforge/shared/sh_job_config.lua"
SkillTree.Config.JobTreesByName = {
    ["Civil Protection"] = "police_tree",
    ["Police Chief"] = "police_tree",
    ["Medic"] = "medic_tree",
    ["Garbage Collector"] = "garbage_tree",
    ["Mob Boss"] = "criminal_tree",
    ["Thief"] = "criminal_tree",
    ["Citizen"] = "citizen_tree",
    ["Gun Dealer"] = "gun_dealer_tree",
    ["Cook"] = "cook_tree"
}
```

---

## Method 2: By TEAM Enum

```lua
SkillTree.Config.JobTrees = {
    [TEAM_POLICE] = "police_tree",
    [TEAM_MEDIC] = "medic_tree",
    [TEAM_GUN] = "gun_dealer_tree",
}
```

---

## Method 3: By DarkRP Category

```lua
SkillTree.Config.JobTreesByCategory = {
    ["Government"] = "police_tree",
    ["Criminals"] = "criminal_tree",
    ["Citizens"] = "citizen_tree"
}
```

---

## Method 4: Custom Hook/Callback

### Using the config callback

```lua
SkillTree.Config.JobTreesCallback = function(ply)
    -- Custom logic based on faction, level, etc.
    local faction = ply:GetNWString("faction", "")
    if faction == "Law" then return "police_tree" end
    if faction == "Underworld" then return "criminal_tree" end
    return nil -- Fallback to other mappings
end
```

### Using the hook

```lua
hook.Add("SkillTree_GetPlayerTree", "MyServer_JobTree", function(ply)
    if ply:Team() == TEAM_POLICE then return "police_tree" end
    return nil
end)
```

---

## Legacy Mapping (ActiveTrees)

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.ActiveTrees = {
    Default = "darkrp_default",
    ByJob = {
        ["Citizen"] = "citizen_tree",
        ["Police Officer"] = "police_tree",
    },
    ByUserGroup = {
        ["vip"] = "vip_tree",
        ["superadmin"] = "admin_tree"
    }
}
```

!!! warning "Legacy compatibility"
    `ActiveTrees` is kept for backwards compatibility. New configurations should use `JobTreesByName`, `JobTrees`, or `JobTreesByCategory`.

---

## Server-Side Safety

If a mapped tree doesn't exist on disk, the system falls back:

1. The mapped tree ID → check if it exists
2. If not → try the default tree
3. If default doesn't exist → use the first available tree

```lua
if not SkillTree.Trees[activeTree] then
    if SkillTree.Trees[fallback] then
        activeTree = fallback
    else
        activeTree = next(SkillTree.Trees) -- First available
    end
end
```
