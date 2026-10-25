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
