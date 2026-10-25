---
title: Steal A Crate - Technical Reference
categories:
  - "[[Projects]]"
tags:
  - project
  - roblox
  - reference
  - api
created: 2026-10-15
status: active
---

# 📡 Steal A Crate - Technical Reference

> **Complete dictionary of RemoteEvents, asset IDs, UI component structures, and code conventions.**

Parent Hub: [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]

---

## 🌐 RemoteEvents API Dictionary

All network remotes reside under `game.ReplicatedStorage.Remotes`.

| RemoteEvent | Direction | Parameters | Description |
| :--- | :--- | :--- | :--- |
| `SendMessage` | Server $\rightarrow$ Client | `text: string`, `preset: string?` | Displays a notification popup (`Normal`, `Success`, `Robux`, `Rolled`, `Error`). |
| `BroadcastChatMessage` | Server $\rightarrow$ Client | `message: string` | Pushes a gold system message to TextChatService or legacy chat. |
| `BatAttack` | Client $\rightarrow$ Server | `targetModel: Model` | Validates melee hit on server; flings victim ~150 studs and drops crate. |
| `DeployTrap` | Client $\rightarrow$ Server | `cframe: CFrame` | Spawns a bear trap from player's inventory; starts 60s lifecycle. |
| `RagdollCharacter` | Server $\rightarrow$ Client | `duration: number`, `fling: Vector3` | Triggers client constraint ragdoll and applies impulse. |
| `SpeedGained` | Server $\rightarrow$ Client | `amount: number` | Notifies client of treadmill speed tick; triggers `SpeedPopupController`. |
| `PickUpCollectible` | Client $\rightarrow$ Server | `cratePart: BasePart` | Welds crate to player arms; applies weight encumbrance. |
| `DropCrate` | Client $\rightarrow$ Server | `none` | Breaks weld and restores player's unencumbered movement speed. |
| `PlaceCrate` | Client $\rightarrow$ Server | `targetSlot: BasePart` | Delivers crate to base hatch/conveyor for cash reward. |

---

## 🔊 Sound Asset Registry

All game audio resides in `game.ReplicatedStorage.Assets.Sounds`.

| Sound Name | Asset ID | Volume | Usage |
| :--- | :--- | :--- | :--- |
| **NotificationPop** | `rbxassetid://105983221709653` | 0.55 | Default notification pop-in cue |
| **SuccessSound** | `rbxassetid://86810634715248` | 0.50 | Success & Robux gradient popups |
| **ErrorSound** | `rbxassetid://87519554692663` | 0.60 | Error / action rejected notification |
| **ButtonClick** | `rbxassetid://15675059323` | 0.50 | Generic UI button interactions (single .Activated trigger) |
| **MutationMagic** | `rbxassetid://132185731364109` | 0.50 | Magical chime when mutated crate opens (replaces electric MutationSound) |
| *MutationSound* | *(Purged)* | - | Deprecated and purged from audio assets |

---

## 🎬 Animation Asset Registry (Domofon Games - Group `858153940`)

All animations reside in `game.ReplicatedStorage.Assets.Animations` and are owned by Domofon Games.

