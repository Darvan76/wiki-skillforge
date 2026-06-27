# Tree Validation

Every tree is automatically validated when loaded, saved, or deployed. The validator ensures structural integrity and security.

---

## Validation Rules

### Structural Checks

| Check | Error Message | Details |
|-------|---------------|---------|
| Root type | `Tree data must be a table` | Root must be a table |
| ID | `Tree must have a valid ID string` | Must be non-empty string |
| ID chars | `Tree ID contains unsafe characters` | Only alphanumeric, `-`, `_` |
| Name | `Tree must have a name` | Must be non-empty string |
| Branches | `Tree must have a branches table` | Must exist and be a table |
| Nodes | `Tree must have a nodes table` | Must exist and be a table |

### Branch Validation

| Check | Error Message |
|-------|---------------|
| Branch ID | `Branch ID is invalid` (alphanumeric + `-` + `_`) |
| Branch type | `Branch must be a table` |
| Branch name | `Branch is missing a name` |

### Node Validation

| Check | Error Message |
|-------|---------------|
| Node ID | `Node ID is invalid` |
| Node type | `Node must be a table` |
| Node name | `Node is missing a name` |
| Branch reference | `Node references non-existent branch` |
| Position | `Node requires valid numeric X and Y coordinates` |
| Max rank | `Node must have a maxRank integer > 0` |
| Cost array | `Node requires a 'cost' array matching its maxRank` |
| Cost values | `Node has invalid cost value at rank` |
| Required level | `Node requires a 'requiredLevel' array` |
| Effect values | `Node has invalid 'effectValue' array length` |
| Prerequisites | `Node requires non-existent node` |
| Effect type | `Node has invalid effectType` |
| Callback | `Node has invalid callback identifier name` |

---

## Security Scanning

The validator scans for suspicious content to prevent code injection through tree JSON files:

```lua title="lua/skillforge/sv_tree_validator.lua"
local function scanForCode(tbl)
    for k, v in pairs(tbl) do
        if type(v) == "string" then
            local lowerStr = string.lower(v)
            if string.find(lowerStr, "function%s*%(")
               or string.find(lowerStr, "ply:")
               or string.find(lowerStr, "os%.")
               or string.find(lowerStr, "http%.")
               or string.find(lowerStr, "runstring")
               or string.find(lowerStr, "debug%.") then
                return false, "Suspicious string containing executable code"
            end
        end
    end
end
```

---

## Cycle Detection

The validator runs a DFS-based cycle detection on the prerequisite graph:

```
Input:  A → B → C → A
Output: "Prerequisite cycle detected involving node 'A'"
```

---

## Running Validation

### Via console command

```
skilltree_validate_trees
```

This validates all loaded trees and reports results.

### Via API

```lua
local isValid, err = SkillTree.ValidateTree(treeData)
if not isValid then
    print("Tree validation failed: " .. err)
end
```

### Automatic validation

Validation runs automatically when:
- A tree is loaded from disk
- A tree is saved via the editor
- A tree is imported via JSON
- Default trees are deployed
