# Export & Import

## Exporting a Tree

### From the Editor

1. Open the tree you want to export
2. Click **File → Export**
3. The JSON is copied to your clipboard
4. Paste it into a file and save

### From the Server

```lua
local json = SkillTree.ExportTree("police_tree")
file.Write("my_exported_tree.json", json)
```

---

## Importing a Tree

### Via Console Command

1. Have your JSON ready
2. Open the editor
3. Click **File → Import**
4. Paste the JSON
5. The tree appears on the canvas
6. Review and save

### Via API

```lua
local json = file.Read("my_custom_tree.json", "DATA")
local ok, treeID = SkillTree.ImportTree(json)
if ok then
    print("Tree imported: " .. treeID)
else
    print("Import failed: " .. treeID)  -- Contains error message
end
```

### Via File Copy

Copy the JSON file to `data/skillforge/trees/` on your server:

```
data/skillforge/trees/my_custom_tree.json
```

Then reload:

```
skilltree_reload_trees
```

---

## Import Validation

When importing, the tree is automatically validated. Common errors:

| Error | Cause |
|-------|-------|
| Invalid JSON format | Syntax error in the JSON |
| Missing tree 'id' | No `id` field in root |
| Validation failed | Tree structure doesn't meet requirements |

---

## Sharing Trees

You can share tree JSON files with other server owners:

```json
{
    "id": "shared_tree",
    "name": "Shared Community Tree",
    "author": "Community Member",
    "version": "1.0.0",
    ...
}
```

To install:
1. Copy the JSON file
2. Import via editor or file copy
3. Map it to a job in your config
