---
kanban-plugin: basic
tags:
  - project
  - kanban
  - roblox
  - gamedev
---

## 📥 Backlog

- [ ] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: **[TASK-02]** Offline Earnings / Idle AFK Income System (timestamp delta, cap, claim modal) #high
- [ ] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: **[TASK-03]** Interactive "Mountain of Money" World Prop (central cash vault, token-bucket rate limiter) #medium
- [ ] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: **[TASK-04]** Community Engagement Perks: Group Join & Favorite Rewards (server GroupService check, triad state) #medium
- [ ] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: **[TASK-05]** Economy & Progression Balance Pass (early game pacing, upgrade curves, spawn intervals) #high
- [ ] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: **[TASK-06]** General Bug Fixes, Network Optimization & QoL Polish (console audit, safe-zone boundaries) #medium
- [ ] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Build Plot upgrade shop (expanded holding pens, faster conveyor belts) #high
- [ ] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Implement Rebirth progression system with speed gain multipliers #high
- [ ] [[02 - Areas/Check-UI Design System|Check-UI]]: Build 7-Day Daily Rewards Modal (3x2 grid + Rainbow Day 7 card) #medium
- [ ] [[02 - Areas/Blender Modeler & 3D Art|Blender MCP]]: Model 18-asset modular biome set for Snow / Tundra zone #high
- [ ] [[01 - Projects/PlotTest/PlotTest|PlotTest]]: Implement thread-safe dynamic plot allocator with Trove cleanup #medium
- [ ] [[03 - Resources/7 Environmental Layers Biome Checklist|Asset Pipeline]]: Build Desert / Canyon 20-asset manifest #low

## 🚧 In Progress

- [ ] [[01 - Projects/PlotTest/PlotTest|PlotTest]]: Port verified plot instancing logic into Steal A Crate PlotManager #high
- [ ] [[02 - Areas/World Building & Level Design|World Building]]: Audit zone boundary collision meshes to prevent player flinging out of map #medium

## ✅ Done

- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: **[TASK-01]** First-Time User Experience (FTUE): Guaranteed Tutorial Crate & 5-Step Funnel (TutorialService, TutorialController, ground chevron arrows, cartoon pointer hand, fast 3s open, guaranteed Scarf Bear, $250 reward, AnalyticsService funnel) #high

- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Fixed crate grounding & terrain sinking (PrimaryParts, bottom PivotOffsets, WeldConstraints, dynamic bottomRelPivot math in SetupCratesService, BaseService, PlacementController) #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Published 23 entity animations to Domofon Games (858153940) via Roblox Open Cloud Assets API and linked in ReplicatedStorage.Assets.Animations #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Imported 8 Biome Crates (Snow & Desert) into ReplicatedStorage.Assets.Crates & mapped in CratesData #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Imported Desert entities SandCentipede (Mythic) & SunkenPharaoh (Secret) into ReplicatedStorage.Assets.Entities and CharactersData #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Integrated Treadmill LVL 5 (gain 40, $35k upgrade, Level 5 cap, synced with UpgradeSign and PlotTemplate) #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: 3D ViewportFrame model centering & 360° turntable spin loop engine (PetIndexUI, GrowingCratesUI, EquippedPetsUI) #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Cross-device responsive UI scaling & text anti-overflow engine (EquippedPetsUI, GrowingCratesUI, PetIndexUI, ShopUI, SellUI) #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Fixed dual click sound & event duplicate firing on HUD and modal buttons (centralized to modern .Activated with debouncing) #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Purged MutationSound electric audio asset & playback from ReplicatedStorage and controllers #medium
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Spatial grid pet scattering on expanded base plots & widened wander perimeter math #medium
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Dynamic FOV camera shift for crate carrying and treadmill sprinting #medium
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: 3D ViewportFrame rendering in PetIndexUI, GrowingCratesUI, and EquippedPetsUI with mutation rendering #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Add connection sound effect when Bat strikes enemy player #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Visual hologram trap placement indicator before dropping #medium
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Crate opening particle burst effect when opening at base hatch #medium
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Connect Check-UI HUD menus (ShopUI, PetIndexUI, GrowingCratesUI, EquippedPetsUI) #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Fixed Crates & Pets drawer opening bug (resolved require-cycle lock & bound cross-platform Activated events) #high
- [x] [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]: Implement AnalyticsService onboarding funnels (Tutorial, FirstHeist, CoreProgression) #high
- [x] Initialized dedicated Roblox Obsidian Studio Vault with PARA architecture
- [x] Configured Check-UI permanent `ZoneBanner` with 100% solid GothamBlack typography
- [x] Built non-lethal constraint ragdoll & 150-stud bat fling combat engine
- [x] Created randomized crate physics scaling (0.7x - 2.2x) with proportional weight encumbrance
- [x] Implemented treadmill speed training loop with floating tween popup text
- [x] Setup Rokit & Rojo 7.6.1 toolchain for [[01 - Projects/PlotTest/PlotTest|PlotTest]]
- [x] Documented complete [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]] GDD, Architecture, and API specs
