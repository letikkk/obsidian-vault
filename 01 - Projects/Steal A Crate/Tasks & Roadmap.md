---
title: Steal A Crate - Tasks & Roadmap
categories:
  - "[[Projects]]"
tags:
  - project
  - roblox
  - tasks
  - roadmap
created: 2026-10-15
status: active
---

# 📋 Steal A Crate - Tasks & Roadmap

> **Active development roadmap, completed features, and sprint backlog powered by Obsidian's `Tasks` plugin.**

Parent Hub: [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]] · Kanban: [[01 - Projects/Project Kanban|Project Kanban]]

---

## 🚀 Active Sprint & In Progress

### Epic: Onboarding, Retention & Economy Expansion
- [x] **[TASK-01] First-Time User Experience (FTUE): Guaranteed Tutorial Crate & Funnel** #high ✅ 2026-10-25
  - Deterministic collision-safe tutorial crate spawn adjacent to player (`(36, 10, -78)`).
  - Client theft protection lock (`TutorialOwner = player.UserId`).
  - 5-step tutorial flow matching reference: "Steal a Crate!", "Go to your Pen!", "Place your Crate!", "Open the Crate", "Place your Pet!".
  - Animated cartoon hand pointer cursor (`rbxassetid://131458905217618`) & dynamic red ground chevron trail (`rbxassetid://119897674193442`).
  - Fast 3s opening countdown on tutorial crate & guaranteed starter Scarf Bear reward.
  - $250 completion bonus & persistent profile store flag (`isTutorialCompleted = true`).
  - Funnel analytics tracking: `Tutorial: Start -> StealCrate -> PlaceCrate -> OpenCrate -> PlacePet`.
  - Fixed banner permanence for existing players via progression auto-detection (`isExistingPlayer`).
  - Implemented luminous guidance Beam ray with flowing chevrons, 3D waypoint beacon (`▼`), and `GetTutorialState` RemoteFunction client sync.
- [x] **[TASK-02] Offline Earnings / Idle AFK Income System** #high ✅ 2026-10-26
  - Store `LastLogoutTimestamp: number` in `ProfileStore` data.
  - Calculate `deltaTime = math.min(CurrentTime - LastLogoutTimestamp, MAX_OFFLINE_SECONDS)` (12-hour cap).
  - Payout rate derived dynamically from placed collectibles & crates via `getPlayerIncomeRate` (minimum $5/s baseline).
  - Atomic persistence in `PlayerData`, `Template`, and ProfileStore session saving.
  - RemoteEvent `ClaimOfflineCash` & client event `OfflineCashClaimed` dispatching payout amount and pile coordinates.
  - Client-side feedback: tactile `SuccessSound` chime, rising pop-up text (`+$18K`, GothamBlack, lime neon `#98FF00`, black UIStroke) with tween fadeout, sparkle particle burst, and Check-UI `MessageHandler` toast.
- [x] **[TASK-03] Interactive "Mountain of Money" World Prop** #medium ✅ 2026-10-26
  - Modeled interactive central cash pile prop (`Money`) in plot center with dollar bill textures & white cartoon rim highlight (`Highlight`, `OutlineTransparency = 0.1`).
  - Dynamic vertical scaling: min Y = 1.0, max Y = 20.0 scaling proportionally up to $25k offline earnings.
  - Sized to span the full base pen width & depth ($42 \times 42$ studs base, expanding automatically with pen fence upgrades).
  - Rock-solid ground anchoring: grounded at $Y = 10.05$ with raycast floor alignment to map geometry with zero floor sinking.
  - Step-to-claim interaction: purged all ProximityPrompts; claims instantly by walking/stepping onto the pile via client Heartbeat bounding-box query + server ZonePlus & Touched fallbacks.
  - Visible only on join when offline income exists (`OfflineCash > 0`). When offline earnings are zero, pile is fully invisible (`Transparency = 1`, all texture layers transparent, outline & billboard disabled).
  - Smooth removal on claim: tweens down to floor level and fades transparency to 1 simultaneously, removing the pile completely.
  - Player spawn point relocated: moved `SpawnPoint` in `PlotTemplate` outside in front of the base entrance walkway near the treadmill, oriented looking into the pen. Players spawn facing their base with an unobstructed view of the base interior and the giant offline cash pile.
- [ ] **[TASK-04] Community Engagement Perks: Group Join & Favorite Rewards** #medium
  - Server validation via `Player:IsInGroup(GROUP_ID)`.
  - Profile state tracking (`GroupRewardClaimed`, `FavoriteRewardClaimed`).
  - Button State Triad: `Claim`, `Claimed`, `Locked / Join Group`.
