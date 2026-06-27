# Active Abilities

Active abilities are skills that players can manually activate with a cooldown.

---

## How They Work

1. Player unlocks an active ability node
2. The node must have `"type": "active"` in its definition
3. Player can activate it from the skill menu
4. The ability executes with the player's current rank's effect value
5. A cooldown is enforced before it can be used again

```lua title="lua/skillforge/sv_effects.lua"
function SkillTree.UseAbility(ply, skillID)
    local node = SkillTree.GetNode(treeID, skillID)
    if not node or not node.type or node.type ~= "active" then return end
    if not ply:STN_HasSkill(skillID) then return end

    local cooldown = node.cooldown or 10
    local lastUse = SkillTree.ActiveCooldowns[steamID][skillID] or 0
    if CurTime() - lastUse < cooldown then return end

    SkillTree.ActiveCooldowns[steamID][skillID] = CurTime()
    -- Execute effect based on effType
end
```

---

## Available Active Effects

### Dash

Propels the player forward at high speed.

```json
{
    "effectType": "Dash",
    "effectValue": [500, 600, 700],
    "type": "active",
    "cooldown": 15
}
```

### QuickHeal

Instantly restores health.

```json
{
    "effectType": "QuickHeal",
    "effectValue": [25, 50, 75],
    "type": "active",
    "cooldown": 30
}
```

### Shield

Creates a temporary damage-absorbing barrier.

```json
{
    "effectType": "Shield",
    "effectValue": [50, 100, 150],
    "type": "active",
    "cooldown": 30,
    "duration": 8
}
```

### Berserker

Temporary damage and speed boost.

```json
{
    "effectType": "Berserker",
    "effectValue": [1.3, 1.4, 1.5],
    "type": "active",
    "cooldown": 45,
    "duration": 6
}
```

### SpeedSurge

Temporary speed boost.

```json
{
    "effectType": "SpeedSurge",
    "effectValue": [1.5, 1.6, 1.7],
    "type": "active",
    "cooldown": 30,
    "duration": 10
}
```

### DoubleXP

Temporary XP multiplier.

```json
{
    "effectType": "DoubleXP",
    "effectValue": [2.0, 2.5, 3.0],
    "type": "active",
    "cooldown": 120,
    "duration": 60
}
```

---

## Complete Active Node Example

```json
{
    "berserker_rage": {
        "id": "berserker_rage",
        "name": "Berserker Rage",
        "description": "Enter a rage state, increasing damage and speed.",
        "branch": "combat",
        "gridX": 3,
        "gridY": 2,
        "icon": "../../materials/skilltree_nexus/icons/icon_combat.png",
        "color": "#ef4444",
        "maxRank": 3,
        "cost": [2, 3, 5],
        "requiredLevel": [20, 35, 50],
        "requires": ["combat_mastery"],
        "effectType": "Berserker",
        "effectValue": [1.3, 1.4, 1.5],
        "callback": "",
        "type": "active",
        "cooldown": 60,
        "duration": 8
    }
}
```

---

## Cooldown System

Active cooldowns are tracked per-player in `SkillTree.ActiveCooldowns`. When a player disconnects, their cooldowns are cleaned up:

```lua
hook.Add("PlayerDisconnected", "stn_net_cleanup_ratelimit", function(ply)
    SkillTree.ActiveCooldowns[steamID] = nil
end)
```

The cooldown is checked server-side to prevent abuse. The client cannot bypass cooldowns.
