---
title: Steal A Crate - Tasks & Roadmap
categories:
  - "[[Projects]]"
tags:
  - project
  - roblox
  - tasks
  - roadmap
created: 2026-10-15
status: active
---

# 📋 Steal A Crate - Tasks & Roadmap

> **Active development roadmap, completed features, and sprint backlog powered by Obsidian's `Tasks` plugin.**

Parent Hub: [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]] · Kanban: [[01 - Projects/Project Kanban|Project Kanban]]

---

## 🚀 Active Sprint & In Progress

- [ ] Connect Obsidian vault notes with repository git workflow #low

---

## ✅ Completed Milestones

### Combat & Ragdoll Engine
- [x] Add sound effect when Bat successfully connects with another player #high
- [x] Implement visual trap placement indicator (hologram wireframe preview before drop) #medium
- [x] Add crate opening particle burst effect when opening at the base hatch #medium

### Core Mechanics & Physics
- [x] Implement randomized crate scale (0.7x to 2.2x) and mass tiering #high
- [x] Implement dynamic carrying slowdown based on crate weight #high
- [x] Implement dual-arm hold weld and automatic drop on damage #high
- [x] Build modular `PlotTemplate` and `PlotRoots` dynamic instantiation on player join #high
- [x] Build treadmill speed training granting stats every 0.2s with ultra-fast popups #medium

### Combat & Ragdoll Engine
- [x] Create non-lethal constraint-based ragdoll module inspired by *Steal an Egg* #high
- [x] Implement enemy hit reaction with ~50 studs fling impulse #high
- [x] Build Bat weapon with directional raycast hitbox on LMB / Mobile tap #high
- [x] Fix bat swing animation looping bug (proper one-shot playback) #high
- [x] Set Bat hit impulse to fling victims ~150 studs and drop crates #high
- [x] Build Trap weapon with 5-charge maximum stock #high
- [x] Implement trap auto-despawn and charge replenishment after 60s or upon trigger #high

### User Interface & Game Feel (`Check-UI`)
- [x] Port notification stack from *Collect a Snack* into `PlayerGui.Main.Messages` #medium
- [x] Import notification audio cues (`NotificationPop`, `SuccessSound`, `ErrorSound`, `ButtonClick`) #medium
- [x] Build 5 notification gradient presets (`Normal`, `Success`, `Robux`, `Rolled`, `Error`) #medium
- [x] Build live `LeaderstatsHUD` displaying real-time Cash and Speed #medium
- [x] Create Zone Entering UI banner (`Forest 🙂`, `Beach 🏖️`, `Snow ❄️`, `Safe Zone 🛡️`) #high
- [x] Refactor zone banner to permanent `StarterGui.Main.ZoneBanner` Frame #high
- [x] Fix half-transparent text issue: isolate UIGradient to Background Frame for 100% solid text #high
- [x] Connect Check-UI HUD menus: ShopUI, PetIndexUI, GrowingCratesUI, and EquippedPetsUI #high
- [x] Implement AnalyticsService onboarding funnels (Tutorial, FirstHeist, CoreProgression) #high ✅ 2026-10-25

---

## 🔮 Backlog & Future Milestones

### Milestone 1: Economy & Upgrades
- [ ] Build Plot upgrade store (expanded holding pens, faster conveyor belts) #medium
- [ ] Implement rebirth system multiplying base speed gains #high
- [ ] Build crate sell multiplier upgrades #medium

### Milestone 2: Cosmetics & Social
- [ ] Daily login streak rewards wheel #medium
- [ ] Trails & Pet eggs hatching station #low
- [ ] Global speed & cash leaderboards in Safe Zone hub #low
- [ ] Mobile UI controls polishing (custom thumbstick styling) #low
