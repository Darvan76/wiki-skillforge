# Permissions

Skillforge has **12 granular permissions** for fine-grained admin control.

---

## Permission System

Permissions are checked in this order:

```lua title="lua/skillforge/shared/sh_admin.lua"
function SkillTree.HasPermission(ply, perm)
    -- Superadmins always bypass
    if ply:IsSuperAdmin() then return true end

    -- 1. SAM compatibility
    if ply.HasPermission and ply:HasPermission(perm) then return true end

    -- 2. ULX / ULib compatibility
    if ULib and ULib.ucl and ULib.ucl.query then
        if ULib.ucl.query(ply, perm) then return true end
    end

    -- 3. CAM (Common Admin Manager)
    if CAM and CAM.HasPermission then
        if CAM.HasPermission(ply, perm) then return true end
    end

    -- 4. Fallback: IsAdmin whitelist
    if SkillTree.IsAdmin(ply) then return true end

    return false
end
```

---

## Permission List

| Permission | Description | Used By |
|-----------|-------------|---------|
| `skilltree.admin.view` | View the admin panel | Panel access |
| `skilltree.admin.manage_players` | Modify player level, XP, and points | Commands + Panel |
| `skilltree.admin.givexp` | Give/take XP from players | `skilltree_givexp`, Panel |
| `skilltree.admin.setlevel` | Set a player's level | `skilltree_setlevel`, Panel |
| `skilltree.admin.reset` | Reset skills, branches, or trees | `skilltree_resetskills`, Panel |
| `skilltree.admin.editor` | Access the visual tree editor | `skilltree_editor` |
| `skilltree.admin.manage_trees` | Create, save, activate, reload trees | Editor + Commands |
| `skilltree.admin.import` | Import tree JSON | Panel |
| `skilltree.admin.export` | Export tree JSON | Panel |
| `skilltree.admin.delete` | Delete tree configs from disk | Panel |
| `skilltree.admin.logs` | View admin action logs | Panel |
| `skilltree.admin.debug` | Use debug/sync tools | Debug commands |

---

## ULX Registration

If ULX is installed, all permissions are automatically registered with ULib:

```lua title="lua/ulx/modules/sh/skillforge.lua"
for perm, desc in pairs(SkillTree.Permissions) do
    ULib.ucl.registerAccess(perm, "superadmin", desc, "SkillTree")
end
```

You can then use ULX commands to assign permissions:

```
!ulx adduser "Player" "skilltree.admin.view"
!ulx adduser "Player" "skilltree.admin.givexp"
```

---

## Permission Mapping

| Console Command | Required Permission |
|----------------|-------------------|
| `skilltree_givexp` | `skilltree.admin.givexp` |
| `skilltree_takexp` | `skilltree.admin.givexp` |
| `skilltree_setlevel` | `skilltree.admin.setlevel` |
| `skilltree_givepoints` | `skilltree.admin.manage_players` |
| `skilltree_takepoints` | `skilltree.admin.manage_players` |
| `skilltree_resetskills` | `skilltree.admin.reset` |
| `skilltree_unlockskill` | `skilltree.admin.manage_players` |
| `skilltree_lockskill` | `skilltree.admin.manage_players` |
| `skilltree_admin` | `skilltree.admin.view` |
| `skilltree_editor` | `skilltree.admin.editor` |
