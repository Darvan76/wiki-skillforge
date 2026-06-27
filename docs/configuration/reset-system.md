# Reset System

Configure how players can reset their skill trees.

---

## Configuration Table

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.Reset = {
    Enabled = true,
    CostMoney = 50000,
    Cooldown = 86400,
    RefundPercentage = 100,
    AllowPartialReset = true
}
```

---

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `Enabled` | bool | `true` | Enable the reset system |
| `CostMoney` | int | `50000` | DarkRP money cost to reset |
| `Cooldown` | int | `86400` | Cooldown in seconds (24h) |
| `RefundPercentage` | int | `100` | Percentage of points refunded |
| `AllowPartialReset` | bool | `true` | Allow resetting individual branches |

---

## How Reset Works

1. Player clicks **Reset Skills** in the menu
2. System checks cooldown (`24h` default)
3. System checks money (`$50,000` default)
4. All skill points spent are calculated
5. Refund is applied (`100%` by default)
6. Skills are cleared, points are returned
7. Effects are re-applied (all passives removed)

```lua title="lua/skillforge/sv_core.lua"
-- Refund calculation
for skillID, rank in pairs(data.skills) do
    local node = tree.nodes[skillID]
    if node and node.cost then
        for i = 1, rank do
            refundedPoints = refundedPoints + (node.cost[i] or 0)
        end
    end
end
local refundPercent = (SkillTree.Config.Reset.RefundPercentage or 100) / 100
refundedPoints = math.floor(refundedPoints * refundPercent)
```

---

## Examples

### Free reset (no cost, no cooldown)

```lua
SkillTree.Config.Reset.CostMoney = 0
SkillTree.Config.Reset.Cooldown = 0
```

### Expensive premium reset

```lua
SkillTree.Config.Reset.CostMoney = 200000
SkillTree.Config.Reset.Cooldown = 604800  -- 1 week
SkillTree.Config.Reset.RefundPercentage = 50
```

### Disable partial reset

```lua
SkillTree.Config.Reset.AllowPartialReset = false
```
