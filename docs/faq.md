# FAQ

## General

### What is Skillforge?

Skillforge is a skill tree system for Garry's Mod DarkRP servers. Each DarkRP job can have its own skill tree with branches, nodes, XP, levels, and rewards.

### Do I need DarkRP?

**Yes**, Skillforge is designed specifically for DarkRP servers. While some features work without DarkRP, the full integration (job mapping, XP sources, salary, arrest, etc.) requires DarkRP.

### Does it work with other gamemodes?

The system is built for DarkRP and there are no plans to support other gamemodes natively. However, developers can use the API to create custom integrations.

### How many trees can I have?

Unlimited. Each tree is a JSON file in `data/skillforge/trees/`. The server comes with 9 default trees.

---

## Installation

### How do I install Skillforge?

Follow the [Installation Guide](getting-started/installation.md). You can install via GModStore or manually.

### Does it work on shared hosting?

Yes, Skillforge uses SQLite (built into Garry's Mod) and doesn't require external databases.

### Can I use it without ULX/SAM?

Yes. Permissions work with ULX, SAM, CAM, or a built-in fallback. Without any admin mod, the `IsAdmin()` function is used.

---

## Configuration

### How do I change the open key?

```lua
SkillTree.Config.General.OpenKey = KEY_F5  -- Change to F5
```

### How do I add more skill points per level?

```lua
SkillTree.Config.Leveling.SkillPointsPerLevel = 2
```

### How do I make leveling slower?

```lua
SkillTree.Config.Leveling.BaseXP = 200
SkillTree.Config.Leveling.GrowthMultiplier = 1.20
```

### How do I disable XP for killing NPCs?

```lua
SkillTree.Config.XP.NPCKill.Enabled = false
```

### How do I change the theme color?

```lua
SkillTree.Config.Theme.PrimaryColor = Color(255, 100, 50)
```

---

## Jobs & Trees

### How do I assign a tree to a job?

```lua
SkillTree.Config.JobTreesByName["Police Officer"] = "police_tree"
```

### Can one job have multiple trees?

No, each job maps to exactly one tree. But you can use the hook `SkillTree_GetPlayerTree` for dynamic assignment.

### Can multiple jobs share a tree?

Yes. Multiple job names can map to the same tree.

### How do I create a new tree?

Use the [Visual Editor](visual-editor/index.md) or create a JSON file in `data/skillforge/trees/`.

---

## XP & Progression

### What is the XP formula?

```lua
XPRequired(level) = floor(100 * 1.15^(level-1))
```

### What is the max level?

Default is 100. Configurable via `SkillTree.Config.Leveling.MaxLevel`.

### How do I give XP to a player?

```
skilltree_givexp "Player Name" 500
```

### Does XP carry over between jobs?

It depends on the [Progression Mode](job-system/progression-modes.md):
- **Global**: XP is shared across all jobs
- **Separate**: Each job has its own XP
- **Hybrid**: XP is per-job but level is global

### What is prestige?

Prestige allows max-level players to reset for permanent bonuses (skill points + XP multiplier). See the [Prestige Guide](configuration/prestige.md).

---

## Permissions

### I can't open the admin panel

Make sure you have `superadmin` or `admin` rank, or your SteamID is in `SkillTree.Config.Admin.AllowSteamIDs`.

### How do I give permissions with ULX?

```
!ulx adduser "Player" "skilltree.admin.view"
!ulx adduser "Player" "skilltree.admin.givexp"
```

### What are all the permissions?

There are 12 permissions. See the [Permissions Reference](administration/permissions.md).

---

## Development

### Can I add my own effects?

Not directly in the current version. You can use the `CustomFunction` effect type with a registered callback.

### Can I create custom XP actions?

Yes. Use `SkillTree.RegisterJobXPAction`. See the [Job XP API](developer/job-xp-api.md).

### Can I integrate my own addon?

Yes. Use the [Integration API](developer/integration-api.md) or [Hooks](developer/hooks.md).

### How do I get player data from another addon?

```lua
local level = ply:STN_GetLevel()
local xp = ply:STN_GetXP()
local hasSkill = ply:STN_HasSkill("combat_training")
```

---

## Troubleshooting

### The menu doesn't open

1. Check that DarkRP is installed and loaded
2. Try typing `!skills` in chat
3. Check server console for errors
4. Verify `EnableDarkRP = true` in config

### No trees are showing

1. Run `skilltree_reload_trees` in console
2. Check `data/skillforge/trees/` for JSON files
3. Check validation: `skilltree_validate_trees`

### Players can't unlock skills

1. Check they have enough skill points
2. Check they meet the level requirement
3. Check prerequisites are unlocked
4. Check the job allows the skill

### HUD not showing

```lua
SkillTree.Config.General.EnableHUD = true
```

### Errors in console

Enable debug mode to see detailed logs:
```lua
SkillTree.Config.General.Debug = true
```

---

## Support

### Where can I get help?

- [GitHub Issues](https://github.com/Darvan76/wiki-skillforge/issues)
- [GModStore Page](https://www.gmodstore.com/market/skillforge)

### How do I report a bug?

Open a GitHub issue. Include:
- Server OS
- DarkRP version
- Other addons installed
- Console error logs
- Steps to reproduce
