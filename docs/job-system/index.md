# Job System

The job system is the bridge between DarkRP jobs and Skillforge trees. It controls:

- **Which tree** each job uses
- **How progression** works (shared or per-job)
- **What XP actions** each job can perform
- **What skills** each job can unlock

---

## Key Concepts

<div class="grid cards" markdown>

-   :material-source-branch: **Progression Modes**  
    Choose between Global, Separate, or Hybrid progression.

-   :material-map: **Job-Tree Mapping**  
    4 different ways to assign trees to jobs.

-   :material-chart-bell-curve: **Job XP Config**  
    Per-action XP with cooldowns, anti-farm, and limits.

-   :material-lock: **Allowed Skills**  
    Restrict specific skills to specific jobs.

</div>

---

## Configuration Files

| File | Location | Purpose |
|------|----------|---------|
| `sh_job_config.lua` | `lua/skillforge/shared/` | Job-tree mappings, progression mode, per-job XP |
| `sh_config.lua` | `lua/skillforge/` | `ActiveTrees`, `JobSkills` |

---

## Quick Start

### Map a job to a tree

```lua
SkillTree.Config.JobTreesByName["Police Officer"] = "police_tree"
```

### Set progression to per-job

```lua
SkillTree.Config.JobProgression.Mode = "separate"
```

### Add XP for a job action

```lua
SkillTree.Config.JobXP["Police Officer"] = {
    ArrestPlayer = { Enabled = true, XP = 100, Cooldown = 30 }
}
```

---

## Related Pages

- [Progression Modes](progression-modes.md) — Deep dive into global/separate/hybrid
- [Job-Tree Mapping](job-tree-mapping.md) — All mapping methods explained
- [Job XP Config](job-xp-config.md) — Configuring XP per action
- [Allowed Skills](allowed-skills.md) — Restricting skills by job
