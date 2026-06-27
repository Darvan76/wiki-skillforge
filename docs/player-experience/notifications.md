# Notifications

The notification system provides toast-style messages for various events.

---

## How It Works

Notifications are sent from the server to individual clients via net messages:

```lua title="lua/skillforge/sv_networking.lua"
function SkillTree.Net.SendNotification(ply, text, typeStr)
    net.Start("stn_notification")
    net.WriteString(text)
    net.WriteString(typeStr or "info")
    net.Send(ply)
end
```

---

## Notification Types

| Type | Color | Usage |
|------|-------|-------|
| `info` | Blue | General information |
| `success` | Green | Successful actions (unlock, upgrade) |
| `error` | Red | Errors (not enough points, requirements not met) |
| `warning` | Yellow | Warnings (cooldown active) |
| `skill` | Purple | Skill-related events (ability activation) |

---

## Notification Events

| Event | Type | Message |
|-------|------|---------|
| Skill unlocked | `success` | "Unlocked: Skill Name (Rank 1)" |
| Skill upgraded | `success` | "Upgraded: Skill Name (Rank 2)" |
| XP gained | `info` | "+50 XP (Arrest)" |
| Level up | `success` | "Level Up! 15 (+1 Pts)" |
| Not enough points | `error` | "Not enough skill points!" |
| Level too low | `error` | "Your level is too low!" |
| Prerequisites not met | `error` | "Prerequisites not met!" |
| Ability ready | `info` | "Shield activated! +50 HP absorbed" |
| Reset complete | `success` | "Skills successfully reset!" |
| Reset cooldown | `error` | "You must wait 12h 30m before resetting" |
| Discount applied | `success` | "Discount applied: $500 refunded!" |

---

## Custom Notifications

You can send custom notifications from your own code:

```lua
-- From any server-side code
SkillTree.Net.SendNotification(ply, "Custom message here!", "info")
```

---

## Notification Display Duration

Notifications auto-dismiss after approximately 4 seconds. They stack vertically if multiple appear at once.
