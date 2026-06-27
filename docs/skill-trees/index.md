# Skill Trees

Skill trees are the core of Skillforge. Each tree contains **branches** (categories) and **nodes** (skills) that players can unlock.

---

## What is a Skill Tree?

A skill tree is a JSON file stored in `data/skillforge/trees/*.json`. It defines:

- **Branches** — Categories like "Combat", "Defense", "Mobility"
- **Nodes** — Individual skills within branches
- **Connections** — Prerequisite relationships between nodes

---

## Default Trees

Skillforge ships with **9 default trees**:

| Tree ID | Name | Branches | Nodes | Best For |
|---------|------|----------|-------|----------|
| `darkrp_default` | Skillforge RPG | 8 | ~48 | General use / RPG core |
| `police_tree` | Police Department | 4 | 12 | Law enforcement jobs |
| `medic_tree` | Medical Corps | 4 | 12 | Medical jobs |
| `garbage_tree` | Sanitation | 4 | 12 | Garbage collector jobs |
| `criminal_tree` | Criminal Network | 4 | 12 | Criminal jobs |
| `gun_dealer_tree` | Arms Trade | 4 | 12 | Gun dealer jobs |
| `economy_tree` | Economic Empire | 4 | 12 | Economy jobs |
| `citizen_tree` | Citizen | 4 | 12 | Default civilian jobs |
| `cook_tree` | Culinary Arts | 4 | 12 | Cook jobs |

---

## Tree Structure

```json
{
    "id": "police_tree",
    "name": "Police Department",
    "description": "Complete police hierarchy",
    "author": "System",
    "version": "2.0.0",
    "branches": { ... },
    "nodes": { ... },
    "connections": [ ... ]
}
```

---

## Deploying Trees

Trees are automatically deployed from `lua/skillforge/default_trees/` to `data/skillforge/trees/` when the server starts. The system only deploys trees that don't already exist in the data directory.

```lua title="lua/skillforge/sv_tree_loader.lua"
local DEFAULT_TREE_FILES = {
    "darkrp_default.json",
    "police_tree.json",
    "garbage_tree.json",
    "medic_tree.json",
    "criminal_tree.json",
    "gun_dealer_tree.json",
    "citizen_tree.json",
    "economy_tree.json",
    "cook_tree.json"
}
```

---

## Related Pages

- [Tree Structure](tree-structure.md) — Complete JSON schema
- [Branches](branches.md) — Working with branches
- [Nodes](nodes.md) — Node configuration
- [Effect Types](effect-types.md) — All available effects
- [Active Abilities](active-abilities.md) — Active skill types
- [Prerequisites](prerequisites.md) — Node requirements
- [Validation](validation.md) — Tree validation rules
