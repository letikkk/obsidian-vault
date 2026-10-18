---
title: Local Audio & UI Asset Catalog
categories:
  - "[[Resources]]"
tags:
  - resource
  - roblox
  - ui
  - audio
  - sfx
  - asset-catalog
created: 2026-10-18
status: active
---

# 🔊 Resource: Local Audio & UI Asset Catalog

> **Centralized directory of local interface assets, audio cues, and verified Roblox Asset IDs across projects.**

---

## 🎵 Local Sound Library (`C:\Users\meepo\Documents\UIAssets\Sounds`)

High-quality tactile interface sound cues ready for Roblox Studio import or local prototyping:

| Sound File | Format | Recommended UI Action | Character & Feel |
| :--- | :--- | :--- | :--- |
| `click-a.ogg` | OGG Vorbis | Generic button click / Modal open | Crisp, medium-pitch tactile snap |
| `click-b.ogg` | OGG Vorbis | Close button `[X]` / Back navigation | Slightly lower pitch confirmation click |
| `switch-a.ogg` | OGG Vorbis | Toggle ON (SFX, Music, Settings) | Upward chirping switch |
| `switch-b.ogg` | OGG Vorbis | Toggle OFF (SFX, Music, Settings) | Downward chirping switch |
| `tap-a.ogg` | OGG Vorbis | Mobile HUD interaction / Tab switch | Soft, subtle touch response |
| `tap-b.ogg` | OGG Vorbis | Item card selection in Shop | Deeper touch response |

---

## 🌐 Verified Roblox Cloud Sound Registry (`ReplicatedStorage.Assets.Sounds`)

Production sound assets actively configured in [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]:

| Sound Name | Asset ID | Volume | Gameplay Function |
| :--- | :--- | :--- | :--- |
| **NotificationPop** | `rbxassetid://105983221709653` | 0.55 | Zone banner pop-in & standard notification |
| **SuccessSound** | `rbxassetid://86810634715248` | 0.50 | Crate delivered at hatch / cash awarded |
| **ErrorSound** | `rbxassetid://87519554692663` | 0.60 | Action rejected / invalid purchase / cooldown |
| **ButtonClick** | `rbxassetid://15675059323` | 0.50 | Check-UI button interaction sound |

---

## 🎨 Local Vector & Icon Packs

### 1. Free Icon Pack v3.1 (Basic)
- **Path:** `C:\Users\meepo\Documents\UIAssets\Free Icon Pack v3.1 (Basic)`
- Contains over 200+ clean vector-style icons for gamepasses, player currencies, badges, weapons, and status effects.

### 2. Cartoon UIElements Library
- **Path:** `C:\Users\meepo\Documents\UIAssets\UIElements`
- **Variants:** `Blue`, `Green`, `Grey`, `Red`, `Yellow`, `Purple`
- **Styles:** `Double`, `Flat`, `Gloss`, `Gradient`, `Line`, `Depth`
- **Components:** Beveled square buttons, round buttons, sliders, checkmarks, stars, and directional arrows.

---

## 🔗 Related Vault Links
- UI Design System: [[02 - Areas/Check-UI Design System|Check-UI Design System]]
- Color & Spec Reference: [[03 - Resources/Check-UI Component & Color Reference|Check-UI Component & Color Reference]]
- Active UI Specs: [[01 - Projects/Steal A Crate/Technical Reference|Steal A Crate Technical Reference]]
