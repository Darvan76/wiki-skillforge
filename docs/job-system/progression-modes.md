# Progression Modes

Skillforge supports three progression modes that determine how levels, XP, and skill points are managed across jobs.

---

## Configuration

```lua title="lua/skillforge/shared/sh_job_config.lua"
SkillTree.Config.JobProgression = {
    Mode = "separate",
    SaveJobXP = true,
    SaveJobSkills = true,
    SharedSkillPoints = false,
    AllowGlobalTree = true,
    AllowJobTrees = true
}
```

---

## Mode Comparison

| Feature | Global | Separate | Hybrid |
|---------|--------|----------|--------|
| **Level** | Shared across all jobs | Per-job | Shared |
| **XP** | Single XP pool | Per-job XP | Per-job but affects global level |
| **Skill Points** | Shared pool | Per-job pool | Can be shared or separate |
| **Skill Tree** | Same tree always | Different per job | Different per job |
| **Best for** | Simple servers | Thematic RPG | Balanced approach |

---

## Global Mode

Everything is shared. A player has one level, one XP bar, and one set of skills regardless of job.

```lua
SkillTree.Config.JobProgression.Mode = "global"
```

**Use case**: Servers where skills are character-bound, not job-bound.

---

## Separate Mode (Default)

Each job has its own level, XP, skill points, and unlocked skills.

```lua
SkillTree.Config.JobProgression.Mode = "separate"
```

**Use case**: Thematic progress — a Police Officer levels up their police tree, a Criminal levels up their criminal tree.

**How data is stored**:

```
skilltree_job_progress table:
├── steamid64
├── job_id          ← "Civil Protection", "Medic", etc.
├── level           ← Job-specific level
├── xp              ← Job-specific XP
├── skill_points    ← Job-specific skill points
└── skills_json     ← Job-specific unlocked skills
```

When a player switches jobs, their previous job progress is saved and the new job's progress is loaded.

---

## Hybrid Mode

Level is global, but XP is earned separately per job. Skill points can be shared.

```lua
SkillTree.Config.JobProgression.Mode = "hybrid"
```

**Use case**: Servers that want job-specific XP grinding but a global sense of progression.

---

## Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `Mode` | string | `"separate"` | `"global"`, `"separate"`, or `"hybrid"` |
| `SaveJobXP` | bool | `true` | Persist job-specific XP data |
| `SaveJobSkills` | bool | `true` | Persist job-specific skill unlocks |
| `SharedSkillPoints` | bool | `false` | Share skill points across jobs (separate mode) |
| `AllowGlobalTree` | bool | `true` | Allow a global fallback tree |
| `AllowJobTrees` | bool | `true` | Allow job-specific trees |
