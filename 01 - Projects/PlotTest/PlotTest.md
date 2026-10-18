---
title: PlotTest
categories:
  - "[[Projects]]"
  - "[[Games]]"
type:
  - Roblox Engine Prototype
  - Luau
year: 2026
status: In Progress
priority: high
created: 2026-10-18
tags:
  - project
  - roblox
  - architecture
  - rojo
  - luau
  - plot-system
---

# 🏗️ Project: PlotTest

> **Modular plot base architecture and dynamic plot allocation engine.** Built with Rokit and Rojo 7.6.1, establishing an isolated sandbox for testing player base claiming, spatial isolation, dynamic model instancing, and clean Trove lifecycle boundaries for multiplayer Roblox simulators.

---

## 🗂️ Project Navigation Hub

| Section | Document | Description |
| :--- | :--- | :--- |
| 🏛️ **Architecture** | [[01 - Projects/PlotTest/Plot System Architecture\|Plot System Architecture]] | Claiming lifecycle, Trove memory bounds, spatial coordinate mapping. |
| 📋 **Global Sprint** | [[01 - Projects/Project Kanban\|Project Kanban]] | Active cross-project tasks and development milestones. |
| 📦 **Flagship Integration** | [[01 - Projects/Steal A Crate/Steal A Crate\|Steal A Crate]] | Target recipient of verified plot allocation modules. |

---

## 📌 Project Overview & Technical Setup

- **Local Repository:** `C:\Users\meepo\Documents\RobloxProjects\PlotTest`
- **Toolchain Manager:** Rokit (`rokit.toml` -> `rojo-rbx/rojo@7.6.1`)
- **Project Configuration:** `default.project.json`
- **Strict Typing:** `--!strict` enforced across all Luau files
- **Key Purpose:** Serve as the verified, modular foundation for all plot-based games (player plots, base building, conveyor placement, and safe-zone boundaries).

### Development Workflow

```bash
# Build binary or XML place file
rojo build -o "PlotTest.rbxlx"

# Start live sync server to Roblox Studio
rojo serve
```

---

## 🔄 Core Plot Lifecycle Flow

```mermaid
sequenceDiagram
    autonumber
    actor Player as Player
    participant Server as Server (PlotManager)
    participant Workspace as Workspace.Plots
    participant Data as ProfileStore

    Player->>Server: PlayerAdded (Joined Game)
    Server->>Server: Find unoccupied PlotRoot
    Server->>Workspace: Clone PlotTemplate to PlotRoot.CFrame
    Server->>Data: Load Player Plot Data (buildings, upgrades)
    Server->>Server: Bind Player Trove to Plot cleanup
    Server-->>Player: PlotAssigned (PlotID, Position)
    
    note over Player, Workspace: Gameplay loop: building, upgrading, storing crates

    Player->>Server: PlayerRemoving (Leaves Game)
    Server->>Data: Save & Session-Unlock Plot State
    Server->>Server: Clean Trove (Disconnect events, tweens)
    Server->>Workspace: Destroy Cloned Plot Hierarchy
    Server->>Server: Mark PlotRoot as Unoccupied
```

---

## 🛠️ Key Architectural Milestones

- [x] Initialized Rokit and Rojo 7.6.1 project structure.
- [x] Configured DataModel tree mapping (`Shared`, `Server`, `Client`).
- [ ] Implement `PlotManager` server service with thread-safe plot claiming.
- [ ] Implement spatial boundary fences with `CanQuery = false` performance optimization.
- [ ] Integrate Trove deterministic cleanup on plot unclaiming.
- [ ] Export production-ready module to `Steal A Crate` codebase.

---

## 👥 Related Vault Links
- Active Sprint: [[01 - Projects/Project Kanban|Project Kanban]]
- Architecture Spec: [[01 - Projects/PlotTest/Plot System Architecture|Plot System Architecture]]
- Luau Standards: [[02 - Areas/Roblox Luau Engineering|Roblox Luau Engineering]]
