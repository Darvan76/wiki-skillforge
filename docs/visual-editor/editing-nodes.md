# Editing Nodes

## Selecting a Node

Click on any node on the canvas. The inspector panel on the right will show its properties.

---

## Node Properties

### General

| Field | Description |
|-------|-------------|
| ID | Unique identifier (read-only after creation) |
| Name | Display name shown to players |
| Description | Tooltip description |
| Branch | Branch this node belongs to |

### Position

| Field | Description |
|-------|-------------|
| Grid X | Column position (0 = leftmost) |
| Grid Y | Row position (0 = top) |

Drag the node to reposition, or enter coordinates manually. Grid spacing is 140px.

### Ranks

| Field | Description |
|-------|-------------|
| Max Rank | How many times this skill can be upgraded |
| Cost 1-5 | Skill point cost for each rank |
| Level Req 1-5 | Required player level for each rank |

### Effects

| Field | Description |
|-------|-------------|
| Effect Type | Choose from 28 effect types |
| Effect Value 1-5 | Value for each rank |

### Prerequisites

The **requires** field lists other node IDs that must be unlocked first. Use the connection tool to visually create prerequisites.

### Active Ability

Toggle to make this an active ability, then set:

| Field | Description |
|-------|-------------|
| Cooldown | Seconds between uses |
| Duration | Duration of the effect (if applicable) |

---

## Deleting a Node

1. Select the node
2. Press **Delete** key or click the delete button in the inspector
3. Confirm deletion

!!! warning "Connection removal"
    Deleting a node also removes all its connections. Other nodes that required this node will become invalid until reconnected.
