---
title: Check-UI Design System
categories:
  - "[[Areas]]"
tags:
  - area
  - roblox
  - ui
  - ux
  - design-system
  - check-ui
created: 2026-10-18
status: active
---

# 🎨 Area: Check-UI Design System

> **The definitive design specification and component architecture for high-engagement, non-generic Roblox cartoon, simulator, and tycoon interfaces.**  
> Crafted with mathematical precision, strict GothamBlack typography, physical 3D bevels, multi-palette thematic hierarchy, and universal multi-device responsive scaling.

---

## 💎 The 8 Non-Negotiable Commandments

1. **Strict GothamBlack (`Enum.Font.GothamBlack`):**
   - The ONLY allowed font for all headings, labels, button text, and badges.
   - Text outlines use contextual dark strokes (`UIStroke` thickness `1.5 - 3.5px`, color `#0E1418`).
2. **100% Opaque Slate Canvas (`#3B5866`):**
   - Window canvas is ALWAYS `Color3.fromRGB(59, 88, 102)` with charcoal outer border (`#181E22`, 3.5px).
   - Never use translucent frosted glass or transparent backgrounds.
3. **Physical 3D Beveled Depth:**
   - Every interactive element has a 3-4px dark extrusion bottom bevel.
   - Buttons sink 2px downward on press (`Activated`) to give tangible tactile feedback.
4. **Signature 3D Beveled Square Close Button `[X]` (`38x38px`):**
   - Deep crimson base (`#730010`), shifted bright crimson face (`#E11428`), pastel pink outline (`#FFA0AA`, 1.5px), and centered GothamBlack `X` in `#FFFFFF`.
5. **2-Tier 3D Header Shadow Divider:**
   - A thematic dark accent line (3px height) stacked directly above a pure black line (3px height, `#000000`, 0.65 transparency).
6. **Seamless Fading Damier (Checkerboard):**
   - Full-height checkerboard texture overlay with smooth 4-point vertical transparency gradient to prevent sharp cutoff lines.
7. **Center-Anchored Tween Architecture:**
   - `AnchorPoint = Vector2.new(0.5, 0.5)` with child `UIScale` animated via `TweenService` for uniform expanding entrance (`Enum.EasingStyle.Back`, `Enum.EasingDirection.Out`).
8. **The Button State Triad:**
   - **Claim:** Vibrant Lime Neon (`#80FF00` -> `#50D000`).
   - **Claimed:** Metallic Silver Slate (`#D7DEE8` -> `#A0AAB8`).
   - **Locked:** Deep Crimson Alert (`#FF283C` -> `#C81420`).
   - **Skip / Action:** Warm Golden Amber (`#FFB400` -> `#E68C00`).

---

## 🎨 The Thematic Matrix: The 5 Header Archetypes

Every menu uses an unmistakable color identity, while preserving identical 60px header height, white top highlight, fading damier, and 2-tier bottom shadow divider:

| Menu Archetype    | Gradient Top | Gradient Bottom | Top Highlight | Damier Color | Dark Divider |
| :---------------- | :----------- | :-------------- | :------------ | :----------- | :----------- |
| **Shop**          | `#FF1496`    | `#E10019`       | `#FFC8E1`     | `#960014`    | `#7D0012`    |
| **Codes**         | `#00CDFF`    | `#0082F5`       | `#B4F0FF`     | `#004B96`    | `#00326E`    |
| **Settings**      | `#FFFFFF`    | `#D7DEE8`       | `#FFFFFF`     | `#6E7887`    | `#5A6470`    |
| **Rebirth**       | `#A000FF`    | `#6000C8`       | `#E0A0FF`     | `#600090`    | `#500078`    |
| **Daily Rewards** | `#98FF00`    | `#50D000`       | `#E0FFB0`     | `#358000`    | `#256000`    |

---

## 📱 Universal Responsive Engine (`UIScale`)

To ensure flawless layout on every device (Phone, Tablet, Desktop, Console), Check-UI uses a single root `UIScale` inside the `ScreenGui`:

$$\text{ScaleFactor} = \text{math.clamp}\left(\min\left(\frac{\text{Viewport.X}}{1920}, \frac{\text{Viewport.Y}}{1080}\right) \times 1.45, 0.52, 1.18\right)$$

- Clamped between `0.52` (smallest mobile phones) and `1.18` (4K monitors).
- Never allows text clipping, icon overlap, or distorted modal proportions.

---

## 📂 Core Check-UI Files in Plugin
- Specification: `C:\Users\meepo\.gemini\config\plugins\roblox-game-developer\skills\roblox-ui-designer\DESIGN_SYSTEM.md`
- Luau Controllers: `CheckUIController.luau`, `CheckUIComponents.luau`, `CheckUITheme.luau`
- Icon Registry: `CheckUIIcons.luau` (1,022 curated HD simulator icons)

---

## 🔗 Related Vault Links
- Active Game UI: [[01 - Projects/Steal A Crate/Technical Reference|Steal A Crate Technical Reference]]
- Color & Spec Cheatsheet: [[03 - Resources/Check-UI Component & Color Reference|Check-UI Component & Color Reference]]
- Asset Catalog: [[03 - Resources/Local Audio & UI Asset Catalog|Local Audio & UI Asset Catalog]]
- Programming Rules: [[02 - Areas/Roblox Luau Engineering|Roblox Luau Engineering]]
