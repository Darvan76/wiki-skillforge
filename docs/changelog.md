# Changelog

## v1.0.0 — Initial Release

### Core System
- Complete skill tree framework with tree, branch, and node management
- 28 passive and active effect types
- JSON-based tree definitions with validation
- Player metatable extensions (8 `STN_*` methods)
- SQLite persistence with auto-migration

### XP & Leveling
- Exponential XP formula: `floor(BaseXP * GrowthMultiplier^(level-1))`
- 7 XP sources: playtime, player kills, NPC kills, money, arrest, heal, sell
- XP multiplier system from skills and buffs
- Level-up bonus points and milestone rewards
- Anti-exploit: rate limiting, AFK detection, per-minute caps, anti-farming

### DarkRP Integration
- Salary multiplier
- Money gain XP and money multiplier
- Arrest XP (normal + wanted bonus)
- Job change XP bonus
- Shop discounts (entities and vehicles)
- Heal XP
- Printer money bonus

### Job System
- 3 progression modes: Global, Separate, Hybrid
- 4 job-to-tree mapping methods: TEAM enum, job name, category, callback
- Per-job XP configuration with cooldowns and limits
- Job skill restrictions via whitelist

### Job Integrations
- **Police**: Arrests, weapon confiscation, contraband confiscation
- **Medic**: Heal (per-HP), revive
- **Criminal**: Lockpicking, robberies, printer theft
- **Economy**: Weapon sales, ammo sales
- **Food**: Cooking, selling
- **Garbage**: Collection, recycling, delivery, routes

### Default Trees (9)
- `darkrp_default` — 8 branches, ~48 nodes (RPG core)
- `police_tree` — 4 branches, 12 nodes
- `medic_tree` — 4 branches, 12 nodes
- `garbage_tree` — 4 branches, 12 nodes
- `criminal_tree` — 4 branches, 12 nodes
- `gun_dealer_tree` — 4 branches, 12 nodes
- `citizen_tree` — 4 branches, 12 nodes
- `economy_tree` — 4 branches, 12 nodes
- `cook_tree` — 4 branches, 12 nodes

### Administration
- 12 granular permissions
- 20+ console commands
- 11 ULX commands
- Full HTML admin panel (dashboard, players, logs, backups, analytics)
- SQLite admin action logs
- Tree backup and restore system

### UI/UX
- HTML/DHTML skill tree menu
- Draggable HUD with level, XP bar, skill points
- XP gain floaters
- Level-up banner
- Toast notification system
- Scoreboard level display
- Visual tree editor (zoom, pan, connections)

### Visual Effects
- 5-layer level-up particle system (burst, ring, rising, sparks, aura)
- 4 effect variants (default, darkrp, combat, admin)
- Configurable quality levels
- Screen flash and sound effects
- Resolution-independent scaling

### Developer Features
- 30+ public API functions
- 11 custom hooks
- Callback registration system with security
- Job XP action registration API
- 12 integration API functions
- Language system (EN, ES, FR — 172 strings each)
- Extensive security scanning for tree JSON files
- Automatic cycle detection in prerequisites

### Miscellaneous
- Prestige system (10 levels)
- Daily missions system
- Achievement system
- Auto-save with configurable interval
- Player disconnect cleanup
- Debug mode for development
