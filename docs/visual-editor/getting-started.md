# Visual Editor - Getting Started

## Opening the Editor

```
skilltree_editor
```

Requires: `skilltree.admin.editor` permission.

---

## Interface Overview

The editor interface consists of:

1. **Toolbar (top)** — Tools for creating branches, nodes, and connections
2. **Canvas (center)** — Drag-and-drop workspace for tree layout
3. **Inspector (right panel)** — Properties panel for selected elements
4. **Branch List (left panel)** — List of all branches in the current tree

---

## Basic Navigation

| Action | Mouse/Keyboard |
|--------|---------------|
| Pan | Click and drag on empty canvas space |
| Zoom | Mouse scroll wheel |
| Select node | Left click on a node |
| Deselect | Click on empty canvas |
| Delete selected | Delete key |

---

## Quick Workflow

1. **Open the editor** — `skilltree_editor`
2. **Create a branch** — Click "Add Branch" and set name/color
3. **Add nodes** — Right-click on the canvas and select "Add Node"
4. **Position nodes** — Drag nodes to desired grid positions
5. **Connect nodes** — Drag from a node's output to another's input
6. **Configure properties** — Click a node and edit in the inspector
7. **Save** — Click "Save Tree" to save to the server

---

## Saving

- **Save** writes the tree to `data/skillforge/trees/` on the server
- Trees are immediately available after saving
- Players currently viewing the tree will need to re-open to see changes
