# Food Integration

Automated XP hooks and public API for Cook jobs.

---

## How It Works

The food integration awards job XP when cooks prepare food or sell food to another player. It is useful for DarkRP cook jobs and for custom food systems that do not use the default DarkRP entities.

---

## Public API

### Report Food Cooked

Call this when a cook prepares a food item:

```lua
SkillTree.ReportFoodCooked(cook, foodClass)

-- Example:
function CookFood(cook, foodItem)
    -- Your cooking logic
    cook:Give(foodItem)
    SkillTree.ReportFoodCooked(cook, foodItem)
end
```

### Report Food Sold

Call this when a cook sells food to another player:

```lua
SkillTree.ReportFoodSold(cook, buyer, foodClass)

-- Example:
function SellFood(cook, buyer, foodItem, price)
    cook:addMoney(price)
    buyer:Give(foodItem)
    SkillTree.ReportFoodSold(cook, buyer, foodItem)
end
```

---

## XP Actions

| Action ID | Description | Default XP | Cooldown |
|-----------|-------------|------------|----------|
| `cook_food` | Cook food | 20 | 3s |
| `cook_sell` | Sell food | 30 | 5s |

---

## Related Configuration

```lua
SkillTree.Config.JobXP["Cook"] = {
    CookFood = { Enabled = true, XP = 20, Cooldown = 5 },
    SellFood = { Enabled = true, XP = 30, Cooldown = 10 }
}
```

## Related Pages

- [Economy Integration](economy.md) — commercial APIs for Gun Dealer and Cook jobs.
- [Job XP Config](../job-system/job-xp-config.md) — default XP values and cooldowns.
