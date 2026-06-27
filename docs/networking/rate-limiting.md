# Rate Limiting

Network messages are rate-limited to prevent abuse and server lag.

---

## Configuration

```lua
SkillTree.Config.AntiExploit.RateLimitNet = 0.5  -- Seconds between actions
```

---

## How Rate Limiting Works

### Global Rate Limit

Max 10 network actions per second per player:

```lua title="lua/skillforge/sv_networking.lua"
local now = CurTime()
if not limits._global or (now - limits._global.t) > 1 then
    limits._global = { t = now, n = 0 }
end
limits._global.n = limits._global.n + 1
if limits._global.n > 10 then
    -- Block and log as security event
    return false
end
```

### Per-Action Cooldown

Each action type has its own cooldown:

```lua
local cooldown = SkillTree.Config.AntiExploit.RateLimitNet or 0.5
if (now - (limits[action] or 0)) < cooldown then return false end
limits[action] = now
```

### Input Validation

All input strings are validated for length and character safety:

```lua
local function IsValidID(id)
    return type(id) == "string" and #id > 0 and #id <= 64
        and string.match(id, "^[%a%d_%-]+$") ~= nil
end
```

---

## Rate Limited Actions

| Action | Global Cap | Per-Action Cooldown |
|--------|------------|-------------------|
| `unlock_skill` | 10/s | 0.5s |
| `use_ability` | 10/s | 0.5s |
| `reset_skills` | 10/s | 0.5s |
| `req_sync` | 10/s | 0.5s |
| `admin_action` | 10/s | 0.2s (separate) |
| `request_admin_data` | 10/s | 1s (separate) |

---

## Security Logging

Violations are logged:

```lua
if SkillTree.Log then
    SkillTree.Log.Add("security",
        string.format("%s hit global net rate limit (action: %s)",
        ply:Nick(), action))
end
```

---

## Connection Cleanup

Rate limit data is cleaned up on disconnect:

```lua
hook.Add("PlayerDisconnected", "stn_net_cleanup_ratelimit", function(ply)
    SkillTree.Net.RateLimit[steamID] = nil
    SkillTree.ActiveCooldowns[steamID] = nil
end)
```