- [x] **[TASK-05] Economy & Progression Balance Pass (90-Minute Dunes Target)** #high ✅ 2026-10-26
  - Centralized crate weight, slowdown curves, and economy scaling across Forest -> Beach -> Snow -> Dunes.
  - Calibrated enemy chase speeds (`ForestOldMan` 24 -> `KingCrab` 38 -> `Yeti` 56 -> `Insurrectionist` 76).
  - Scaled Treadmill progression: Level 1 (free, +10), Level 2 ($1.5k, +30), Level 3 ($12k, +75), Level 4 ($85k, +175), Level 5 ($350k, +750).
  - Stealing Dunes crates now requires ~3.2M SpeedPoints and Treadmill Level 5, targeting ~90 minutes of active progression.
- [x] **[TASK-INVENTORY] Satchel Backpack Engine & Fixed Quickslots** #high ✅ 2026-10-26
  - Integrated open-source Satchel inventory engine (DevForum 2451549 / RyanLua Satchel v1.4.1 + TopbarPlus v3.4.0).
  - Hard-locked Bat to Hotbar Slot 1 and Trap to Hotbar Slot 2; drag-and-drop disabled and swap rejection enforced.
  - Converted client loader into clean `StarterPlayerScripts.SatchelLoader` LocalScript with zero duplicate execution warnings.
- [x] **[TASK-ZONES] Dunes Zone Banner & Desert Ambience** #medium ✅ 2026-10-26
  - Added Dunes zone boundary coordinates ($Z \le -350.5$) and `Dunes 🏜️` golden banner popup (`Color3.fromRGB(255, 220, 140)`).
  - Wired procedural desert ambient loop (`DesertAmbience`) with pitch modulation.
- [x] **[TASK-PROMPTS] ProximityPrompt Purge for Upgrade Boards** #medium ✅ 2026-10-26
  - Purged ProximityPrompts from `TreadmillUpgrade` and `Pet upgrade` signs in workspace, replicated assets, and `PlotTemplate`.
  - Upgrades are now exclusively activated via direct SurfaceGui button interactions.
- [x] **[TASK-06] General Bug Fixes, Network Optimization & QoL Polish** #medium ✅ 2026-10-27
  - Resolved asset type mismatch errors in `TutorialController` by extracting underlying image asset IDs (`rbxassetid://135597858720677` and `rbxassetid://70378970941187`).
  - Mobile viewport & touch control safety: audited ScreenGui safe insets (`DeviceSafeInsets`), positioned `DayNightHUD` with responsive touch-offset (`-130px`) to prevent overlap with the mobile jump button.
  - Physics anti-sink floor grounding audit: unified mathematical bounding-box bottom offset in `SetupCratesService` drop logic and world spawns (`bottomRelPivot`), verified 20 crates in live play mode at exact $Y = 10.00$ flush on terrain.
  - Zero uncaught Luau runtime errors verified across client and server in live Play mode.

- [ ] Connect Obsidian vault notes with repository git workflow #low

---

## ✅ Completed Milestones

### Combat & Ragdoll Engine
- [x] Add sound effect when Bat successfully connects with another player #high
- [x] Implement visual trap placement indicator (hologram wireframe preview before drop) #medium
- [x] Add crate opening particle burst effect when opening at the base hatch #medium

### Core Mechanics & Physics
- [x] Implement randomized crate scale (0.7x to 2.2x) and mass tiering #high
- [x] Implement dynamic carrying slowdown based on crate weight #high
- [x] Implement dual-arm hold weld and automatic drop on damage #high
- [x] Build modular `PlotTemplate` and `PlotRoots` dynamic instantiation on player join #high
- [x] Build treadmill speed training granting stats every 0.2s with ultra-fast popups #medium

### Combat & Ragdoll Engine
- [x] Create non-lethal constraint-based ragdoll module inspired by *Steal an Egg* #high
- [x] Implement enemy hit reaction with ~50 studs fling impulse #high
- [x] Build Bat weapon with directional raycast hitbox on LMB / Mobile tap #high
- [x] Fix bat swing animation looping bug (proper one-shot playback) #high
- [x] Set Bat hit impulse to fling victims ~150 studs and drop crates #high
- [x] Build Trap weapon with 5-charge maximum stock #high
- [x] Implement trap auto-despawn and charge replenishment after 60s or upon trigger #high

