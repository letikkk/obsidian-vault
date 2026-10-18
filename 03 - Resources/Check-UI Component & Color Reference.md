---
title: Check-UI Component & Color Reference
categories:
  - "[[Resources]]"
tags:
  - resource
  - roblox
  - ui
  - check-ui
  - design-system
  - color-palette
created: 2026-10-18
status: active
---

# 🎨 Resource: Check-UI Component & Color Reference

> **Exact color hex codes, RGB vectors, button geometry blueprints, and UI controller binding code snippets for Check-UI.**

---

## 🎨 Master Color Palette & RGB Matrix

### 1. Window Canvas & Frame
- **Canvas Base:** `#3B5866` -> `Color3.fromRGB(59, 88, 102)`
- **Outer Border:** `#181E22` -> `Color3.fromRGB(24, 30, 34)` (Stroke: `3.5px`)
- **Inner Recessed Box:** `#243640` -> `Color3.fromRGB(36, 54, 64)`

### 2. The 5 Header Color Archetypes

| Menu | Gradient Top | Gradient Bottom | Top Highlight Line | Damier Overlay | Dark Shadow Divider |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Shop** | `#FF1496` `(255, 20, 150)` | `#E10019` `(225, 0, 25)` | `#FFC8E1` | `#960014` | `#7D0012` |
| **Codes** | `#00CDFF` `(0, 205, 255)` | `#0082F5` `(0, 130, 245)` | `#B4F0FF` | `#004B96` | `#00326E` |
| **Settings** | `#FFFFFF` `(255, 255, 255)` | `#D7DEE8` `(215, 222, 232)`| `#FFFFFF` | `#6E7887` | `#5A6470` |
| **Rebirth** | `#A000FF` `(160, 0, 255)` | `#6000C8` `(96, 0, 200)` | `#E0A0FF` | `#600090` | `#500078` |
| **Daily Rewards** | `#98FF00` `(152, 255, 0)` | `#50D000` `(80, 208, 0)` | `#E0FFB0` | `#358000` | `#256000` |

### 3. The Button State Triad & Action Buttons

| State | Top Gradient | Bottom Gradient | Bevel Bottom Extrusion | Text Outline Color |
| :--- | :--- | :--- | :--- | :--- |
| **Claim (Neon Lime)** | `#80FF00` `(128, 255, 0)` | `#50D000` `(80, 208, 0)` | `#308000` `(48, 128, 0)` | `#143200` |
| **Claimed (Silver Slate)** | `#D7DEE8` `(215, 222, 232)`| `#A0AAB8` `(160, 170, 184)`| `#647080` `(100, 112, 128)`| `#323840` |
| **Locked (Crimson Red)** | `#FF283C` `(255, 40, 60)` | `#C81420` `(200, 20, 32)` | `#78000A` `(120, 0, 10)` | `#3C0005` |
| **Skip (Golden Amber)** | `#FFB400` `(255, 180, 0)` | `#E68C00` `(230, 140, 0)` | `#965A00` `(150, 90, 0)` | `#462800` |

---

## 🔲 Signature 3D Close Button `[X]` Blueprint

- **Dimensions:** `38 x 38 px`
- **Base Extrusion:** `Color3.fromRGB(115, 0, 16)` (`#730010`)
- **Top Face:** `Color3.fromRGB(225, 20, 40)` (`#E11428`), offset 3px from bottom
- **Top Stroke:** `Color3.fromRGB(255, 160, 170)` (`#FFA0AA`), thickness `1.5px`
- **Text:** `X`, `Enum.Font.GothamBlack`, Size `22px`, Color `#FFFFFF`, dark drop-shadow

---

## 💻 UI Controller Binding Pattern (Strict Luau)

```luau
--!strict
local SoundService = game:GetService("SoundService")
local TweenService = game:GetService("TweenService")

local TWEEN_IN = TweenInfo.new(0.08, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
local TWEEN_OUT = TweenInfo.new(0.12, Enum.EasingStyle.Back, Enum.EasingDirection.Out)

local function bindButton(button: GuiButton, clickSound: Sound?, onActivated: () -> ())
    local uiScale = button:FindFirstChildWhichIsA("UIScale") or Instance.new("UIScale")
    uiScale.Parent = button

    button.MouseButton1Down:Connect(function()
        TweenService:Create(uiScale, TWEEN_IN, { Scale = 0.94 }):Play()
    end)

    button.MouseButton1Up:Connect(function()
        TweenService:Create(uiScale, TWEEN_OUT, { Scale = 1.0 }):Play()
    end)

    button.Activated:Connect(function()
        if clickSound then
            clickSound:Play()
        end
        onActivated()
    end)
end
```

---

## 🔗 Related Vault Links
- Design System Area: [[02 - Areas/Check-UI Design System|Check-UI Design System]]
- Flagship UI Specs: [[01 - Projects/Steal A Crate/Technical Reference|Steal A Crate Technical Reference]]
- Audio & Icons: [[03 - Resources/Local Audio & UI Asset Catalog|Local Audio & UI Asset Catalog]]
