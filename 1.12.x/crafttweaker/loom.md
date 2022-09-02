---
layout: page
title: "Loom"
permalink: /1.12.x/crafttweaker/loom/
excluded_in_search: true
---

# Loom Recipes

Loom recipe manager has three methods for recipe manipulation:

```zenscript
// Import Loom methods into your script
import mods.terrafirmacraft.Loom;
// Adds a recipe with the given parameters
Loom.addRecipe(String registryName, IIngredient input, IItemStack output, int steps, String loomTexture)
// Removes all recipes that have a given output
Loom.removeRecipe(IItemStack output)
// Removes all recipes that have a given output
Loom.removeRecipe(String registryName)
```

Arguments:

- `steps` is the number of steps needed to complete the recipe. It's the number of times the player has to click the loom, each movement of the loop advances one step. Within TFC, this is the same as the number of items required for the recipe, but it is not required to be so.
- `loomTexture` is a path (`ResourceLocation`) to a texture file, to be used to display on the loom in the world.(For example, `"minecraft:textures/blocks/wool_colored_white.png"` references the vanilla texture for white wool). If you are using custom textures you need some form of data/resource loading (read: a resource pack) for this to be able to reference your texture correctly.
