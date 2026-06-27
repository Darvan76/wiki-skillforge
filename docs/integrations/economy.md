# Economy Integration

Public API for Gun Dealers and Cooks.

---

## How It Works

The economy integration provides APIs for weapon sales, ammo sales, and food-related actions.

---

## Gun Dealer API

### Report Weapon Sold

Call this when a gun dealer sells a weapon to another player:

```lua
SkillTree.ReportWeaponSold(dealer, buyer, weaponClass)

-- Example:
function SellWeapon(dealer, buyer, weapon)
    -- Your sale logic
    dealer:addMoney(price)
    buyer:Give(weapon)
    SkillTree.ReportWeaponSold(dealer, buyer, weapon)
end
```

### Report Ammo Sold

Call this when a gun dealer sells ammunition:

```lua
SkillTree.ReportAmmoSold(dealer, buyer, ammoType)

-- Example:
function SellAmmo(dealer, buyer, ammoType, amount)
    -- Your ammo sale logic
    dealer:addMoney(amount * ammoPrice)
    buyer:GiveAmmo(amount, ammoType)
    SkillTree.ReportAmmoSold(dealer, buyer, ammoType)
end
```

---

## Cook API

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
| `merchant_sell_weapon` | Sell weapon | 50 | 10s |
| `merchant_sell_ammo` | Sell ammo | 15 | 3s |
| `cook_food` | Cook food | 20 | 3s |
| `cook_sell` | Sell food | 30 | 5s |

---

## Related Configuration

```lua
SkillTree.Config.JobXP["Gun Dealer"] = {
    SellWeapon = { Enabled = true, XP = 50, Cooldown = 15, PreventFarmSamePlayer = true },
    SellAmmo = { Enabled = true, XP = 15, Cooldown = 5 }
}

SkillTree.Config.JobXP["Cook"] = {
    CookFood = { Enabled = true, XP = 20, Cooldown = 5 },
    SellFood = { Enabled = true, XP = 30, Cooldown = 10 }
}
```
