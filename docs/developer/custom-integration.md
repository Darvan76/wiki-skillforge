# Custom Integration

A complete guide to creating a custom job integration from scratch.

---

## Integration File Structure

Create a file at `lua/skillforge/integrations/sv_mymod_integration.lua`. It's loaded automatically.

```lua title="lua/skillforge/integrations/sv_mymod_integration.lua"
--[[
    SkillTree Nexus - My Custom Mod Integration
    Provides XP for custom job actions.
]]

if not DarkRP then return end

-- Register XP actions
hook.Add("Initialize", "stn_mymod_actions", function()
    SkillTree.RegisterJobXPAction("mymod_do_thing", {
        name = "Did a Thing",
        defaultXP = 50,
        cooldown = 10,
        jobWhitelist = {"My Custom Job"}
    })
end)

-- Hook custom events
hook.Add("MyCustomMod_ThingDone", "stn_mymod_xp", function(ply)
    SkillTree.AddJobXPByAction(ply, "mymod_do_thing")
end)

-- Public API
function SkillTree.ReportMyModThingDone(ply)
    SkillTree.AddJobXPByAction(ply, "mymod_do_thing")
end
```

---

## Step-by-Step

### 1. Create the File

```
lua/skillforge/integrations/sv_mymod_integration.lua
```

### 2. Add Safety Check

```lua
if not DarkRP then return end
```

### 3. Register Actions

```lua
hook.Add("Initialize", "stn_mymod_actions", function()
    SkillTree.RegisterJobXPAction("mymod_my_action", {
        name = "My Action",
        defaultXP = 100,
        cooldown = 30,
        jobWhitelist = {"My Job"}
    })
end)
```

### 4. Hook Your Events

```lua
hook.Add("YourMod_Event", "stn_mymod_xp", function(ply, ...)
    SkillTree.AddJobXPByAction(ply, "mymod_my_action", {
        -- optional metadata
    })
end)
```

### 5. Expose Public API

```lua
function SkillTree.ReportMyAction(ply, ...)
    SkillTree.AddJobXPByAction(ply, "mymod_my_action", { ... })
end
```

---

## Full Example

```lua title="lua/skillforge/integrations/sv_lumberjack.lua"
--[[
    SkillTree Nexus - Lumberjack Integration
    Custom job: Lumberjack
]]

if not DarkRP then return end

-- Register actions
hook.Add("Initialize", "stn_lumberjack_actions", function()
    SkillTree.RegisterJobXPAction("lumberjack_chop_tree", {
        name = "Tree Chopped",
        defaultXP = 30,
        cooldown = 10,
        jobWhitelist = {"Lumberjack"}
    })
    SkillTree.RegisterJobXPAction("lumberjack_sell_wood", {
        name = "Wood Sold",
        defaultXP = 60,
        cooldown = 20,
        jobWhitelist = {"Lumberjack"}
    })
end)

-- Public API
function SkillTree.ReportTreeChopped(ply)
    SkillTree.AddJobXPByAction(ply, "lumberjack_chop_tree")
end

function SkillTree.ReportWoodSold(ply)
    SkillTree.AddJobXPByAction(ply, "lumberjack_sell_wood")
end
```

Then configure the job:

```lua
SkillTree.Config.JobTreesByName["Lumberjack"] = "lumberjack_tree"
SkillTree.Config.JobXP["Lumberjack"] = {
    ChopTree = { Enabled = true, XP = 30, Cooldown = 10 },
    SellWood = { Enabled = true, XP = 60, Cooldown = 20 }
}
```

---

## Job XP Configuration Integration

Add the job to `SkillTree.Config.JobXP`:

```lua
SkillTree.Config.JobXP["My Custom Job"] = {
    MyAction = {
        Enabled = true,
        XP = 100,
        Cooldown = 30,
        MaxXPPerMinute = 300,
        Reason = "Performed custom action"
    }
}
```
