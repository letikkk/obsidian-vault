---
title: 7 Environmental Layers Biome Checklist
categories:
  - "[[Resources]]"
tags:
  - resource
  - roblox
  - level-design
  - biomes
  - asset-manifest
  - checklist
created: 2026-10-18
status: active
---

# 🌲 Resource: 7 Environmental Layers Biome Checklist

> **The mandatory 18–24 asset archetype manifest checklist to ensure non-sparse, visually rich biomes.**

---

## 📋 The 18–24 Archetype Manifest Matrix

Every biome must verify all 7 layers before level assembly commences:

### Layer 1: Perimeter Enclosure (3–4 Archetypes)
- [ ] `L1_Cliff_Wall_Straight`: Stepped Cartesian cliff bastion (4-stud grid).
- [ ] `L1_Cliff_Corner_90`: 90-degree outer corner bastion.
- [ ] `L1_Cliff_Overhang`: Elevated rock shelf with tactile beveled underside.
- [ ] `L1_Gateway_Pillar`: Gateway buttress or entrance arch post.

### Layer 2: Ground Stratification & Recesses (3 Archetypes)
- [ ] `L2_Floor_Tile_Recessed`: Low-tier ground plate (-1 to -2 studs elevation).
- [ ] `L2_River_Channel` / `L2_Ice_Pond`: Recessed water, ice, or lava basin.
- [ ] `L2_Stepping_Stones`: Ground traversal path markers across channels.

### Layer 3: Hero Geographic Landmarks (1–2 Centerpieces)
- [ ] `L3_Hero_Centerpiece_A`: Primary focal landmark (e.g. Prehistoric Dinosaur Bone Arch, Ancient Altar).
- [ ] `L3_Hero_Centerpiece_B`: Secondary landmark (e.g. Floating Crystal Shrine, Beacon Tower).

### Layer 4: Landmark Flora & Trees (3 Archetypes)
- [ ] `L4_Tree_Large`: Fully grown biome tree (Tiered Snow Pine, Palm, or Saguaro Cactus).
- [ ] `L4_Tree_Medium`: Medium flora variant with altered branch/crown silhouette.
- [ ] `L4_Tree_Young_Stump`: Cut tree stump or young sapling with moss/snow detail.

### Layer 5: Natural Stepped Rock Clusters (3–4 Archetypes)
- [ ] `L5_Rock_Anchor`: Massive primary boulder with stepped terracing.
- [ ] `L5_Rock_Satellite_A`: Medium flanking stone.
- [ ] `L5_Rock_Satellite_B`: Flat angular slab rock.
- [ ] `L5_Rock_Pebble_Scatter`: Ground rock cluster.

### Layer 6: Micro-Scatter & Ground Cover (3–4 Archetypes)
- [ ] `L6_Scatter_Bush`: Round voxel foliage shrub (`CanCollide = false`).
- [ ] `L6_Scatter_Grass_Tuft`: Dense low grass patch (`CanCollide = false`).
- [ ] `L6_Scatter_Flower_Or_Drift`: Biome-specific accent (Wildflower, snow drift, starfish).
- [ ] `L6_Scatter_Biome_Debris`: Twig bunch, seashell, or dry bones.

### Layer 7: Vertical & Atmospheric Accents (2–3 Archetypes)
- [ ] `L7_Vertical_Ceiling_Accent`: Hanging icicles or cave stalactites.
- [ ] `L7_Vertical_Floor_Accent`: Floor crystal spike or wooden lantern post.
- [ ] `L7_Atmospheric_VFX_Chest`: Biome treasure crate or particle emitter origin.

---

## 🎨 Biome Presets & Aesthetic Definitions

| Biome | Flora Theme | Rock Palette | Recessed Channel | Hero Landmark |
| :--- | :--- | :--- | :--- | :--- |
| **Forest** | Deciduous & Oaks | Medium stone grey (`Studs`) | Muddy river bed with pebbles | Ancient Mossy Stone Arch |
| **Snow / Tundra** | Tiered Snow Pines | Slate blue-grey with snow caps | Translucent cyan frozen ice pond | Crystalized Glacier Shrine |
| **Desert / Canyon** | Saguaro Cacti (dual 90° arms) | Reddish brown terracotta strata | Dry cracked canyon bed | Prehistoric Rib Archway |
| **Volcanic** | Burnt Charred Stumps | Basalt black (`Weld` metal sheen) | Glowing Neon orange lava stream | Obsidian Monolith Tower |
| **Safe Zone Hub** | Manicured shrubs & planters | Polished white quartz trim | Stepped water fountain basin | Central Leaderboard Podium |

---

## 🔗 Related Vault Links
- Asset Pipeline Area: [[02 - Areas/Roblox Asset Pipeline|Roblox Asset Pipeline]]
- World Building Area: [[02 - Areas/World Building & Level Design|World Building & Level Design]]
- Blender Recipes: [[03 - Resources/Blender MCP Automation Recipes|Blender MCP Automation Recipes]]
- Active Heist Zones: [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]
