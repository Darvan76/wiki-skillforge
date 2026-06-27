# Visual Editor

Skillforge includes a full HTML/DHTML visual editor for creating and modifying skill trees without writing JSON by hand.

---

## Overview

The visual editor allows server administrators to:

- Create new skill trees
- Add and configure branches
- Add and configure nodes
- Create prerequisite connections between nodes
- Position nodes on a grid
- Preview the tree layout
- Save directly to the server

---

## Accessing the Editor

Open the editor with the console command:

```
skilltree_editor
```

Requires the `skilltree.admin.editor` permission.

---

## Editor Features

| Feature | Description |
|---------|-------------|
| Canvas | Zoomable, panable canvas for tree layout |
| Node Inspector | Click any node to edit its properties |
| Branch Manager | Create, edit, and delete branches |
| Connection Tool | Draw connections between nodes |
| Grid Snapping | Auto-snap nodes to grid positions |
| Real-time Preview | See the tree as players will see it |
| Validation | Automatic validation on save |

---

## Related Pages

- [Getting Started](getting-started.md) — First steps with the editor
- [Creating Trees](creating-trees.md) — Create a tree from scratch
- [Editing Nodes](editing-nodes.md) — Add, edit, and delete nodes
- [Branches & Connections](branches-and-connections.md) — Work with branches and prerequisite links
- [Export & Import](export-import.md) — Import/export tree JSON
