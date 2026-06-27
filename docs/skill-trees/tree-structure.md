# Tree Structure

Complete reference for the skill tree JSON schema.

---

## Root Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | string | ✅ | Unique tree identifier (snake_case) |
| `name` | string | ✅ | Display name |
| `description` | string | ✅ | Brief description |
| `author` | string | ✅ | Creator name |
| `version` | string | ✅ | Version string |
| `branches` | object | ✅ | Map of branch objects |
| `nodes` | object | ✅ | Map of node objects |
| `connections` | array | ❌ | Connection array |

---

## Complete Example

```json title="data/skillforge/trees/my_tree.json"
{
    "id": "my_custom_tree",
    "name": "My Custom Tree",
    "description": "Description of what this tree does.",
    "author": "YourName",
    "version": "1.0.0",
    "branches": {
        "combat": {
            "id": "combat",
            "name": "Combate",
            "description": "Branch description.",
            "color": "#ef4444",
            "icon": "../../materials/skilltree_nexus/icons/icon_combat.png"
        }
    },
    "nodes": {
        "my_first_node": {
            "id": "my_first_node",
            "name": "Node Name",
            "description": "Tooltip description of the node.",
            "branch": "combat",
            "gridX": 1,
            "gridY": 1,
            "x": 140,
            "y": 140,
            "icon": "../../materials/skilltree_nexus/icons/icon_runner.png",
            "color": "#ef4444",
            "maxRank": 5,
            "cost": [1, 1, 2, 2, 3],
            "requiredLevel": [1, 5, 10, 15, 20],
            "requires": [],
            "effectType": "WalkSpeedMultiplier",
            "effectValue": [1.03, 1.06, 1.09, 1.12, 1.15],
            "callback": ""
        }
    },
    "connections": [
        { "from": "my_first_node", "to": "my_second_node" }
    ]
}
```

---

## Field Validation

| Field | Validation Rules |
|-------|-----------------|
| `id` | Alphanumeric, underscores, dashes only. Max 64 chars. |
| `branch` | Must reference an existing branch ID |
| `x`, `y` | Numeric coordinates (auto-converted from gridX/gridY with 140px spacing) |
| `maxRank` | Integer ≥ 1 |
| `cost` | Array length must match maxRank, all values ≥ 0 |
| `requiredLevel` | Array length must match maxRank, all values ≥ 0 |
| `effectValue` | Array length must match maxRank (optional) |
| `requires` | Must reference existing node IDs |
| `effectType` | Must be a valid registered effect type |
| `callback` | Alphanumeric only (no special characters or spaces) |

---

## How to Create a Tree

### Option 1: Manual JSON

Create a file in `data/skillforge/trees/` on your server:

```json
// data/skillforge/trees/my_custom_tree.json
```

Then reload:

```
skilltree_reload_trees
```

### Option 2: Using the Visual Editor

Open the editor:

```
skilltree_editor
```

Use the HTML interface to create, edit, and save trees.

### Option 3: Programmatically

```lua
local treeData = {
    id = "my_custom_tree",
    name = "My Custom Tree",
    description = "Created via script",
    author = "Me",
    version = "1.0.0",
    branches = { ... },
    nodes = { ... }
}
SkillTree.SaveTree("my_custom_tree", treeData)
```

---

## Template File

A ready-to-use template is available at:
`lua/skillforge/default_trees/_TEMPLATE.json`
