# Medic Integration

Automated XP hooks and public API for medical jobs.

---

## How It Works

The medic integration hooks into healing events and provides a revive API.

## Hooks

### Heal XP

Grants XP proportional to the amount of HP healed:

```lua title="lua/skillforge/integrations/sv_darkrp_medic.lua"
hook.Add("SkillTree_PlayerHealed", "stn_medic_heal_xp", function(healer, target, amount)
    SkillTree.AddJobXPByAction(healer, "medic_heal", {
        targetSteamID64 = targetID,
        units = amount  -- XPPerHP * amount
    })
end)
```

---

## Public API

### Report Player Revived

Call this when a medic revives a downed player:

```lua
SkillTree.ReportPlayerRevived(healer, target)

-- Example with a custom defibrillator:
function DefibPlayer(medic, patient)
    patient:Spawn()
    SkillTree.ReportPlayerRevived(medic, patient)
end
```

---

## XP Actions

| Action ID | Description | XP Formula | Cooldown |
|-----------|-------------|------------|----------|
| `medic_heal` | Heal HP | 1 XP per HP healed | None (per-HP rate) |
| `medic_revive` | Revive player | 150 flat XP | 30s |

---

## Example: Custom Healing Integration

```lua
-- If you have a custom healing system, connect it like this:
function MyMedicSystem_HealPlayer(medic, patient, amount)
    patient:SetHealth(math.min(patient:Health() + amount, patient:GetMaxHealth()))

    -- Report to Skillforge
    hook.Run("SkillTree_PlayerHealed", medic, patient, amount)
end

function MyMedicSystem_RevivePlayer(medic, patient)
    -- Your revive logic
    SkillTree.ReportPlayerRevived(medic, patient)
end
```

---

## Related Configuration

```lua
SkillTree.Config.JobXP["Medic"] = {
    HealPlayer = {
        Enabled = true,
        XPPerHP = 1,
        MaxXPPerMinute = 250,
        PreventSelfFarm = true,
        Reason = "Healed player"
    },
    RevivePlayer = {
        Enabled = true,
        XP = 150,
        Cooldown = 45,
        Reason = "Revived player"
    }
}
```
