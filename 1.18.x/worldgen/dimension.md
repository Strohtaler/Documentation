---
layout: page
title: "Dimension"
permalink: /1.18.x/worldgen/dimension/
---

In order to modify the `TerraFirmaCraft` world preset, it is necessary to override the vanilla overworld dimension (`data/minecraft/dimension/overworld.json`). The format of a dimension can be found [here](https://minecraft.fandom.com/wiki/Custom_dimension#Dimension_syntax). Included here is [an example](#example) of an override for the vanilla overworld, with TFC properties set to defaults.

Configuration:

- `type` is the namespaced ID of the [dimension type](https://minecraft.fandom.com/wiki/Custom_dimension#Dimension_type). The default is `minecraft:overworld`.
- `generator` is an object:
    - `type` is the namespaced ID of the chunk generator. It must be `tfc:overworld`.
    - `seed` is an optional `long` (Default: `0`). It is the seed of the world.
    - `noise_settings` is the [noise settings](https://minecraft.fandom.com/wiki/Custom_world_generation#Noise_settings) used in the chunk generator. The default is `minecraft:overworld`.
    - `flat_bedrock` is a `boolean`. It controls if the bottom layer of bedrock in the world is flat.
    - `biome_source` is an object:
        - `type` is the namespaced ID of the biome source. It must be `tfc:overworld`.
        - `seed` is an optional `long` (Default: `0`). It is the seed used for the biome source.
        - `spawn_distance` is an integer. It is the farthest distance away from the spawn center location the player is allowed to spawn.
        - `spawn_center_x` is an integer. It is the center x position that the player tries to spawn at.
        - `spawn_center_z` is an integer. It is the center z position that the player tries to spawn at.
        - `rock_layer_settings` is a [rock layer settings](#rock-layer-settings), which describes the rock layers of the world.
        - `temperature_settings` is a [climate settings](#climate-settings), which describes the temperature settings of the world.
        - `rainfall_settings` is a [climate settings](#climate-settings), which describes the rainfall settings of the world.
- `forge:use_server_seed` is a `boolean`. If true, this dimension will ignore the `seed` property specified above in the generator and biome source fields, and instead use the seed from either `server.properties` (if on a server), or the create world screen (if on a client).


#### Example

This is an example `overworld.json` override, with the default values used by TFC.

File: `data/minecraft/dimension/overworld.json`
```json
{
  "type": "minecraft:overworld",
  "generator": {
    "type": "tfc:overworld",
    "noise_settings": "minecraft:overworld",
    "flat_bedrock": false,
    "biome_source": {
      "type": "tfc:overworld",
      "spawn_distance": 8000,
      "spawn_center_x": 0,
      "spawn_center_z": 0,
      "rock_layer_settings": {
        "rock_layer_scale": 128,
        "rocks": [
          "tfc:chalk",
          "tfc:chert",
          "tfc:claystone",
          "tfc:conglomerate",
          "tfc:dolomite",
          "tfc:limestone",
          "tfc:shale",
          "tfc:gneiss",
          "tfc:marble",
          "tfc:phyllite",
          "tfc:quartzite",
          "tfc:schist",
          "tfc:slate",
          "tfc:diorite",
          "tfc:gabbro",
          "tfc:granite",
          "tfc:andesite",
          "tfc:basalt",
          "tfc:dacite",
          "tfc:rhyolite"
        ]
      },
      "temperature_settings": "tfc:default",
      "rainfall_settings": "tfc:default"
    }
  },
  "forge:use_server_seed": true
}
```

### Rock Layer Settings

This describes the rocks, and rock layers, as used during world generation. It must be an object, with the following fields.

Configuration:

- `rock_layer_scale` is an positive integer. It is a multiplier on how far apart rock regions are, in blocks. It must be a power of two. The default is 128.
- `rocks` is an array of rock presets, or rock definitions. Rock presets are rocks that are provided via TFC, or addons, and consist of the id name of the rock (i.e. `tfc:basalt`). Rock definitions are an object, which consist of a custom defined rock, by stating what blocks should be used for various rock states. A rock definition must have the following fields:
    - `id` is the namespaced ID of the rock.
    - `raw` is the block ID of the rock's raw block.
    - `hardened` is the block ID of the rock's hardened block.
    - `gravel` is the block ID of the rock's gravel block.
    - `cobble` is the block ID of the rock's cobblestone block.
    - `sand` is the block ID of the rock's sand block.
    - `sandstone` is the block ID of the rock's sandstone block.
    - `spike` is an optional block ID of the rock's spike block. This must be a TFC-like rock spike block.
    - `loose` is an optional block ID of the rock's loose rock block. This must be a TFC-like loose rock block.
    - `top_layer` is a boolean. If true, this rock will generate in the top rock layer.
    - `middle_layer` is a boolean. If true, this rock will generate in the middle rock layer.
    - `bottom_layer` is a boolean. If true, this rock will generate in the bottom rock layer.

#### Presets

TFC adds the following rock presets, which can be used in the above `rocks` array:

- `tfc:chalk`, `tfc:chert`, `tfc:claystone`, `tfc:conglomerate`, `tfc:dolomite`, `tfc:limestone`, `tfc:shale`, `tfc:gneiss`, `tfc:marble`, `tfc:phyllite`, `tfc:quartzite`, `tfc:schist`, `tfc:slate`, `tfc:diorite`, `tfc:gabbro`, `tfc:granite`, `tfc:andesite`, `tfc:basalt`, `tfc:dacite`, `tfc:rhyolite`

#### Example

This is an example rock settings, which can be used instead of a preset string:

```json
{
  "id": "basalt",
  "raw": "tfc:rock/raw/basalt",
  "hardened": "tfc:rock/hardened/basalt",
  "gravel": "tfc:rock/gravel/basalt",
  "cobble": "tfc:rock/cobble/basalt",
  "sand": "tfc:sand/red",
  "sandstone": "tfc:raw_sandstone/red",
  "top_layer": true,
  "middle_layer": true,
  "bottom_layer": false
}
```

### Climate Settings

This ia an object which controls various climate related parameters about the world, either as rainfall, or temperature. The climate settings defines the base climate generation of the world. This includes the climate scale (how far apart 'peaks' are, i.e. for lines of latitude), and if the climate model should by cyclical (with repeating peaks of max and min areas), or endless (with a moderate equator and 'infinite' peaks).

It can be either a climate preset or a custom climate settings definition. A climate preset consists of the string climate settings preset identifier, as provided by TFC or addons. A climate settings definition consists of an object with the following parameters.

Configuration:

- `scale` is an integer, which represents how far apart peaks are.
- `endless_poles` is a boolean, which when true, will cause the peak regions to be endless rather than cyclical.

#### Presets

In addition to the above object, the string `tfc:default` can be used anywhere a climate settings is needed, which uses the below default values.


#### Example

This is a climate settings, using the same values as `tfc:default`:

```json
{
  "scale": 20000,
  "endless_poles": false
}
```