### User Interface & Game Feel (`Check-UI`)
- [x] Port notification stack from *Collect a Snack* into `PlayerGui.Main.Messages` #medium
- [x] Import notification audio cues (`NotificationPop`, `SuccessSound`, `ErrorSound`, `ButtonClick`) #medium
- [x] Build 5 notification gradient presets (`Normal`, `Success`, `Robux`, `Rolled`, `Error`) #medium
- [x] Build live `LeaderstatsHUD` displaying real-time Cash and Speed #medium
- [x] Create Zone Entering UI banner (`Forest 🙂`, `Beach 🏖️`, `Snow ❄️`, `Safe Zone 🛡️`) #high
- [x] Refactor zone banner to permanent `StarterGui.Main.ZoneBanner` Frame #high
- [x] Fix half-transparent text issue: isolate UIGradient to Background Frame for 100% solid text #high
- [x] Connect Check-UI HUD menus: ShopUI, PetIndexUI, GrowingCratesUI, and EquippedPetsUI #high
- [x] Implement AnalyticsService onboarding funnels (Tutorial, FirstHeist, CoreProgression) #high ✅ 2026-10-25
- [x] Implement dynamic FOV camera expansion when carrying heavy crates and running on treadmills #medium ✅ 2026-10-25
- [x] Align HUD button pivots to AnchorPoint (0.5, 0.5) with tactile UIScale hover/press bounce animations #medium ✅ 2026-10-25
- [x] Fix double-click sound and dual event triggers on UI elements (purged legacy MouseButton1Click, centralized to Activated with debouncing) #high ✅ 2026-10-25
- [x] Purge MutationSound electrical zap audio asset and all playback references across ReplicatedStorage, MutationModule, MutationController, and HatchController #medium ✅ 2026-10-25
- [x] Implement spatial grid pet scattering and dynamic wander boundaries on expanded plots (PenLevel > 1) in BaseService #medium ✅ 2026-10-25
- [x] Cross-device responsive UI scaling & anti-overflow: convert fixed font sizes to TextScaled + UITextSizeConstraint across EquippedPetsUI, GrowingCratesUI, PetIndexUI, ShopUI, and SellUI #high ✅ 2026-10-25
- [x] Fix header and pet row text collisions in EquippedPetsUI (EquippedCount vs ExtraSlotButton, PetName vs UnequipButton) #high ✅ 2026-10-25
- [x] Fix header text collision in GrowingCratesUI (Title vs GrowAllButton) #high ✅ 2026-10-25
- [x] Fix pet card text bleeding across columns in PetIndexUI across all 4 biomes with ClipsDescendants and text wrapping #high ✅ 2026-10-25
- [x] Integrate dynamic getDeviceScale() engine (0.58 to 1.12) bound to ViewportSize for modal dialogs (PetIndexUI, ShopUI, SellUI, TrailShopUI) #high ✅ 2026-10-25
- [x] Implement 3D ViewportFrame previews across PetIndexUI (all 32 biome cards + PetDetails with undiscovered silhouette), GrowingCratesUI (ready & growing crates), and EquippedPetsUI (equipped pets with dynamic mutation VFX rendering) #high ✅ 2026-10-25
- [x] Correct ViewportFrame model centering (bounding box delta offset) & integrate continuous 360° turntable spinning animation across PetIndexUI, GrowingCratesUI, and EquippedPetsUI #high ✅ 2026-10-25

### World, Progression & Asset Pipeline
- [x] Configure and integrate Treadmill Level 5 (`TreadmillLVL5`: 40 Speed gain, $35,000 upgrade cost, Level 5 cap, synced with UpgradeSign and PlotTemplate) #high ✅ 2026-10-25
- [x] Import new Desert entities `SandCentipede` (Mythic) and `SunkenPharaoh` (Secret) into `ReplicatedStorage.Assets.Entities` and register stats in `CharactersData` #high ✅ 2026-10-25
- [x] Import 8 new biome crate models (`FrostWoodCrate`, `IceboundCrate`, `AuroraRelicCrate`, `DuneCrate`, `MirageCrate`, `SunkenSandsCrate`, `PharaohCrate`, `PrecursorCrate`) into `ReplicatedStorage.Assets.Crates` and map in `CratesData` #high ✅ 2026-10-25
- [x] Fix crate grounding & physics collision: configure PrimaryParts, bottom-aligned PivotOffset, rigid WeldConstraints, and dynamic bounding-box bottom compensation in SetupCratesService, BaseService, and PlacementController to eliminate terrain sinking #high ✅ 2026-10-25
- [x] Publish 23 entity animations via Roblox Open Cloud to Domofon Games (`858153940`) and link in `ReplicatedStorage.Assets.Animations` (SandCentipede, SunkenPharaoh, FernFox, ScarabHopper, DustImp, BoneVulture, CinderJackal, EclipseHorror, FallenProtocol, Moth, Mammoth, Glaceclaw) #high ✅ 2026-10-25

---

## 🔮 Backlog & Future Milestones

### Milestone 1: Economy & Upgrades
- [ ] Build Plot upgrade store (expanded holding pens, faster conveyor belts) #medium
- [ ] Implement rebirth system multiplying base speed gains #high
- [ ] Build crate sell multiplier upgrades #medium

### Milestone 2: Cosmetics & Social
- [ ] Daily login streak rewards wheel #medium
- [ ] Trails & Pet eggs hatching station #low
- [ ] Global speed & cash leaderboards in Safe Zone hub #low
- [ ] Mobile UI controls polishing (custom thumbstick styling) #low
