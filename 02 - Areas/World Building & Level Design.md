---
title: World Building & Level Design
categories:
  - "[[Areas]]"
tags:
  - area
  - roblox
  - level-design
  - world-building
  - spatial-math
created: 2026-10-18
status: active
---

# 🌍 Area: World Building & Level Design

> **Professional Roblox Studio scene assembly, level design, and map integration.**  
> Enforces mathematical anti-intersection laws, multi-point raycast surface snapping, grid snapping, 100% anchoring integrity, and natural clustering.

---

## 🛑 The Critical Defect: Model Intersection & Penetration

> [!CAUTION]
> ### Strict Prohibition: Zero Model-in-Model Penetration
> Careless placement scripts generate models directly inside other models (e.g. trees embedded inside rock boulders, rocks poking through canyon walls, or decorative props spawning inside structures).
> 
> Placement must obey rigorous bounding box mathematics, cluster-aware radial spacing, and multi-point ground surface verification.

---

## 📐 The 5 Mandatory Spatial Laws

1. **Oriented-to-World AABB Overlap Test:**
   - Every candidate model's world footprint must pass an Oriented-to-World AABB overlap test against all previously placed models.
   - When models are rotated 45° or 90°, their bounding box expands. Never check raw local dimensions.
2. **Pivot vs. Bounding Box Offset Drift Compensation:**
   - `model:PivotTo(cf)` sets the model's *Pivot*, not its bounding box center.
   - If the model's pivot is at its bottom base or off-center, placing the pivot at `hitResult.Position.Y + height/2` floats the model in the air or sinks it into terrain.
   - Ground contact must be mathematically computed via `boundingBoxCFrame:ToObjectSpace(model:GetPivot())`.
3. **Multi-Point Downward Surface Raycasting:**
   - Never cast only 1 ray at $(X, Z)$.
   - Cast **5 downward rays**: 1 at the center and 4 at the bounding box corners.
   - All 5 rays must hit walkable surfaces with `Normal.Y >= 0.70` (slopes $\le 45^\circ$). If any corner overhangs a cliff or hits a steep wall, reject placement.
4. **Cluster-Aware Placement Math:**
   - Satellite rocks and shrubs around an anchor boulder must be placed within a tight radial contact ring (`anchorRadius + satelliteRadius + 0.5 studs`) without penetrating the anchor's collision volume.
5. **Mandatory Post-Assembly Spatial Collision Audit:**
   - Run the automated Luau audit script after scene generation to mathematically prove zero model overlaps exist across the workspace.

---

## 🏗️ Core Assembly Rules

- **100% Anchoring Rule:** Every single static piece of geometry (floors, walls, trees, rocks, buildings, decorations) MUST have `Anchored = true`.
- **Strict Grid Snapping:**
  - Large cliff bastions & terrain: `4 studs`
  - Architectural walls & floor tiles: `2 studs`
  - Props & decorative clusters: `1 stud` or `0.5 stud`
- **Zero Z-Fighting:** Never place two coplanar surfaces at the exact same coordinate. Offset overlapping decals, trim, and carpets by at least `0.02` studs on the normal axis.
- **Physics Optimization:**
  - Walkways & walls: `CanCollide = true`, `CanTouch = true`.
  - Micro-scatter (grass tufts, flowers, pebbles): `CanCollide = false`, `CanTouch = false`, `CanQuery = false`.
- **Anti-Blowout Lighting Rule:**
  - Never place lights with `Brightness > 0.8` or `Range > 16` adjacent to bright/white reflective surfaces. Avoid blinding whiteout blooms.

---

## 🔗 Related Vault Links
- Math & Scripts: [[03 - Resources/Spatial Math & Anti-Intersection Guide|Spatial Math & Anti-Intersection Guide]]
- Biome Layer Manifest: [[03 - Resources/7 Environmental Layers Biome Checklist|7 Environmental Layers Biome Checklist]]
- Asset Pipeline: [[02 - Areas/Roblox Asset Pipeline|Roblox Asset Pipeline]]
- 3D Modeling: [[02 - Areas/Blender Modeler & 3D Art|Blender Modeler & 3D Art]]
