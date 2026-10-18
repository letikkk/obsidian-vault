---
title: Roblox Luau Engineering
categories:
  - "[[Areas]]"
tags:
  - area
  - roblox
  - engineering
  - luau
  - architecture
created: 2026-10-18
status: active
---

# ⚡ Area: Roblox Luau Engineering

> **Production engineering standards, architectural design patterns, and exploit-resistant network models for professional Roblox Studio games.**  
> Grounded in strict typing, zero-trust server validation, Trove deterministic memory lifecycles, and modular services.

---

## 🏛️ The 4 Cardinal Architectural Patterns

Roblox experiences must strictly separate responsibilities into four distinct architectural layers based on data ownership and simulation throughput:

```mermaid
flowchart TD
    subgraph S1 ["1. Singleton Services & Controllers"]
        SVC["Coordination & Global Endpoints<br/>(EconomyService, PlayerDataService, UIController)"]
    end
    subgraph S2 ["2. Object-Oriented Classes (OOP)"]
        OOP["Stateful Discrete Entities with Lifecycles<br/>(Weapons, Pets, Vehicles, PlotInstances)"]
    end
    subgraph S3 ["3. CollectionService Components"]
        COMP["Tagged World Objects Behavior<br/>(Chests, RebirthPads, ProximityDoors, HazardZones)"]
    end
    subgraph S4 ["4. Entity-Component-System (ECS)"]
        ECS["Mass High-Throughput Simulation<br/>(Floating Orbs, Projectiles, Swarms, Dropped Coins)"]
    end
    
    SVC --> OOP & COMP
    OOP --> COMP
    SVC --> ECS
```

| Pattern | Primary Domain | Memory Management | Key Characteristics |
| :--- | :--- | :--- | :--- |
| **Singleton Service / Controller** | Global coordination, remotes, external APIs, persistent game loops. | Initialized at boot; lives for server lifetime. | Service-Controller pattern; cross-communicates via `require`. |
| **Object-Oriented Programming (OOP)** | Discrete stateful game entities with identity and lifespan. | Owned by a `Trove`; explicit `:Destroy()` method. | Metatables with `__index`; sealed typed table constructors. |
| **CollectionService Components** | 3D Workspace models placed by level designers. | Lifecycle bound to `GetInstanceAddedSignal` and instance deletion. | Single responsibility bound to tag; zero code embedded inside parts. |
| **Entity-Component-System (ECS)** | Thousands of uniform, lightweight spatial entities. | Flat arrays / continuous typed buffers. | Pure data tables, integer IDs, zero-allocation iterators on `Heartbeat`. |

---

## 📜 The Non-Negotiable Engineering Rules

1. **Zero Comments Policy:**
   - Never write comments (`-- ...` or `--[[ ... ]]`) in production Luau.
   - The only allowed directives are compiler headers on line 1: `--!strict` (and optional `--!native` or `--!optimize 2`).
   - Self-documenting code through unambiguous naming and explicit type annotations is mandatory.
2. **Zero Prints Policy:**
   - Production code must never execute `print(...)`.
   - Alert developers strictly through `warn(...)` for actionable errors.
   - Track analytics through `AnalyticsService`.
3. **Zero Procedural UI Generation:**
   - Never instantiate UI hierarchies via code (`Instance.new("ScreenGui")`, `Instance.new("Frame")`, etc.).
   - All UI must be pre-built in `StarterGui` under [[02 - Areas/Check-UI Design System|Check-UI]] guidelines. Luau programmers only perform **Controller Binding**.
4. **100% Strict Type Safety (`--!strict`):**
   - Every file begins with `--!strict`.
   - Export explicit type definitions for network payloads, state objects, and class tables.
5. **Server-Authoritative Networking (Zero-Trust Client):**
   - Clients send *intent* only (e.g., `RequestBuyItem`, `RequestSwingBat`).
   - The server validates cooldowns, prices, inventories, and spatial raycast distance.
   - Enforce zero-allocation token-bucket rate limiters on all incoming remote events.
6. **Deterministic Memory Cleanup (Trove / Janitor):**
   - Never leave event connections or tweens dangling.
   - Every class, component, and temporary visual effect must be tied to a `Trove`.
7. **Modern Task Library Exclusivity:**
   - Never use `wait()`, `spawn()`, or `delay()`.
   - Always use `task.wait()`, `task.spawn()`, `task.defer()`, `task.delay()`, `task.cancel()`.
8. **Player Lifecycle Completeness:**
   - Always iterate existing players (`for _, player in Players:GetPlayers() do`) upon service boot before connecting `Players.PlayerAdded`.
   - Always release player locks and state on `Players.PlayerRemoving`.

---

## 🗄️ Standard Directory Standard

```text
ReplicatedStorage/Shared
├── Config          # Static balance tables, constants, asset registries
├── Classes         # Replicated OOP class modules
├── Components      # ECS component definitions
├── Modules         # Trove, FastSignal, ObjectPool, RateLimiter
├── Remotes         # RemoteEvents, RemoteFunctions
└── Types           # Strict type contracts
ServerScriptService/Server
├── Services        # PlayerDataService, EconomyService, PlotService
├── Classes         # Server-side entity classes
├── Components      # CollectionService tagged world components
└── Systems         # ECS simulation systems
```

---

## 🔗 Related Vault Links
- Active Project: [[01 - Projects/Steal A Crate/System Architecture|Steal A Crate System Architecture]]
- Modular Sandbox: [[01 - Projects/PlotTest/PlotTest|PlotTest]]
- Production Templates: [[03 - Resources/Luau Production Cheatsheet|Luau Production Cheatsheet]]
- UI Binding: [[02 - Areas/Check-UI Design System|Check-UI Design System]]
