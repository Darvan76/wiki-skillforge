# Police Integration

Automated XP hooks and public API for police jobs.

---

## How It Works

The police integration hooks into DarkRP's arrest system and provides public APIs for weapon and contraband confiscation.

## Hooks

### Arrest XP

Grants XP when a player arrests another player, with bonus XP for arresting wanted criminals:

```lua title="lua/skillforge/integrations/sv_darkrp_police.lua"
hook.Add("playerArrested", "stn_police_arrest_xp", function(criminal, time, arrester)
    local wanted = criminal:isWanted and criminal:isWanted() or false
    if wanted then
        SkillTree.AddJobXPByAction(arrester, "police_arrest_wanted", { targetSteamID64 = targetID })
    else
        SkillTree.AddJobXPByAction(arrester, "police_arrest", { targetSteamID64 = targetID })
    end
end)
```

---

## Public API

### Report Weapon Confiscated

Call this when a weapon is confiscated from a player:

```lua
SkillTree.ReportWeaponConfiscated(ply, target, weaponClass)

-- Example usage:
hook.Add("MyStripWeaponEvent", "PoliceXP", function(ply, target, weapon)
    SkillTree.ReportWeaponConfiscated(ply, target, weapon)
end)
```

### Report Illegal Entity Confiscated

Call this when contraband (drugs, illegal entities) is confiscated:

```lua
SkillTree.ReportIllegalEntityConfiscated(ply, ent)

-- Example usage:
function ConfiscateEntity(ply, ent)
    -- Your confiscation logic
    ent:Remove()
    SkillTree.ReportIllegalEntityConfiscated(ply, ent)
end
```

---

## XP Actions

| Action ID | Description | Default XP | Cooldown |
|-----------|-------------|------------|----------|
| `police_arrest` | Arrest a player | 100 | 15s |
| `police_arrest_wanted` | Arrest a wanted player | 150 | 30s |
| `police_confiscate_weapon` | Confiscate a weapon | 20 | 5s |
| `police_confiscate_illegal` | Confiscate contraband | 30 | 5s |

---

## Example: Custom Confiscation Tool

```lua
-- Add this to a custom confiscation weapon/addon
function CustomTool_Confiscate(ply, target)
    -- Your confiscation logic
    for _, weapon in ipairs(target:GetWeapons()) do
        target:StripWeapon(weapon:GetClass())
        SkillTree.ReportWeaponConfiscated(ply, target, weapon:GetClass())
    end
end
```

---

## Related Configuration

```lua
SkillTree.Config.JobXP["Civil Protection"] = {
    ArrestPlayer = { Enabled = true, XP = 100, Cooldown = 30 },
    ArrestWantedPlayer = { Enabled = true, XP = 150, Cooldown = 60 },
    ConfiscateWeapon = { Enabled = true, XP = 20, Cooldown = 10 },
    ConfiscateIllegalEntity = { Enabled = true, XP = 30, Cooldown = 10 }
}
```
