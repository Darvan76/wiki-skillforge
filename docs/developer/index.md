# Developer Reference

Complete reference for integrating Skillforge with other addons and creating custom functionality.

---

## Available Systems

<div class="grid cards" markdown>

-   :material-code-json: **API Reference**  
    30+ public functions for XP, skills, trees, players, and utilities.

-   :material-account: **Player Methods**  
    8 methods added to the Player metatable (`STN_*`).

-   :material-hook: **Hooks**  
    11 custom hooks fired throughout the system.

-   :material-function: **Callbacks**  
    Register custom Lua functions that execute when skills are upgraded.

-   :material-briefcase: **Job XP API**  
    Register custom job XP actions and give XP from any code.

-   :material-api: **Integration API**  
    12 public API functions for job-specific integrations.

-   :material-puzzle: **Custom Integration**  
    Build a complete integration for a custom job.

-   :material-file-code: **Examples**  
    15 complete, copy-paste ready examples.

</div>

---

## Namespace

```lua
SkillTree           -- Main global table
SkillTree.Config    -- Configuration
SkillTree.Trees     -- Loaded tree data
SkillTree.PlayerData -- Player progression data
SkillTree.DB        -- Database operations
SkillTree.Net       -- Network messaging
SkillTree.XP        -- XP engine
SkillTree.Admin     -- Admin functions
SkillTree.DarkRP    -- DarkRP integration
```

## Quick Links

- [API Reference](api-reference.md)
- [Player Methods](player-methods.md)
- [Hooks](hooks.md)
- [Callbacks](callbacks.md)
- [Job XP API](job-xp-api.md)
- [Integration API](integration-api.md)
- [Custom Integration](custom-integration.md)
- [Examples](examples.md)