| Entity | Idle Asset ID | Walk Asset ID | Extra Asset IDs |
| :--- | :--- | :--- | :--- |
| **SandCentipede** | `rbxassetid://128253931263762` | `rbxassetid://140634133279132` | - |
| **SunkenPharaoh** | `rbxassetid://120629636648891` | `rbxassetid://78959423403575` | - |
| **FernFox** | `rbxassetid://108889141788533` | `rbxassetid://97810246004297` | - |
| **ScarabHopper** | `rbxassetid://118558772784188` | `rbxassetid://136792647557418` | - |
| **DustImp** | `rbxassetid://95566247351386` | `rbxassetid://92487888569158` | - |
| **BoneVulture** | `rbxassetid://106401394604364` | `rbxassetid://107064691244499` | - |
| **CinderJackal** | `rbxassetid://79514294950840` | `rbxassetid://110850620849176` | - |
| **EclipseHorror** | `rbxassetid://82800389860098` | `rbxassetid://95823606714347` | - |
| **FallenProtocol** | `rbxassetid://93806855486127` | `rbxassetid://113095548997251` | - |
| **Moth** | `rbxassetid://111891575048663` | `rbxassetid://94427832365301` | - |
| **Mammoth** | `rbxassetid://138636595000594` | `rbxassetid://128525679170695` | - |
| **Glaceclaw** | `rbxassetid://128571667493496` | `rbxassetid://131581818350069` | - |
| **ScarfBear** | `rbxassetid://117409210079538` | `rbxassetid://74188872002719` | - |
| **ForestOwl** | `rbxassetid://96388736253534` | `rbxassetid://102289040641160` | - |
| **StumpRig** | `rbxassetid://85358185036177` | `rbxassetid://99425354105478` | - |
| **Otter** | `rbxassetid://77189915727077` | `rbxassetid://95112558786289` | - |
| **MushroomDeer** | `rbxassetid://103193641509697` | `rbxassetid://91266209254945` | - |
| **Mawler** | `rbxassetid://104041350789423` | `rbxassetid://111638242845997` | - |
| **Patapim** | `rbxassetid://80570477844475` | `rbxassetid://100467920442035` | - |
| **ReefReaper** | `rbxassetid://81314998499540` | `rbxassetid://92469131814475` | - |
| **Seagull** | `rbxassetid://113715310291587` | `rbxassetid://82124237906107` | - |
| **Crab** | `rbxassetid://94252729906679` | `rbxassetid://79965403879272` | - |
| **Turtle** | `rbxassetid://101350500008466` | `rbxassetid://72807626175617` | - |
| **Seal** | `rbxassetid://86252345213570` | `rbxassetid://132349720729732` | - |
| **Octopus** | `rbxassetid://81809497442897` | `rbxassetid://78012182585044` | - |
| **Tralalero** | `rbxassetid://103681041517550` | `rbxassetid://130479543895303` | - |
| **Hermit** | `rbxassetid://116062200064281` | `rbxassetid://125564772570878` | - |
| **Merchant** | `rbxassetid://87757201132121` | - | - |
| **ForestOldMan** (Enemy) | `rbxassetid://74955343958567` | - | Run: `93922981330789`, Hit: `115437735416982`, Trigger: `116238258598796` |
| **KingCrab** (Enemy) | `rbxassetid://85472407638640` | - | Run: `101012495901968`, Hit: `115437735416982`, Trigger: `100770708540874` |
| **Yeti** (Enemy) | `rbxassetid://134769640898858` | - | Run: `129016072691507`, Hit: `100037034845168`, Trigger: `104573455434621` |
| **Insurrectionist** (Enemy) | `rbxassetid://105653045406230` | - | Run: `108223510892888`, Hit: `105210033812220`, Trigger: `76312148176812` |
| **Player** | - | - | Hit: `rbxassetid://135634562842670` |

---

## 🏃 Treadmill Progression Specification

Configured in `ServerScriptService.Main.Services.TreadmillService` and synced with `PlotTemplate.UpgradeSign`.

| Level | Gain / Tick | Upgrade Cost | Model Name | PrimaryPart |
| :--- | :--- | :--- | :--- | :--- |
| **Level 1** | +1 Speed | Starter Default | `Treadmilllvl1` | `Part` |
| **Level 2** | +3 Speed | $250 | `Treadmilllvl2` | `Black` |
| **Level 3** | +8 Speed | $1,500 | `Treadmilllvl3` | `Black` |
| **Level 4** | +20 Speed | $7,500 | `Treadmilllvl4` | `Black` |
| **Level 5** | +40 Speed | $35,000 | `TreadmillLVL5` / `Treadmilllvl5` | `Black` |

---

## 📦 Biome Crates & Extended Entities

Configured in `ReplicatedStorage.Data.CratesData` and `ReplicatedStorage.Data.CharactersData`.

