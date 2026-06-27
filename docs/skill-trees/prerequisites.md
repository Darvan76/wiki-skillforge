# Prerequisites

Nodes can require other nodes to be unlocked first, creating skill trees with meaningful progression paths.

---

## How Prerequisites Work

Each node has a `requires` array that lists node IDs that must be unlocked before this node can be purchased:

```json
{
    "police_training": {
        "requires": []
    },
    "efficient_arrest": {
        "requires": ["police_training"]
    },
    "wanted_hunter": {
        "requires": ["efficient_arrest"]
    }
}
```

This creates a linear chain: `police_training → efficient_arrest → wanted_hunter`.

---

## Multiple Prerequisites

A node can require multiple other nodes:

```json
{
    "combat_mastery": {
        "requires": ["combat_training", "sidearm_drills", "rifle_control"]
    }
}
```

All prerequisites must be unlocked before `combat_mastery` is available.

---

## Validation: Cycle Detection

The system automatically detects prerequisite cycles to prevent deadlocks:

```lua title="lua/skillforge/sv_tree_validator.lua"
local function detectCycle(nodeID, nodes, visited, recStack)
    visited[nodeID] = true
    recStack[nodeID] = true

    local node = nodes[nodeID]
    if node and node.requires then
        for _, reqID in ipairs(node.requires) do
            if not visited[reqID] then
                if detectCycle(reqID, nodes, visited, recStack) then
                    return true
                end
            elseif recStack[reqID] then
                return true  -- Cycle detected!
            end
        end
    end
    recStack[nodeID] = false
    return false
end
```

!!! warning "Circular prerequisites"
    If you create a cycle (A → B → C → A), the tree will fail validation and won't load.

---

## Checking Availability

Unlock availability is checked server-side:

```lua title="lua/skillforge/sh_effect_types.lua"
function SkillTree.CanUpgradeSkill(ply, treeID, skillID)
    -- ... check level, points ...

    local requires = skillData.requires
    if requires then
        for _, reqID in ipairs(requires) do
            if not ply:STN_HasSkill(reqID) then
                return false, "RequirementNotMet"
            end
        end
    end

    return true, "OK"
end
```

---

## Visual Representation

In the skill tree UI, prerequisites are shown as connecting lines between nodes. Nodes with unmet prerequisites appear grayed out with a lock icon.

---

## Best Practices

- **Depth**: Keep tree depth to 3-4 nodes max per branch
- **Width**: Offer 3-4 nodes at each tier for meaningful choices
- **Bottlenecks**: Avoid single-node bottlenecks (one node required for everything)
- **Theming**: Prerequisites should make thematic sense (e.g., "Rifle Control" → "Sniper Training")
