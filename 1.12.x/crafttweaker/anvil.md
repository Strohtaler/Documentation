---
layout: page
title: "Anvil Recipes"
permalink: /1.12.x/crafttweaker/anvil/
---

# Anvil Recipes

The Anvil has three methods for manipulating recipes:

```zenscript
// Import anvil methods into your script
import mods.terrafirmacraft.Anvil;
// Adds a recipe with the given parameters
Anvil.addRecipe(String registryName, IIngredient input, IItemStack output, int minTier, String skillType, String... forgeRules);
// Removes all recipes that have a given output
Anvil.removeRecipe(IItemStack output);
// Removes a single recipe by registry name
Anvil.removeRecipe(String registryName);
```

Important things to note:

- Input can't be stacked. Anvils only accept one item per slot.
- input must be forgeable (please refer to [item capabilities](../items/) for registering forging capability to an item).
- Tiers are 0 = Stone, 1 = Copper, 2 = Bronze, 3 = Wrought Iron, 4 = Steel, 5 = Black Steel and 6 = Red/Blue Steel.
- Skill type is what category of skill the forging should contribute to. Valid entries are `general`, `tools`, `weapons`, `armor`, or null. If the skill type is `tools`, `weapons`, or `armor` then the result item will have a skill bonus applied to it.
- A recipe must have 1, 2 or 3 rules. Rules consist of a type (`HIT`, `DRAW`, `PUNCH`, `BEND`, `UPSET`, or `SHRINK`), followed by an order (`ANY`, `NOT_LAST`, `LAST`, `SECOND_LAST`, `THIRD_LAST`), separated by an underscore. As example, `HIT_ANY`, `DRAW_SECOND_LAST`, and `UPSET_NOT_LAST` are valid rule names.
