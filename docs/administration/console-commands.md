# Console Commands

Server and client console commands for administration.

---

## Player Commands

| Command | Description | Usage |
|---------|-------------|-------|
| `skilltree_open` | Open the skill menu | Client |
| `skilltree_editor` | Open the visual tree editor | Admin only |

## Chat Commands

| Command | Description |
|---------|-------------|
| `!skills` or `/skills` | Open the skill menu |

## Key Bind

| Key | Description |
|-----|-------------|
| `F6` (configurable) | Toggle skill menu |

---

## Admin Commands

All admin commands require the server console or client console with appropriate permissions.

### XP Management

| Command | Permission | Syntax |
|---------|-----------|--------|
| `skilltree_givexp` | `skilltree.admin.givexp` | `skilltree_givexp <player> <amount>` |
| `skilltree_takexp` | `skilltree.admin.givexp` | `skilltree_takexp <player> <amount>` |

### Level Management

| Command | Permission | Syntax |
|---------|-----------|--------|
| `skilltree_setlevel` | `skilltree.admin.setlevel` | `skilltree_setlevel <player> <level>` |

### Point Management

| Command | Permission | Syntax |
|---------|-----------|--------|
| `skilltree_givepoints` | `skilltree.admin.manage_players` | `skilltree_givepoints <player> <amount>` |
| `skilltree_takepoints` | `skilltree.admin.manage_players` | `skilltree_takepoints <player> <amount>` |

### Skill Management

| Command | Permission | Syntax |
|---------|-----------|--------|
| `skilltree_resetskills` | `skilltree.admin.reset` | `skilltree_resetskills <player>` |
| `skilltree_resetbranch` | `skilltree.admin.reset` | `skilltree_resetbranch <player> <branchID>` |
| `skilltree_unlockskill` | `skilltree.admin.manage_players` | `skilltree_unlockskill <player> <skillID>` |
| `skilltree_lockskill` | `skilltree.admin.manage_players` | `skilltree_lockskill <player> <skillID>` |

### Tree Management

| Command | Permission | Syntax |
|---------|-----------|--------|
| `skilltree_reload_trees` | `skilltree.admin.manage_trees` | `skilltree_reload_trees` |
| `skilltree_validate_trees` | `skilltree.admin.manage_trees` | `skilltree_validate_trees` |

### Job-Specific Commands

| Command | Permission | Syntax |
|---------|-----------|--------|
| `skilltree_givejobxp` | `skilltree.admin.givexp` | `skilltree_givejobxp <player> <amount> [job]` |
| `skilltree_setjoblevel` | `skilltree.admin.setlevel` | `skilltree_setjoblevel <player> <level> [job]` |
| `skilltree_resetjobtree` | `skilltree.admin.reset` | `skilltree_resetjobtree <player> [job]` |
| `skilltree_reloadjobxp` | `skilltree.admin.manage_trees` | `skilltree_reloadjobxp` |

### Debug

| Command | Permission | Syntax |
|---------|-----------|--------|
| `skilltree_save_all` | `skilltree.admin.debug` | `skilltree_save_all` |
| `skilltree_showjobprogress` | `skilltree.admin.view` | `skilltree_showjobprogress <player>` |
| `skilltree_test_levelup_fx` | SuperAdmin only | `skilltree_test_levelup_fx <player> [effect]` |
| `skilltree_preview_levelup_fx` | Debug mode | Client-only |

---

## Examples

```lua title="Console"
// Give XP
skilltree_givexp "John Doe" 500

// Set level
skilltree_setlevel "John Doe" 25

// Reset skills
skilltree_resetskills "John Doe"

// Unlock a specific skill
skilltree_unlockskill "John Doe" "combat_training"

// Reload all trees from disk
skilltree_reload_trees

// Validate all trees
skilltree_validate_trees
```
