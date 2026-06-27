# Level-Up Effects

When a player levels up, a particle effect is shown to nearby players.

---

## Configuration

```lua title="lua/skillforge/shared/sh_levelup_config.lua"
SkillTree.LevelUpFX = {
    Enabled = true,
    SendDistance = 2500,
    Duration = 1.5,
    ParticleCount = 80,
    RingParticleCount = 48,
    SparkParticleCount = 35,
    Radius = 70,
    Height = 90,
    UseSound = true,
    SoundPath = "garrysmod/save_load1.wav",
    UseScreenFlashForOwner = true,
    UseChatMessage = true,
    Quality = "high",
    Colors = {
        Primary = Color(120, 90, 255),
        Secondary = Color(80, 200, 255),
        Gold = Color(255, 210, 90),
        White = Color(255, 255, 255)
    },
    Effects = {
        default = { primary = Color(120, 90, 255), secondary = Color(80, 200, 255), ring = Color(255, 210, 90) },
        darkrp  = { primary = Color(255, 210, 90), secondary = Color(120, 220, 90), ring = Color(255, 255, 255) },
        combat  = { primary = Color(255, 50, 50),   secondary = Color(255, 120, 0),  ring = Color(255, 180, 0) },
        admin   = { primary = Color(255, 0, 255),   secondary = Color(0, 255, 255),  ring = Color(255, 255, 255) }
    }
}
```

---

## Particle Layers

The effect consists of **5 layers**:

| Layer | Name | Description |
|-------|------|-------------|
| 1 | **Burst** | Initial explosion of particles from the player |
| 2 | **Ring** | Expanding ring that radiates outward |
| 3 | **Rising** | Particles that float upward from the player |
| 4 | **Sparks** | Small spark particles that fly outward |
| 5 | **Aura** | Glowing aura that fades out around the player |

---

## Visual Quality

| Quality | Particles | Best For |
|---------|-----------|----------|
| `"low"` | Reduced count | Low-end servers/PCs |
| `"medium"` | Balanced | Mid-range systems |
| `"high"` | Full effect | High-end servers |

---

## Effect Variants

Four effect color variants are available:

| Variant | Purpose | Primary Color |
|---------|---------|---------------|
| `default` | Standard level-up | Purple |
| `darkrp` | DarkRP-themed | Gold/Green |
| `combat` | Combat-themed | Red/Orange |
| `admin` | Admin-themed | Magenta/Cyan |

---

## Sound

A sound plays when leveling up:

```lua
SkillTree.LevelUpFX.UseSound = true
SkillTree.LevelUpFX.SoundPath = "garrysmod/save_load1.wav"
```

## Client Effects

- **Screen Flash** — Brief white flash for the leveling-up player
- **Chat Message** — Notification in chat: "You reached level X!"
