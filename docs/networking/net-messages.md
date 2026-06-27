# Net Messages

Skillforge uses **17 network strings** for client-server communication.

---

## Network Strings

| Channel | Direction | Payload | Purpose |
|---------|-----------|---------|---------|
| `stn_unlock_skill` | C → S | skillID (string) | Player upgrades a skill |
| `stn_use_ability` | C → S | skillID (string) | Player uses active ability |
| `stn_reset_skills` | C → S | (none) | Player resets skills |
| `stn_open_menu` | C → S | (none) | Player opens menu |
| `stn_sync_skills` | S → C | NW vars (5 values) | Sync player data |
| `stn_xp_gained` | S → C | amount (u32), reason (string) | XP gain notification |
| `stn_level_up` | S → C | newLevel (u32), pointsGained (u32) | Level-up notification |
| `stn_skill_unlocked` | S → C | skillID (string), newRank (u8) | Skill unlock notification |
| `stn_notification` | S → C | text (string), type (string) | Toast notification |
| `stn_sync_trees` | S → C | Tree data (compressed) | Full tree sync |
| `stn_save_tree` | C → S | Tree JSON (compressed) | Editor saves tree |
| `stn_req_sync` | C → S | (none) | Request data resync |
| `stn_sync_job_mappings` | S → C | Job mappings (compressed) | Job → tree mapping sync |
| `stn_admin_action` | C → S | action, targetSID, arg1, arg2, reason | Admin panel action |
| `stn_request_admin_data` | C → S | (none) | Request admin data package |
| `stn_admin_data` | S → C | Full admin package (compressed) | Dashboard/players/logs/analytics |
| `stn_level_up_fx` | S → C | entity, level (u16), effectType (string) | Level-up particles |

---

## Networked Variables

Each player has these networked variables:

| NW Variable | Type | Description |
|-------------|------|-------------|
| `stn_skills` | NWString (JSON) | `{skillID: rank}` |
| `stn_active_tree` | NWString | Current tree ID |
| `stn_points` | NWInt | Available skill points |
| `stn_level` | NWInt | Current level |
| `stn_xp` | NWInt | Current XP |
| `stn_prestige` | NWInt | Prestige level |

---

## Tree Sync

Trees are synced to clients in compressed form:

```lua title="lua/skillforge/sv_networking.lua"
function SkillTree.SyncTreesToClients(ply)
    local json = util.TableToJSON(SkillTree.Trees)
    local compressed = util.Compress(json)

    net.Start("stn_sync_trees")
    net.WriteUInt(#compressed, 32)
    net.WriteData(compressed, #compressed)
    if ply then net.Send(ply) else net.Broadcast() end
end
```

Trees are sent:
- When a player joins (after 2s delay)
- When `skilltree_reload_trees` is executed
- When the client requests a resync

---

## Rate Limiting

See [Rate Limiting](rate-limiting.md) for details on how net messages are rate-limited to prevent abuse.
