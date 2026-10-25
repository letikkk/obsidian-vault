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
