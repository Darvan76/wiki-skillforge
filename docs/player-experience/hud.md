# HUD

The on-screen HUD shows the player's level, XP, and skill points.

---

## Configuration

```lua
SkillTree.Config.General.EnableHUD = true  -- Enable/disable the HUD
```

---

## HUD Elements

The HUD displays:

1. **Level** — Current player level (top section)
2. **Experience** — Current XP and XP required for next level (middle)
3. **XP Bar** — Progress bar showing XP completion percentage
4. **Skill Points** — Available skill points (bottom)
5. **Key Hint** — "PRESS F6 TO OPEN MENU" (shown when menu is closed)

---

## HUD Scaling

The HUD supports four scale levels controlled by a client setting:

```lua title="lua/skillforge/cl_hud.lua"
local scales = {
    ["08"] = 0.8,  -- Small
    ["10"] = 1.0,  -- Normal (default)
    ["12"] = 1.2,  -- Large
    ["14"] = 1.4   -- Extra Large
}
```

### Font Sizes

| Element | Small (0.8) | Normal (1.0) | Large (1.2) | XL (1.4) |
|---------|-------------|--------------|-------------|----------|
| Level text | 19px | 24px | 29px | 34px |
| Label text | 10px | 12px | 14px | 17px |
| XP text | 11px | 14px | 17px | 20px |

---

## Draggable HUD

The HUD can be repositioned by dragging:

1. Click and hold on the HUD
2. Drag to desired position
3. Release — position is saved automatically via `SkillTree.SaveClientSettings()`

---

## HUD Color

The HUD uses the configurable theme colors:

```lua
SkillTree.Config.Theme.PrimaryColor      -- Main border/accent
SkillTree.Config.Theme.SecondaryColor    -- XP bar fill
```

---

## Floaters

XP gain floaters appear near the HUD when XP is earned:

```lua title="lua/skillforge/cl_hud.lua"
surface.CreateFont("stn_floater_large", {
    font = "Roboto",
    size = math.Round(SkillTree.ScreenScale(28)),
    weight = 900,
})
```

Floaters display: `+50 XP (Arrest)` with a fade-out animation.

---

## Level-Up Banner

When a player levels up, a full-screen banner appears:

```
╔══════════════════════════╗
║      LEVEL UP!          ║
║  YOU REACHED LEVEL 15   ║
║  +1 SKILL POINT AWARDED ║
╚══════════════════════════╝
```

---

## Disabling the HUD

If you want to use a custom HUD or remove it entirely:

```lua
SkillTree.Config.General.EnableHUD = false
```

This disables all HUD elements including floaters, XP bar, and level-up banner.
