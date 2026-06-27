# Branches & Connections

## Managing Branches

### Add Branch

1. Click **Add Branch** in the toolbar
2. Fill in:
   - **ID**: Unique identifier
   - **Name**: Display name
   - **Description**: Branch description
   - **Color**: Hex color for branch nodes
   - **Icon**: Choose from available icons

### Edit Branch

1. Click a branch in the branch list
2. Edit properties in the inspector

### Delete Branch

1. Select branch in the branch list
2. Click delete
3. All nodes in this branch must be reassigned or deleted

---

## Connections (Prerequisites)

Connections create the prerequisite relationships between nodes.

### Create a Connection

1. Enable the **Connection Tool** (shortcut: `C`)
2. Click on the source node (prerequisite)
3. Click on the target node (requires the source)
4. A line appears connecting them

### Visual Indicators

- **Arrow direction**: Source → Target
- **Color**: Matches the branch color
- **Line style**: Solid for available, dashed if locked

### Editing Connections

- Click a connection line to select it
- Press **Delete** to remove the connection
- Drag connection points to reconnect

---

## Connection Validation

The editor validates connections in real-time:

- ✅ Connection valid
- ⚠️ Creates a circular dependency (blocked)
- ❌ Target node references non-existent source

---

## Best Practices

- Keep branches to 3-4 nodes deep max
- Use consistent color coding per branch
- Place root nodes (no prerequisites) at the top
- Chain prerequisites logically: basic → advanced → mastery
- Use connection lines to create clear progression paths
