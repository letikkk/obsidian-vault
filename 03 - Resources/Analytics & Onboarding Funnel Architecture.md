---
title: Analytics & Onboarding Funnel Architecture
tags:
  - resource
  - roblox
  - analytics
  - funnel
  - retention
created: 2026-10-22
status: active
---

# 📊 Resource: Analytics & Onboarding Funnel Architecture

> **Standard for tracking player progression, retention drops, and conversion funnels.**  
> Grounded in Roblox `AnalyticsService:LogOnboardingFunnelStepEvent` and custom event metrics.  
> **Mandate:** Every key game milestone MUST declare a dedicated `Funnel` section enumerating all internal steps.

---

## 🎯 Global Funnel Registry & Standards

### Funnel: Tutorial (First Time User Experience)
- **Step 1: Purchase** — Покупка стартового снаряжения/биты в лобби.
- **Step 2: Collect** — Подбор первого ящика на учебной поляне.
- **Step 3: Sell** — Сдача ящика в базу с зачислением первой игровой валюты.

### Funnel: FirstHeist (First Out-of-Safezone Raid)
- **Step 1: CrossSafeZone** — Выход за пределы защищенной зоны спавна (отслеживается через [[03 - Resources/ZonePlus Spatial Engine|ZonePlus]]).
- **Step 2: LootCrate** — Подбор первого дикого ящика (Common, Rare, Epic).
- **Step 3: RagdollSurvive** — Получение первого удара битой или ловушки с успешным подъемом.
- **Step 4: BankCrate** — Возвращение в безопасную зону и успешный депозит.

### Funnel: CoreProgression (Simulator Loop)
- **Step 1: TreadmillTrain** — Вход на беговую дорожку и получение первого бонуса к скорости.
- **Step 2: CapacityUpgrade** — Покупка рюкзака повышенной вместимости.
- **Step 3: FirstRebirth** — Выполнение первого перерождения с получением перманентного множителя.

### Funnel: Monetization (Shop & GamePass Conversion)
- **Step 1: OpenShop** — Открытие магазина Check-UI.
- **Step 2: InspectItem** — Просмотр описания товара (GamePass, Boost, DevProduct).
- **Step 3: PromptPurchase** — Вызов `MarketplaceService:PromptGamePassPurchase`.
- **Step 4: PurchaseSuccess** — Успешное завершение транзакции и начисление бонуса.

---

## ⚡ AnalyticsService Funnel Tracker Implementation

```luau
--!strict
--[SERVICES]--
local AnalyticsService = game:GetService("AnalyticsService")
local Players = game:GetService("Players")

--[VARIABLES]--
local FunnelService = {}

local FUNNEL_CONFIG = {
	Tutorial = {
		[1] = "Purchase",
		[2] = "Collect",
		[3] = "Sell",
	},
	FirstHeist = {
		[1] = "CrossSafeZone",
		[2] = "LootCrate",
		[3] = "RagdollSurvive",
		[4] = "BankCrate",
	},
	CoreProgression = {
		[1] = "TreadmillTrain",
		[2] = "CapacityUpgrade",
		[3] = "FirstRebirth",
	},
	Monetization = {
		[1] = "OpenShop",
		[2] = "InspectItem",
		[3] = "PromptPurchase",
		[4] = "PurchaseSuccess",
	},
}

--[FUNCTIONS]--
function FunnelService.LogStep(player: Player, funnelName: string, stepIndex: number)
	local steps = FUNNEL_CONFIG[funnelName]
	if not steps then return end
	
	local stepName = steps[stepIndex]
	if not stepName then return end

	pcall(function()
		AnalyticsService:LogOnboardingFunnelStepEvent(player, stepIndex, stepName)
	end)
end

return FunnelService
```
