# Localization

Skillforge supports multiple languages with an extensible translation system.

---

## Configuration

```lua
SkillTree.Config.Language = "es"  -- Default language code
```

---

## Available Languages

| Code | Language | Strings |
|------|----------|---------|
| `en` | English | 172 |
| `es` | Spanish | 172 |
| `fr` | French | 172 |

---

## How It Works

Translations are stored in `SkillTree.Languages[code]` and retrieved via:

```lua title="lua/skillforge/sh_language.lua"
function SkillTree.Lang(key, ...)
    local lang = SkillTree.Config.Language or "en"
    if not SkillTree.Languages[lang] then lang = "en" end
    local str = SkillTree.Languages[lang][key] or SkillTree.Languages.en[key] or key
    if select('#', ...) > 0 then
        return string.format(str, ...)
    end
    return str
end
```

If a key is missing in the selected language, it falls back to English.

---

## Language String Keys

### Menu

| Key | English | Spanish |
|-----|---------|---------|
| `MenuTitle` | "Skillforge" | "Skillforge" |
| `Level` | "Level" | "Nivel" |
| `XP` | "XP" | "XP" |
| `SkillPoints` | "Skill Points" | "Puntos de habilidad" |
| `Unlock` | "Unlock" | "Desbloquear" |
| `Upgrade` | "Upgrade" | "Mejorar" |

### HUD

| Key | English | Spanish |
|-----|---------|---------|
| `HUD_Level` | "LEVEL" | "NIVEL" |
| `HUD_PressKey` | "PRESS %s TO OPEN MENU" | "PULSA %s PARA ABRIR MENÚ" |

### Notifications

| Key | English | Spanish |
|-----|---------|---------|
| `Notif_XPGained` | "+%d XP (%s)" | "+%d XP (%s)" |
| `Notif_SkillUnlocked` | "Unlocked: %s (Rank %d)" | "Desbloqueado: %s (Rango %d)" |

### Admin

| Key | English | Spanish |
|-----|---------|---------|
| `Admin_XPGiven` | "You gave %d XP to %s." | "Le has dado %d XP a %s." |
| `Admin_TreeReset` | "%s's skill tree has been reset." | "Árbol de %s reiniciado con éxito." |

---

## Adding a New Language

To add German (`de`), extend `SkillTree.Languages`:

```lua title="lua/autorun/skillforge_german.lua"
local function AddGerman()
    if not SkillTree or not SkillTree.Languages then
        timer.Simple(1, AddGerman)
        return
    end

    SkillTree.Languages["de"] = {
        MenuTitle = "Skillforge",
        Level = "Stufe",
        XP = "EP",
        SkillPoints = "Fertigkeitenpunkte",
        Unlock = "Freischalten",
        Upgrade = "Verbessern",
        -- ... translate all 172 strings
    }
end
AddGerman()
```

Then set the language:

```lua
SkillTree.Config.Language = "de"
```

---

## Full Language String List

All available keys can be found in `lua/skillforge/sh_language.lua`. The file contains 172 keys organized into sections:

- Menu strings (15 keys)
- HUD strings (6 keys)
- Level-up banner (3 keys)
- Notifications (3 keys)
- Admin panel (35 keys)
- Editor (7 keys)
- Actions (3 keys)
- ULX permissions (12 keys)
- ULX help (11 keys)
- ULX hints (4 keys)
- ULX logs (11 keys)
- Errors (6 keys)