### Extended Biome Crates (`ReplicatedStorage.Assets.Crates`)
- **Snow Biome:** `FrostWoodCrate`, `IceboundCrate`, `AuroraRelicCrate`
- **Desert Biome:** `DuneCrate`, `MirageCrate`, `SunkenSandsCrate`, `PharaohCrate`, `PrecursorCrate`

### Extended Desert Entities (`ReplicatedStorage.Assets.Entities`)
- **SandCentipede:** Mythic tier, BaseWeight `820`, HatchChance `0.04%`, Income `15,000`, SellPrice `650,000`, Multiplier `25.0`
- **SunkenPharaoh:** Secret tier, BaseWeight `1150`, HatchChance `0.005%`, Income `40,000`, SellPrice `1,800,000`, Multiplier `50.0`

---

## 🎭 3D Art, Rigging & Animation Kinematics Specification

### 1. Multi-Part MeshPart & MaterialVariant Architecture
Roblox `MeshPart`s only support a single `Color` and `MaterialVariant`. All models are split into distinct volumetric child meshes parented to the model:
- **`Studs` (`Plastic`):** Organic bodies, creature fur, chitin carapaces, foliage, and wooden slats.
- **`Weld` (`Plastic`):** Metal corner brackets, iron bands, rusty plates, and industrial gym hardware.
- **`Universal` (`Plastic`):** Polished synthetic materials, pedestals, and smooth crystal/ice housings.
- **`Glue` (`Plastic`):** Ancient stone/gold inlays, hieroglyphic plates, and sacred desert relics.
- **`Neon` (`Enum.Material.Neon`):** Emissive crystal shards, magic runes, glowing venom cores, and eyes.

### 2. Volumetric 3D Eye Anatomy
- All creature facial features utilize **100% 3D beveled mesh geometry** (zero 2D Decals or ImageLabels):
  - **Sclera:** Beveled white mesh pill (`White` MeshPart, BrickColor `Institutional white`).
  - **Pupil & Iris:** High-contrast beveled disc (`Eyes` / `Black` / `Pupil.L/R` MeshPart, BrickColor `Really black`).
  - **Specular Catchlight:** Forward-offset white highlight disc giving alive luster.
  - **Articulated Eyebrows:** Dedicated bones (`Eyebrow.L/R`) allowing expressive emotive blinking, squinting, and fierce reactions.

### 3. Skinned Armature Rigging & RootPart Motor6D Dual Pipeline
- **Armature Hierarchy:** Parented directly under `RootPart`, providing complete skeletal deforming rigs (e.g. `ScarfBear` 9 bones, `SandCentipede` 25 bones, `Octopus` 27 bones, `Glaceclaw` 29 bones, `KingCrab` 47 bones).
- **Motor6D Replication:** Each color-separated MeshPart is simultaneously bound to `RootPart` with a `Motor6D` (`Part0 = RootPart`, `Part1 = MeshPart`), guaranteeing physical replication and collision bounds in Roblox Studio.
- **IK Constraints:** Multi-legged creatures feature dedicated inverse kinematics targets (`Foot.IK.L/R`, `FrontLeg-IK.L/R`, `BackLeg-IK.L/R`) locking ground contact and eliminating foot sliding.
- **Sinusoidal Articulated Chains:** Multi-segment arthropods (`SandCentipede`) feature 8 articulated body/tail joints (`Body.001` -> `Tail` -> `Tail.001` -> `Tail.002` -> `Tail.003` -> `TailEnd`), producing fluid natural locomotion waves.

### 4. Animation Cadence & Kinematics
- **Cadence Standard:** 24 FPS baseline with smooth cubic interpolation.
- **Idle Cycles:** 48 keyframes (1.96s - 2.46s). Gentle vertical breathing oscillation on `Root`/`Body` (Y translation ~0.12 studs), ear/tail twitching, and secondary organic ripples (`Priority = Enum.AnimationPriority.Action`).
- **Walk / Run Cycles:** 21 - 24 keyframes (0.83s - 0.96s). Snappy, energetic step cycles with rhythmic leg swings, body tilt, and IK ground planting (`Priority = Enum.AnimationPriority.Action`).
- **Combat & Boss Actions:** 24 - 72 keyframes. Fast anticipation, explosive snap swing, ground pound shockwaves, and settling recoveries.

