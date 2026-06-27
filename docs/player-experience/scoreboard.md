# Scoreboard Integration

Skillforge extends the DarkRP scoreboard to display level information.

---

## How It Works

The scoreboard integration uses `vgui.Register` monkey-patching to extend the existing scoreboard without replacing it:

```lua title="lua/skillforge/cl_scoreboard.lua"
-- Patches the existing scoreboard to add level display
-- Uses vgui.Register to extend the default scoreboard rows
```

---

## What It Shows

Each player row on the scoreboard now displays:

```
[Player Name]            Level 23
[Job Name]               [Skill Points: 5]
```

---

## Configuration

There is no separate configuration for the scoreboard. It's enabled by default and uses the player's current level and skill points from the NW variables:

```lua
ply:SetNWInt("stn_level", data.level)
ply:SetNWInt("stn_points", data.skill_points)
```

---

## Disabling Scoreboard Integration

To remove the level display from the scoreboard:

```lua
-- In your server's autorun:
hook.Add("Initialize", "DisableScoreboard", function()
    -- The scoreboard patch is in cl_scoreboard.lua
    -- Remove or rename that file to disable it
end)
```
