---
title: Steal A Crate - Game Design Document
categories:
  - "[[Projects]]"
  - "[[Games]]"
tags:
  - project
  - roblox
  - gdd
  - design
created: 2026-10-15
status: active
---

# 🎮 Steal A Crate - Game Design Document

> **Game Design Document (GDD) specifying core loops, game feel, player dynamics, physics balancing, and progression curves.**

Parent Hub: [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]

---

## 🎯 Game Pillars

1. **Risk vs. Reward Physics:** Larger, rarer crates grant massive cash, but encumber the player with heavy movement slowdown and disable jumping, making them easy targets.
2. **Hilarious Physical Comedy:** Non-lethal combat with exaggerated ragdoll flings (50 to 150 studs) creates high-energy, memorable streamer-friendly moments.
3. **Continuous Progression:** Idle/training loops (treadmills) feed directly into heist viability, enabling players to haul heavier crates faster.

---

## 🔄 Core Mechanics Breakdown

### 1. Crate Weight & Carrying Physics
- **Randomized Spawning:** Crates spawn across wilderness zones with randomized sizes (0.7x to 2.2x scale) and rarity tiers (Common, Rare, Epic, Legendary).
- **Weight Calculation:** Crate mass scales with volume (`Scale^3`).
- **Encumbrance Formula:**
  $$\text{Speed Penalty} = \min\left(0.65, \frac{\text{Mass}}{\text{MaxMass}}\right)$$
  $$\text{Effective Speed} = \text{BaseSpeed} \times (1 - \text{Speed Penalty})$$
- **Jumping Restriction:** Crates exceeding 1.4x scale completely disable jumping to force tactical navigation through canyon bottlenecks.

---

### 2. Combat & Defense Tools

#### 🏏 The Bat
- **Input:** Left-Mouse-Button (PC) / Screen Tap (Mobile).
- **Animation:** Crisp, non-looping baseball swing animation.
- **Hitbox:** Forward cone raycast (7 studs reach, 120° horizontal arc).
- **Effect on Hit:**
  - Victim ragdolls immediately.
  - Victim is flung backward by **~150 studs** along the attacker's forward look vector.
  - Victim immediately drops any held crate.

#### 🪤 The Bear Trap
- **Inventory Limit:** Max **5 traps** held simultaneously.
- **Placement:** Drops on the floor directly beneath the player with raycast normal alignment.
- **Trigger Conditions:**
  - Stepped on by another player or roaming enemy.
  - Automatically snaps shut, ragdolls victim, and forces crate drop.
- **Replenishment Cycle:**
  - Triggers on contact $\rightarrow$ charges back to owner.
  - Expires after **60 seconds** untouched $\rightarrow$ despawns and refunds 1 charge back to owner.

---

### 3. Training & Base Infrastructure

#### 🏃 The Treadmill
- **Training Frequency:** Grants `+Speed` every **0.2 seconds** while running on the belt.
- **Visual Feedback:** High-speed floating popup (`+Speed`) scales up from center and fades out 3x faster than standard notifications to prevent screen clutter during high-frequency ticks.

#### 🏡 Plot Roots & PlotTemplate
- Maps use clean `PlotRoot` markers instead of hardcoded static plots.
- On player join, `ReplicatedStorage.Templates.PlotTemplate` clones to the player's assigned plot root.
- All persistent player upgrades (hatch upgrades, base walls, decoration) bind to the instantiated template.

---

## 🗺️ Zone Design & Progression

```
[Safe Zone 🛡️] ────► [Forest 🙂] ────► [Beach 🏖️] ────► [Snow ❄️]
  (Z > -65.5)       (-140.5 <= Z <= -65.5)   (-235.5 <= Z <= -140.5)     (Z < -235.5)
```

| Zone | Z Boundary | Difficulty | Crate Multiplier | Visual Identifier |
| :--- | :--- | :--- | :--- | :--- |
| **Safe Zone 🛡️** | $Z > -65.5$ | None (PvP Off) | N/A (Deliveries only) | Lush green lawn, player plots, treadmills |
| **Forest 🙂** | $-140.5 \le Z \le -65.5$ | Low | $1.0\times - 2.5\times$ | Dense trees, low enemy density |
| **Beach 🏖️** | $-235.5 \le Z \le -140.5$ | Medium | $3.0\times - 6.0\times$ | Open sand, high player sightlines |
| **Snow ❄️** | $Z < -235.5$ | Hard | $8.0\times - 20.0\times$ | Ice obstacles, elite roaming enemies |
