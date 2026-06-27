# Logs

Skillforge provides two logging systems: SQLite admin logs and file-based logs.

---

## Admin Logs (SQLite)

All admin actions are logged in the `skillforge_admin_logs` SQLite table:

```sql
CREATE TABLE IF NOT EXISTS skillforge_admin_logs (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    admin_steamid TEXT,
    admin_name TEXT,
    target_steamid TEXT,
    target_name TEXT,
    action TEXT,
    details TEXT,
    timestamp INTEGER
)
```

### Logged Actions

| Action | Description |
|--------|-------------|
| `give_xp` | Admin gave XP to player |
| `take_xp` | Admin took XP from player |
| `set_level` | Admin set player level |
| `modify_points` | Admin modified skill points |
| `reset_tree` | Admin reset player's tree |
| `reset_branch` | Admin reset a branch |
| `reset_skill` | Admin reset a skill |
| `force_unlock` | Admin force-unlocked a skill |
| `force_lock` | Admin force-locked a skill |
| `save_all` | Manual save triggered |
| `reload_trees` | Trees reloaded from disk |
| `validate_trees` | Trees validated |
| `resync_player` | Player data re-synced |
| `reapply_effects` | Effects re-applied |
| `backup_create` | Tree backup created |
| `backup_restore` | Tree restored from backup |
| `backup_delete` | Backup deleted |
| `console_*` | Various console commands |
| `ulx_*` | Various ULX commands |
| `security_violation` | Unauthorized access attempt |

---

## File Logs

General system logs are written to `data/skillforge/logs/`:

```
data/skillforge/logs/
├── 2026_01_01.txt
├── 2026_01_02.txt
└── ...
```

### Log Categories

| Category | Description | Debug Only |
|----------|-------------|------------|
| `skill` | Skill unlock/upgrade events | No |
| `reset` | Skill resets | No |
| `admin` | Admin actions | No |
| `level` | Level-up events | No |
| `security` | Security violations | No |
| `xp` | XP gain events | Yes (Debug mode only) |

### Log Format

```
[Skillforge] [SKILL] [2026-01-01 12:00:00] PlayerName upgraded skill combat_training to rank 3 on tree darkrp_default
[Skillforge] [ADMIN] [2026-01-01 12:01:00] AdminName -> PlayerName | Action: give_xp | Gave 500 XP
[Skillforge] [SECURITY] [2026-01-01 12:02:00] Blocked unknown callback 'hack_func' on tree 'police_tree' skill 'police_training'
```

---

## Debug Mode

Enable detailed logging:

```lua
SkillTree.Config.General.Debug = true
```

This enables XP logging and additional debug output. Disable in production to avoid excessive log file growth.

---

## Viewing Logs

### Admin Panel

The admin panel shows the last 50 SQLite log entries.

### File Logs

Read the log files from the server:

```lua
local logContent = file.Read("skillforge/logs/2026_01_01.txt", "DATA")
```
