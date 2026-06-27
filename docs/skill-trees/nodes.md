# Nodes

Nodes are the individual skills within a tree. Each node can have multiple ranks, costs, requirements, and effects.

---

## Node Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | string | ✅ | Unique node identifier (snake_case) |
| `name` | string | ✅ | Display name |
| `description` | string | ✅ | Tooltip description |
| `branch` | string | ✅ | Branch ID this node belongs to |
| `gridX` | int | ✅ | Grid column position |
| `gridY` | int | ✅ | Grid row position |
| `x` | int | ✅ | Pixel X coordinate (auto-calc from gridX * 140) |
| `y` | int | ✅ | Pixel Y coordinate (auto-calc from gridY * 140) |
| `icon` | string | ✅ | Icon path |
| `color` | string | ✅ | Hex color |
| `maxRank` | int | ✅ | Maximum upgrade rank |
| `cost` | array | ✅ | Skill point cost per rank |
| `requiredLevel` | array | ✅ | Required player level per rank |
| `requires` | array | ❌ | Prerequisite node IDs |
| `effectType` | string | ❌ | Effect type identifier |
| `effectValue` | array | ❌ | Effect value per rank |
| `callback` | string | ❌ | Developer callback name |
| `type` | string | ❌ | `"active"` for active abilities |
| `cooldown` | int | ❌ | Active ability cooldown (seconds) |
| `duration` | int | ❌ | Active ability duration (seconds) |

---

## Example Node

```json
{
    "police_training": {
        "id": "police_training",
        "name": "Police Training",
        "description": "Basic training that increases XP gained from arresting criminals.",
        "branch": "arrests",
        "gridX": 0,
        "gridY": 1,
        "x": 0,
        "y": 140,
        "icon": "../../materials/skilltree_nexus/icons/icon_handcuffed.png",
        "color": "#38bdf8",
        "maxRank": 5,
        "cost": [1, 1, 2, 3, 4],
        "requiredLevel": [1, 4, 8, 12, 18],
        "requires": [],
        "effectType": "JobActionXPMultiplier",
        "effectValue": [1.10, 1.20, 1.30, 1.40, 1.50],
        "callback": ""
    }
}
```

---

## Cost & Rank System

Nodes can have up to 5 ranks (or more). Each rank costs skill points and has a level requirement:

```
Rank 1:  cost[1] = 1,  requiredLevel[1] = 1
Rank 2:  cost[2] = 1,  requiredLevel[2] = 4
Rank 3:  cost[3] = 2,  requiredLevel[3] = 8
Rank 4:  cost[4] = 3,  requiredLevel[4] = 12
Rank 5:  cost[5] = 4,  requiredLevel[5] = 18
```

---

## Prerequisites (requires)

Nodes can require other nodes to be unlocked first:

```json
{
    "efficient_arrest": {
        "requires": ["police_training"]
    },
    "wanted_hunter": {
        "requires": ["efficient_arrest"]
    }
}
```

This creates a chain: `police_training → efficient_arrest → wanted_hunter`.

---

## Effect Values

Each rank can have a different effect value:

| Rank | `WalkSpeedMultiplier` | `DamageResistance` | `SpawnWithArmor` |
|------|----------------------|--------------------|-------------------|
| 1 | 1.03 (+3%) | 0.03 (3%) | 10 |
| 2 | 1.06 (+6%) | 0.06 (6%) | 20 |
| 3 | 1.09 (+9%) | 0.09 (9%) | 35 |
| 4 | 1.12 (+12%) | 0.12 (12%) | 50 |
| 5 | 1.15 (+15%) | 0.15 (15%) | 70 |

---

## Active Ability Nodes

Nodes with `"type": "active"` are abilities that players can manually activate with a cooldown:

```json
{
    "emergency_shield": {
        "id": "emergency_shield",
        "name": "Emergency Shield",
        "description": "Activate a temporary damage-absorbing shield.",
        "branch": "tactical",
        "gridX": 2,
        "gridY": 2,
        "icon": "../../materials/skilltree_nexus/icons/icon_shield.png",
        "color": "#22c55e",
        "maxRank": 3,
        "cost": [2, 3, 4],
        "requiredLevel": [15, 25, 35],
        "requires": ["tactical_response"],
        "effectType": "Shield",
        "effectValue": [50, 100, 150],
        "callback": "",
        "type": "active",
        "cooldown": 30,
        "duration": 8
    }
}
```
