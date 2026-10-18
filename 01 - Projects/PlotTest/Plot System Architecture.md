---
title: PlotTest - Plot System Architecture
categories:
  - "[[Projects]]"
tags:
  - project
  - roblox
  - architecture
  - luau
created: 2026-10-18
status: active
---

# 🏛️ PlotTest - Plot System Architecture

> **Detailed technical specification for modular plot claiming, dynamic template instantiation, client-server replication, and Trove lifecycle management.**

Parent Hub: [[01 - Projects/PlotTest/PlotTest|PlotTest]] · Flagship Game: [[01 - Projects/Steal A Crate/Steal A Crate|Steal A Crate]]

---

## 📐 DataModel & Workspace Hierarchy

```text
Workspace
├── Plots
│   ├── Plot_01 (Model)
│   │   ├── PlotRoot (Part: Anchored=true, Transparency=1, CanCollide=false)
│   │   ├── Bounds (Part: Visual plot boundary frame)
│   │   └── SpawnLocation (SpawnLocation: Team/Neutral)
│   ├── Plot_02 ...
│   └── Plot_08 ...
ServerScriptService
└── Server
    ├── Services
    │   └── PlotService.luau (Manages allocation, player binding, lifecycle)
    └── Classes
        └── PlotInstance.luau (OOP wrapper per allocated plot with Trove)
ReplicatedStorage
└── Shared
    ├── Remotes
    │   └── PlotClaimed (RemoteEvent: Server -> Client)
    └── Types
        └── PlotTypes.luau (Strict type contracts)
```

---

## 🔒 Cardinal Engineering Rules for Plots

1. **Zero Raw Primitives Construction**:
   - Plots are cloned from pre-configured master templates stored in `ServerStorage.Templates.PlotTemplate` rather than constructed iteratively via code.
2. **Pivot-to-Ground Mathematical Alignment**:
   - Every `PlotTemplate` must have its `PrimaryPart` at the bottom center of the foundation plate $(Y=0)$.
   - Placement strictly uses `clonedPlot:PivotTo(plotRoot.CFrame)`.
3. **Deterministic Memory Cleanup (Trove)**:
   - Every `PlotInstance` owns an internal `Trove`.
   - When a player leaves or the plot resets, calling `plotInstance:Destroy()` must:
     - Disconnect all internal ProximityPrompt signals.
     - Cancel ongoing tweens.
     - Call `trove:Clean()`.
     - Explicitly destroy the cloned workspace model.

---

## 📋 Strict Luau Interface Contract

```luau
--!strict
export type PlotState = "Available" | "Claimed" | "Reserved"

export type PlotData = {
    Owner: Player?,
    PlotId: number,
    RootCFrame: CFrame,
    Level: number,
    State: PlotState,
}

export type PlotInstance = {
    Data: PlotData,
    Model: Model?,
    Claim: (self: PlotInstance, player: Player) -> boolean,
    Release: (self: PlotInstance) -> (),
    Destroy: (self: PlotInstance) -> (),
}
```

---

## 🔗 Related Vault Notes
- [[01 - Projects/PlotTest/PlotTest|PlotTest Project Hub]]
- [[02 - Areas/Roblox Luau Engineering|Roblox Luau Engineering]]
- [[03 - Resources/Luau Production Cheatsheet|Luau Production Cheatsheet]]
