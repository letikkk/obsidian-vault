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

## 💎 Production Roblox Cloud UI Asset Registry (Domofon Games - Group `858153940`)

High-resolution 3D rendered interface and shop icons deployed across HUDs, Shop packs, passes, and currencies:

### 1. Currencies & Global Badges
| Asset Name | Local File | Asset ID | In-Game Location & Usage |
| :--- | :--- | :--- | :--- |
| **Money / Cash** | `money.png` | `rbxassetid://79405008321420` | `LeaderstatsHUD.Cash`, `ShopUI.MoneyTab`, `PetIndexUI` Zone Rewards, Shop & Trail Buy Cash buttons |
| **Speed / Running Shoe** | `speed.png` | `rbxassetid://88646027847673` | `LeaderstatsHUD.Speed`, `ShopUI.SpeedTab`, `PopUps.SpeedPopupTemplate`, `Shop_DoubleSpeed` |
| **Robux Coin** | `robux.png` | `rbxassetid://85199044418508` | `ShopUI` & `TrailShopUI` Robux purchase buttons (`CurrencyIcon`) |
| **Featured Star** | `featured.png` | `rbxassetid://81640732418008` | `ShopUI.FeaturedTab.Icon`, `ShopUI.Window.Header.CrateIcon` |

### 2. Gamepasses & Multipliers
| Asset Name | Local File | Asset ID | In-Game Location & Usage |
| :--- | :--- | :--- | :--- |
| **Double Money Pass** | `pass_double_money.png` | `rbxassetid://106170643857020` | `ShopUI.Shop_DoubleMoney.ProductImage` |
| **Double Open / Growth Pass** | `pass_double_open.png` | `rbxassetid://102099570025840` | `ShopUI.Shop_DoubleGrowth.ProductImage` |

### 3. Currency Purchase Packs (ShopUI)
| Product Card | Local File | Asset ID | Pack Value |
| :--- | :--- | :--- | :--- |
| **Shop_SpeedPack_1** | `speed_150K.png` | `rbxassetid://119092270160835` | +150,000 Speed |
| **Shop_SpeedPack_2** | `speed_1M.png` | `rbxassetid://139176416422321` | +1,000,000 Speed |
| **Shop_SpeedPack_3** | `speed_10M.png` | `rbxassetid://107053933186192` | +10,000,000 Speed |
| **Shop_SpeedPack_4** | `speed_50M.png` | `rbxassetid://75648789803465` | +50,000,000 Speed |
| **Shop_SpeedPack_5** | `speed_500M.png` | `rbxassetid://111286817352247` | +500,000,000 Speed |
| **Shop_SpeedPack_6** | `speed_1B.png` | `rbxassetid://112758064821059` | +1,000,000,000 Speed |
| **Shop_MoneyPack_1** | `cash_24K.png` | `rbxassetid://84166498696583` | $24,000 Cash |
| **Shop_MoneyPack_2** | `cash_200K.png` | `rbxassetid://124079293208806` | $200,000 Cash |
| **Shop_MoneyPack_3** | `cash_800K.png` | `rbxassetid://128438064314529` | $800,000 Cash |
| **Shop_MoneyPack_4** | `cash_4M.png` | `rbxassetid://71754785499935` | $4,000,000 Cash |
| **Shop_MoneyPack_5** | `cash_8M.png` | `rbxassetid://73983080306365` | $8,000,000 Cash |

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
