# Visual Theme

Control the colors, animations, and visual effects of the skill tree menu.

---

## Configuration Table

```lua title="lua/skillforge/sh_config.lua"
SkillTree.Config.Theme = {
    PrimaryColor = Color(120, 80, 255),
    SecondaryColor = Color(80, 200, 255),
    BackgroundColor = Color(15, 15, 25, 240),
    LockedColor = Color(80, 80, 80),
    UnlockedColor = Color(120, 80, 255),
    AvailableColor = Color(80, 200, 255),
    MaxedColor = Color(255, 200, 50),
    EnableBlur = true,
    EnableAnimations = true,
    EnableSounds = true
}
```

---

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `PrimaryColor` | `Color` | `120, 80, 255` | Primary accent color (purple) |
| `SecondaryColor` | `Color` | `80, 200, 255` | Secondary accent color (cyan) |
| `BackgroundColor` | `Color` | `15, 15, 25, 240` | Menu background (dark with alpha) |
| `LockedColor` | `Color` | `80, 80, 80` | Locked/unavailable nodes |
| `UnlockedColor` | `Color` | `120, 80, 255` | Owned/upgraded nodes |
| `AvailableColor` | `Color` | `80, 200, 255` | Available-to-buy nodes |
| `MaxedColor` | `Color` | `255, 200, 50` | Fully maxed-out nodes |
| `EnableBlur` | bool | `true` | Background blur effect |
| `EnableAnimations` | bool | `true` | Node animations and transitions |
| `EnableSounds` | bool | `true` | Unlock/upgrade sound effects |

---

## Color Guide

| Color | Hex | Usage |
|-------|-----|-------|
| Primary | `#7850FF` | Main UI accent, buttons, headers |
| Secondary | `#50C8FF` | Highlights, active elements |
| Background | `#0F0F19` | Menu background |
| Locked | `#505050` | Gray locked nodes |
| Unlocked | `#7850FF` | Purple owned nodes |
| Available | `#50C8FF` | Cyan purchasable nodes |
| Maxed | `#FFC832` | Gold maxed nodes |

---

## Examples

### Dark mode theme

```lua
SkillTree.Config.Theme = {
    PrimaryColor = Color(180, 60, 255),
    SecondaryColor = Color(60, 180, 255),
    BackgroundColor = Color(5, 5, 15, 250),
    LockedColor = Color(60, 60, 60),
    UnlockedColor = Color(180, 60, 255),
    AvailableColor = Color(60, 180, 255),
    MaxedColor = Color(255, 180, 30),
    EnableBlur = true,
    EnableAnimations = true,
    EnableSounds = true
}
```

### Light theme

```lua
SkillTree.Config.Theme = {
    PrimaryColor = Color(100, 60, 220),
    SecondaryColor = Color(60, 160, 220),
    BackgroundColor = Color(240, 240, 250, 235),
    LockedColor = Color(160, 160, 160),
    UnlockedColor = Color(100, 60, 220),
    AvailableColor = Color(60, 160, 220),
    MaxedColor = Color(220, 160, 30),
    EnableBlur = false,
    EnableAnimations = true,
    EnableSounds = true
}
```

### Disable animations for low-end servers

```lua
SkillTree.Config.Theme.EnableAnimations = false
SkillTree.Config.Theme.EnableBlur = false
```
