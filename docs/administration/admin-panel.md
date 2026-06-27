# Admin Panel

The HTML admin panel provides a comprehensive interface for managing Skillforge.

---

## Opening the Panel

```
// In-game console
skilltree_admin
```

This opens an HTML panel with the following sections:

---

## Dashboard

The dashboard shows real-time analytics:

- **XP Today** — Total XP earned across all players today
- **Players Online** — Count of online players with Skillforge data
- **Recent Level Ups** — Last 10 level-up events
- **Popular Skills** — Most popular skills across all players
- **Popular Branches** — Most popular branches

---

## Players

A searchable list of all online players with:

| Column | Description |
|--------|-------------|
| Name | Player name with SteamID |
| Level | Current level |
| XP | Current XP / XP required |
| Points | Available skill points |
| Tree | Active tree ID |
| IP | Player's IP address |
| Ping | Connection ping |
| Skills | Each unlocked skill with rank |

You can click a player to see their full skill breakdown.

---

## Action Buttons

For each player, you can:

| Action | Description |
|--------|-------------|
| Give XP | Award XP to the player |
| Take XP | Remove XP from the player |
| Set Level | Set the player's level |
| Give Points | Award skill points |
| Take Points | Remove skill points |
| Reset Tree | Reset all skills |
| Reset Branch | Reset a specific branch |
| Unlock Skill | Force unlock a skill |
| Lock Skill | Force lock a skill |
| Re-sync | Force full data sync |
| Re-apply Effects | Re-apply all skill effects |

---

## Logs

View the last 50 admin actions with:

- Admin name
- Target name
- Action type
- Details
- Timestamp

---

## Backups

Manage tree backups:

- **Create Backup** — Backup a tree's current state
- **Restore Backup** — Restore a tree from a backup file
- **Delete Backup** — Remove old backup files

---

## Analytics

Server-wide analytics:

- Total player records in database
- XP earned today
- Skill popularity ranking
- Branch popularity ranking
- Recent level-ups with timestamps

---

## Tree Management

View all loaded trees with their metadata (name, author, version, node count). From here you can:

- Validate all trees
- Reload trees from disk
- Edit job-tree mappings

---

## Job Configuration

Dynamic job-tree mapping management:

- View current job → tree mappings
- Assign a tree to a job
- Remove a tree from a job
- Changes are saved to persistent config

```lua
-- Mappings are stored in data/skillforge/job_mappings.json
-- Changes take effect immediately
```
