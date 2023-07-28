# LS-B Documentation

## Table of Contents

1. [Installation](#installation)
2. [Usage](#usage)
   - [Creating a Loot System](#creating-a-loot-system)
   - [Adding Tiers](#adding-tiers)
   - [Removing Tiers](#removing-tiers)
   - [Generating Loot](#generating-loot)
   - [Debug Mode](#debug-mode)
   - [Special Loot Events](#special-loot-events)
3. [Examples](#examples)

## Installation
N/A (Unreleased)

## Usage
# Creating a Loot System
To create a new instance of the Loot System, call the new function:
```lua
local lootSystem = LootSystem.new()
```
# Adding Tiers
Use the 'AddTier' function to define new loot tiers with specific probabilities and abilities:
```lua
lootSystem:AddTier(tierName, chance, abilities)
```

* tierName (string): The name of the new tier.
* chance (number): The probability of this tier to be selected (in percentage).
* abilities (table, optional): A table containing the abilities for this tier. Default is an empty table.
 # Removing Tiers
You can remove an existing loot tier by its name using the removeTier function:
```lua
lootSystem:removeTier(tierName)
```
* tierName (string): The name of the tier to be removed.
  # Generating Loot
  To generate loot items, call the giverandomTier function:
  ```lua
  local tier = lootSystem:giverandomTier()
  if tier then
	local ability = lootSystem:generateAbility(tier)
	if ability then
		-- Handle the generated loot item
	  end
  end
  ```
  # Debug Mode
  The debug mode allows you to test and analyze the loot generation. Use the runDebugMode function to enable the debug mode:
  ```lua
  lootSystem:runDebugMode(iterations, enableDebugOutput)
  ```
*  iterations (number, optional): The number of loot generations to perform in debug mode. Default is 100.
*  enableDebugOutput (boolean, optional): Whether to print debug information during the debug mode. Default is true.
# Examples
```lua
local LootSystem = require(game.ServerScriptService.LootSystem)

local lootSystem = LootSystem.new()

-- Adding loot tiers
lootSystem:AddTier("Common", 20, {"Potion", "Gold", "Scroll"})
lootSystem:AddTier("Rare", 10, {"Magic Ring", "Enchanted Sword"})
lootSystem:AddTier("Epic", 5, {"Legendary Armor", "Mythical Staff"})
lootSystem:AddTier("Legendary", 2, {"Dragon Scale", "Divine Amulet"})
lootSystem:AddTier("Mythical", 1, {"Ultimate Artifact"})

-- Generate loot items
for i = 1, 10 do
    local tier = lootSystem:giverandomTier()
    if tier then
        local ability = lootSystem:generateAbility(tier)
        if ability then
            print("Tier:", tier)
            print("Ability:", ability)
            print("------------------")
        end
    end
}

-- Run debug mode
lootSystem:runDebugMode(100, false)

-- Remove a tier
lootSystem:removeTier("Mythical")
```
