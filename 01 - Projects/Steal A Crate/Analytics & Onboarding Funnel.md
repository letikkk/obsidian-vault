---
title: Steal A Crate - Analytics & Onboarding Funnel
tags:
  - project
  - roblox
  - analytics
  - funnel
created: 2026-10-22
status: active
---

# 📊 Steal A Crate - Analytics & Onboarding Funnel

> **Game-specific funnel tracking for player acquisition, tutorial completion, and heist retention.**  
> Parent Hub: [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]  
> Global Spec: [[03 - Resources/Analytics & Onboarding Funnel Architecture|Analytics & Onboarding Funnel Architecture]]

---

## 🎯 Game Milestones & Step Breakdowns

### Funnel: Tutorial (3 шага)
- **Step 1: Purchase** — Игрок покупает деревянную биту в лобби через Check-UI Shop.
- **Step 2: Collect** — Игрок поднимает стартовый учебный ящик `Crate_Wood_01`.
- **Step 3: Sell** — Игрок заносит ящик в зеленый `SellZone` ([[03 - Resources/ZonePlus Spatial Engine|ZonePlus]]) и получает первые $50.

### Funnel: FirstHeist (4 шага)
- **Step 1: CrossSafeZone** — Игрок покидает SafeZone и входит в Wilderness.
- **Step 2: CollectRareCrate** — Подбор первого тяжелого ящика ($150+).
- **Step 3: RagdollSurvive** — Получение удара битой от соперника и восстановление через Ragdoll.
- **Step 4: DepositBank** — Успешная сдача украденного ящика в свою базу.

### Funnel: CoreProgression (3 шага)
- **Step 1: TreadmillTraining** — Накопление +5 Speed на беговой дорожке.
- **Step 2: UpgradeBackpack** — Покупка рюкзака на 2 слота ящиков.
- **Step 3: FirstRebirth** — Выполнение Rebirth 1 (требуется $50,000).

### Funnel: Monetization (3 шага)
- **Step 1: OpenShop** — Переход во вкладку GamePasses в меню.
- **Step 2: PromptPass** — Клик по GamePass `2x Speed` или `VIP Crate Radar`.
- **Step 3: CompletePurchase** — Подтверждение транзакции через Roblox Dialog.