### 5. Crate Bottom-Aligned Pivot Specification
- Standard baseline: 2.16 x 2.16 x 2.16 studs cubic footprint.
- All 16 crate models have `PrimaryPart.PivotOffset = PrimaryPart.CFrame:ToObjectSpace(bottomCFrame)`, ensuring `diffFromBottom = 0.000` studs.
- All internal parts are rigidly connected to `PrimaryPart` via `WeldConstraint`s.
- `SetupCratesService`, `BaseService`, and `PlacementController` dynamically enforce `bottomRelPivot = math.max(0, pivot.Position.Y - (cf.Position.Y - (sz.Y / 2)))`, guaranteeing zero terrain penetration across all scales (`Regular 1.0x`, `Huge 1.8x`, `Colossal 3.5x`).

---

## 🎨 UI Hierarchy Specification (`StarterGui.Main`)

```
StarterGui.Main (ScreenGui: ResetOnSpawn = false, IgnoreGuiInset = true)
├── CrateEquippedFrame (Frame: Full-screen container)
│   ├── Vignette (ImageLabel: radial carrying vignette)
│   ├── RunButton (TextButton: mobile sprint toggle)
│   └── Drop (TextButton: drop crate button)
├── LeaderstatsHUD (Frame: Bottom-left HUD)
│   ├── Cash (Frame: icon + current currency TextLabel)
│   └── Speed (Frame: lightning icon + speed TextLabel)
├── Messages (Frame: Notification stack container)
│   ├── UIListLayout (Vertical, Bottom, Center, Padding = 0.03)
│   └── UIAspectRatioConstraint (AspectRatio = 2.95)
├── ZoneBanner (Frame: Zone entering popup)
│   ├── Background (Frame: Dark slate #0F141A, BackgroundTransparency = 0.5)
│   │   └── FadeGradient (UIGradient: horizontal fade [0 -> 1, 0.18 -> 0.45, 0.82 -> 0.45, 1 -> 1])
│   ├── BannerScale (UIScale: responsive viewport engine [0.52, 1.18])
│   └── ZoneLabel (TextLabel: GothamBlack 38pt, 100% solid opacity, TextTransparency = 0)
│       └── TextStroke (UIStroke: 3.2px, Color = #000000, Transparency = 0)
├── LefttSideButtons (Frame: Shop & Pet Index buttons with AnchorPoint 0.5, 0.5 bounce)
├── RightSideButtons (Frame: Crates & Pets drawer toggle buttons)
├── EquippedPetsUI (Frame: Right-side placed pets drawer with 3D PetViewport models & dynamic mutation VFX)
├── GrowingCratesUI (Frame: Right-side growing crates drawer with 3D CrateViewport models for ready/growing tiers)
├── PetIndexUI (Frame: 4-Biome completion modal with 3D PetViewport models, undiscovered silhouettes & getDeviceScale)
├── ShopUI (Frame: Simulator shop modal with dynamic getDeviceScale)
├── SellUI (Frame: Merchant sell modal with dynamic getDeviceScale)
└── TrailShopUI (Frame: Merchant trails shop modal with dynamic getDeviceScale)
```

---

## 📐 Codebase Constraints & Standards
1. **Comment & Log Hygiene:** Zero comments (`--`), zero `print()`, and zero `warn()` statements permitted across all production Luau scripts.
2. **Typography Rule:** Strict enforcement of `GothamBlack` (`GothamSSm`, Heavy) for all simulator headings and game alerts.
3. **Responsive Rule:** All popup and HUD elements must incorporate `UIScale` bound to multi-device viewport scaling `[0.52, 1.18]`.
