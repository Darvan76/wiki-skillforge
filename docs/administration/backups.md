# Backups

Skillforge includes a built-in backup and restore system for skill trees.

---

## How It Works

Backups are stored in `data/skillforge/backups/` as timestamped JSON files:

```
data/skillforge/backups/
├── tree_police_tree_20260101_120000.json
├── tree_darkrp_default_20260101_120000.json
└── tree_criminal_tree_20260101_120000.json
```

---

## Commands

### Create a Backup

```lua
SkillTree.Admin.CreateBackup(treeID, suffix)
-- Returns: true, filename
```

Via admin panel: click **Create Backup** for any tree.

### Restore a Backup

```lua
SkillTree.Admin.RestoreBackup(filename)
-- Returns: true, treeID
```

This:
1. Reads the backup file
2. Validates the JSON structure
3. Writes it to the active tree location (`data/skillforge/trees/`)
4. Reloads all trees from disk

### Delete a Backup

```lua
SkillTree.Admin.DeleteBackup(filename)
-- Returns: true on success
```

---

## Automatic Backups

There is no automatic backup schedule by default. Admins should create backups:

- Before editing a tree
- After major configuration changes
- Before updates/patches

---

## Best Practices

```lua
-- Create a backup before editing
SkillTree.Admin.CreateBackup("police_tree")

-- If something goes wrong, restore
SkillTree.Admin.RestoreBackup("tree_police_tree_20260101_120000.json")

-- Clean up old backups periodically
-- Manual via admin panel
```

---

## Backup File Format

Backup files are identical to the tree JSON format, just saved with a timestamp suffix:

```json
{
    "id": "police_tree",
    "name": "Police Department",
    "description": "...",
    "author": "System",
    "version": "2.0.0",
    "branches": { ... },
    "nodes": { ... }
}
```
