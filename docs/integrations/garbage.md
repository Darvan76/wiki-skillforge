# Garbage Integration

Public API for Garbage Collector jobs.

---

## How It Works

The garbage integration provides APIs for collecting, recycling, and delivering garbage.

---

## Public API

### Report Garbage Collected

Call this when a player collects garbage (weight in kg):

```lua
SkillTree.ReportGarbageCollected(ply, kg)

-- Example:
function CollectGarbage(ply, weight)
    -- Your garbage collection logic
    ply:addMoney(weight * 5)
    SkillTree.ReportGarbageCollected(ply, weight)
end
```

### Report Garbage Recycled

Call this when a player recycles garbage:

```lua
SkillTree.ReportGarbageRecycled(ply, kg)

-- Example:
function RecycleGarbage(ply, weight)
    -- Your recycling logic
    ply:addMoney(weight * 8)
    SkillTree.ReportGarbageRecycled(ply, weight)
end
```

### Report Garbage Delivered

Call this when a player delivers a garbage bag:

```lua
SkillTree.ReportGarbageDelivered(ply, bagWeight)

-- Example:
function DeliverBag(ply, bag)
    -- Your delivery logic
    ply:addMoney(50)
    SkillTree.ReportGarbageDelivered(ply, bag.weight)
end
```

### Report Route Completed

Call this when a player completes a garbage collection route:

```lua
SkillTree.ReportGarbageRouteCompleted(ply, routeID)

-- Example:
function CompleteRoute(ply, route)
    -- Your route logic
    ply:addMoney(200)
    SkillTree.ReportGarbageRouteCompleted(ply, route.id)
end
```

---

## XP Actions

| Action ID | Description | XP Formula | Cooldown |
|-----------|-------------|------------|----------|
| `garbage_collected` | Collect garbage | 5 XP per kg | None (per-kg rate) |
| `garbage_recycled` | Recycle garbage | 10 XP per kg | None (per-kg rate) |
| `garbage_bag_delivered` | Deliver bag | 50 flat XP | 3s |
| `garbage_route_completed` | Complete route | 200 flat XP | 120s |

---

## Related Configuration

```lua
SkillTree.Config.JobXP["Garbage Collector"] = {
    GarbageCollectedPerKG = { Enabled = true, XPPerKG = 5, MaxXPPerMinute = 200 },
    GarbageRecycledPerKG = { Enabled = true, XPPerKG = 10, MaxXPPerMinute = 300 },
    GarbageBagDelivered = { Enabled = true, XP = 50, Cooldown = 5 },
    GarbageRouteCompleted = { Enabled = true, XP = 200, Cooldown = 300 }
}
```
