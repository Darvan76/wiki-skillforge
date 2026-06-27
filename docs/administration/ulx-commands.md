# ULX Commands

11 ULX chat commands for easy administration of Skillforge.

---

## Command List

| Command | Syntax | Permission | Description |
|---------|--------|-----------|-------------|
| `!givexp` | `!givexp <players> <amount>` | SuperAdmin | Give XP to players |
| `!takexp` | `!takexp <players> <amount>` | SuperAdmin | Take XP from players |
| `!setlevel` | `!setlevel <players> <level>` | SuperAdmin | Set player level |
| `!givepoints` | `!givepoints <players> <amount>` | SuperAdmin | Give skill points |
| `!resetskills` | `!resetskills <players>` | SuperAdmin | Reset player skills |
| `!unlockskill` | `!unlockskill <player> <skillID>` | SuperAdmin | Force unlock skill |
| `!lockskill` | `!lockskill <player> <skillID>` | SuperAdmin | Force lock skill |
| `!setprestige` | `!setprestige <player> <level>` | SuperAdmin | Set prestige level |
| `!givejobxp` | `!givejobxp <players> <amount> <job>` | SuperAdmin | Give job XP |
| `!setjoblevel` | `!setjoblevel <players> <level> <job>` | SuperAdmin | Set job level |
| `!resetjobtree` | `!resetjobtree <player> <job>` | SuperAdmin | Reset job tree |

---

## Detailed Reference

### !givexp

```
!givexp @me 500        → You receive 500 XP
!givexp @all 100       → Everyone receives 100 XP
!givexp "John" 250     → John receives 250 XP
```

### !setlevel

```
!setlevel @me 25       → Your level is set to 25
!setlevel "John" 50    → John's level is set to 50
```

### !givepoints

```
!givepoints @me 5      → You receive 5 skill points
!givepoints @all 3     → Everyone receives 3 skill points
```

### !resetskills

```
!resetskills @me       → Your skills are reset
!resetskills "John"    → John's skills are reset
```

### !unlockskill / !lockskill

```
!unlockskill "John" "combat_training"  → Force unlock combat_training
!lockskill "John" "combat_training"    → Force lock combat_training
```

### !givejobxp

```
!givejobxp @me 500 "Civil Protection"  → Give 500 job XP
!givejobxp "John" 200 "Medic"          → Give 200 Medic XP
```

### !setjoblevel

```
!setjoblevel @me 10 "Garbage Collector"
!setjoblevel "John" 5 "Police Chief"
```

### !resetjobtree

```
!resetjobtree @me "Thief"
!resetjobtree "John" "Medic"
```

---

## ULX Log Messages

All ULX commands generate fancy admin log messages:

```
#A gave #i XP to #T
#A set the level of #T to #i
#A reset the skill tree of #T
#A unlocked skill #s for #T
#A gave #i XP to #T on job #s
```
