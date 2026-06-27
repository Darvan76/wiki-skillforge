# Branches

Branches group related skills into categories within a tree.

---

## Branch Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | string | ✅ | Unique branch identifier |
| `name` | string | ✅ | Display name |
| `description` | string | ✅ | Branch description (shown in tooltip) |
| `color` | string | ✅ | Hex color (e.g. `"#38bdf8"`) |
| `icon` | string | ✅ | Path to icon material |

---

## Example: Police Tree Branches

```json
{
    "branches": {
        "arrests": {
            "id": "arrests",
            "name": "Arrests",
            "description": "Capture efficiency, cooldown reduction, and rewards for bringing criminals to justice.",
            "color": "#38bdf8",
            "icon": "../../materials/skilltree_nexus/icons/icon_handcuffed.png"
        },
        "defense": {
            "id": "defense",
            "name": "Defense",
            "description": "Combat training, damage resistance, and armor for high-risk situations.",
            "color": "#ef4444",
            "icon": "../../materials/skilltree_nexus/icons/icon_shield.png"
        },
        "investigation": {
            "id": "investigation",
            "name": "Investigation",
            "description": "Search techniques, confiscation, and evidence analysis.",
            "color": "#a78bfa",
            "icon": "../../materials/skilltree_nexus/icons/icon_magnifying.png"
        },
        "tactical": {
            "id": "tactical",
            "name": "Tactical",
            "description": "Specialized equipment, operational mobility, and emergency response.",
            "color": "#22c55e",
            "icon": "../../materials/skilltree_nexus/icons/icon_riot_shield.png"
        }
    }
}
```

---

## Icon Paths

Icons are located in `materials/skilltree_nexus/icons/`. There are **64 icons** available:

| Icon | Path |
|------|------|
| Combat | `icon_combat.png` |
| Shield | `icon_shield.png` |
| Arrest | `icon_arrest.png` |
| Handcuffed | `icon_handcuffed.png` |
| Magnifying | `icon_magnifying.png` |
| Runner | `icon_runner.png` |
| Coins | `icon_coins.png` |
| Healing | `icon_healing.png` |
| Lockpick | `icon_lockpicking.png` |
| Recycle | `icon_recycle.png` |
| ...and 54 more | |

Icon paths are auto-sanitized during load:
- Backslashes → forward slashes
- `.jpg` → `.png`
- `icon_speed.png` → `icon_runner.png`
- `icon_money.png` → `icon_coins.png`
