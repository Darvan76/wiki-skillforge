# Administration

Skillforge provides a comprehensive administration system with granular permissions, console commands, ULX commands, an HTML admin panel, backups, and logging.

---

## Overview

| Feature | Description |
|---------|-------------|
| [Permissions](permissions.md) | 12 granular permissions compatible with SAM, ULX, CAM, and fallback |
| [Console Commands](console-commands.md) | 20+ server console commands |
| [ULX Commands](ulx-commands.md) | 11 ULX chat commands for easy administration |
| [Admin Panel](admin-panel.md) | Full HTML/DHTML admin interface |
| [Backups](backups.md) | Tree backup and restore system |
| [Logs](logs.md) | SQLite admin logs and file-based logs |

---

## Admin Access

```lua
SkillTree.Config.Admin = {
    AllowedRanks = {"superadmin", "admin"},
    AllowSteamIDs = {}
}
```

Players with ranks in `AllowedRanks` or whose SteamID is in `AllowSteamIDs` can:
- Access the admin panel
- Use admin console commands
- Receive admin permissions if no SAM/ULX system is installed

For granular permission control, see [Permissions](permissions.md).
