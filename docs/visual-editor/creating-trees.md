# Creating Trees

## New Tree From Scratch

1. Click **File → New Tree**
2. Set the tree properties:
   - **ID**: `my_custom_tree` (unique, alphanumeric + underscores)
   - **Name**: "My Custom Tree"
   - **Description**: Brief description
   - **Author**: Your name
   - **Version**: `1.0.0`

---

## Adding Branches

1. Click **Add Branch**
2. Set properties:
   - **ID**: `combat` (unique per tree)
   - **Name**: "Combat"
   - **Description**: "Combat skills"
   - **Color**: `#ef4444` (hex color)
   - **Icon**: Select from available icons

---

## Adding Nodes

1. Right-click on the canvas
2. Select **Add Node**
3. Click to place it on the grid
4. Configure in the inspector panel

### Required Node Properties

| Property | Description |
|----------|-------------|
| ID | Unique node identifier |
| Name | Display name |
| Branch | Which branch it belongs to |
| Max Rank | Max upgrade level (1-5) |
| Cost | Skill point cost per rank |
| Required Level | Level requirement per rank |

### Optional Node Properties

| Property | Description |
|----------|-------------|
| Effect Type | Type of effect this node grants |
| Effect Value | Value per rank |
| Prerequisites | Other nodes required first |
| Callback | Developer callback name |
| Active Ability | Enable cooldown/duration for active skills |

---

## Saving

Click **Save** to write the tree to the server. The tree is validated before saving. If validation fails, error messages will indicate what needs to be fixed.
