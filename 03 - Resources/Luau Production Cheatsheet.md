---
title: Luau Production Cheatsheet
categories:
  - "[[Resources]]"
tags:
  - resource
  - roblox
  - luau
  - code-snippets
  - cheatsheet
created: 2026-10-18
status: active
---

# 💻 Resource: Luau Production Cheatsheet

> **Verified, production-grade Luau code templates adhering to strict typing (`--!strict`), zero comments, zero prints, and Trove lifecycle management.**

---

## 1. Strict Singleton Service Boilerplate

```luau
--!strict
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local Trove = require(ReplicatedStorage.Shared.Modules.Trove)

local PlayerService = {}
PlayerService.__index = PlayerService

local _trove = Trove.new()

local function onPlayerAdded(player: Player)
    local playerTrove = _trove:Extend()
    playerTrove:Add(player.CharacterAdded:Connect(function(character)
        
    end))
end

local function onPlayerRemoving(player: Player)
    
end

function PlayerService.Init()
    for _, player in Players:GetPlayers() do
        task.spawn(onPlayerAdded, player)
    end
    _trove:Add(Players.PlayerAdded:Connect(onPlayerAdded))
    _trove:Add(Players.PlayerRemoving:Connect(onPlayerRemoving))
end

function PlayerService.Destroy()
    _trove:Clean()
end

return PlayerService
```

---

## 2. Strict OOP Class Boilerplate (Sealed Table Typing)

```luau
--!strict
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Trove = require(ReplicatedStorage.Shared.Modules.Trove)

export type WeaponInstance = {
    Owner: Player,
    Model: Model,
    Damage: number,
    Cooldown: number,
    LastAttackTime: number,
    Attack: (self: WeaponInstance, target: Model) -> boolean,
    Destroy: (self: WeaponInstance) -> (),
}

local WeaponClass = {}
WeaponClass.__index = WeaponClass

function WeaponClass.new(owner: Player, model: Model, damage: number, cooldown: number): WeaponInstance
    local trove = Trove.new()
    
    local self = setmetatable({
        Owner = owner,
        Model = model,
        Damage = damage,
        Cooldown = cooldown,
        LastAttackTime = 0,
        _trove = trove,
    }, WeaponClass) :: any

    trove:Add(model.Destroying:Connect(function()
        self:Destroy()
    end))

    return self
end

function WeaponClass:Attack(target: Model): boolean
    local now = os.clock()
    if now - self.LastAttackTime < self.Cooldown then
        return false
    end
    self.LastAttackTime = now
    return true
end

function WeaponClass:Destroy()
    self._trove:Clean()
end

return WeaponClass
```

---

## 3. Strict CollectionService Component Boilerplate

```luau
--!strict
local CollectionService = game:GetService("CollectionService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Trove = require(ReplicatedStorage.Shared.Modules.Trove)

local TAG_NAME = "InteractiveChest"

local ChestComponent = {}
ChestComponent.__index = ChestComponent

local _instances: { [Instance]: any } = {}

local function onInstanceAdded(instance: Instance)
    if not instance:IsA("Model") then
        return
    end

    local trove = Trove.new()
    local prompt = instance:FindFirstChildWhichIsA("ProximityPrompt", true)
    if prompt then
        trove:Add(prompt.Triggered:Connect(function(player)
            
        end))
    end

    _instances[instance] = trove
end

local function onInstanceRemoved(instance: Instance)
    local trove = _instances[instance]
    if trove then
        trove:Clean()
        _instances[instance] = nil
    end
end

function ChestComponent.Init()
    for _, instance in CollectionService:GetTagged(TAG_NAME) do
        task.spawn(onInstanceAdded, instance)
    end
    CollectionService:GetInstanceAddedSignal(TAG_NAME):Connect(onInstanceAdded)
    CollectionService:GetInstanceRemovedSignal(TAG_NAME):Connect(onInstanceRemoved)
end

return ChestComponent
```

---

## 4. Zero-Allocation Token-Bucket Rate Limiter

```luau
--!strict
export type RateLimiter = {
    Check: (self: RateLimiter, player: Player) -> boolean,
    Cleanup: (self: RateLimiter, player: Player) -> (),
}

local RateLimiterClass = {}
RateLimiterClass.__index = RateLimiterClass

function RateLimiterClass.new(capacity: number, refillRatePerSec: number): RateLimiter
    local tokens: { [Player]: number } = {}
    local lastRefills: { [Player]: number } = {}

    local self = setmetatable({}, RateLimiterClass)

    function self:Check(player: Player): boolean
        local now = os.clock()
        local currentTokens = tokens[player] or capacity
        local lastRefill = lastRefills[player] or now
        local elapsed = now - lastRefill

        currentTokens = math.min(capacity, currentTokens + elapsed * refillRatePerSec)
        lastRefills[player] = now

        if currentTokens >= 1 then
            tokens[player] = currentTokens - 1
            return true
        end

        tokens[player] = currentTokens
        return false
    end

    function self:Cleanup(player: Player)
        tokens[player] = nil
        lastRefills[player] = nil
    end

    return self :: any
end

return RateLimiterClass
```

---

## 🔗 Related Vault Links
- Architecture Area: [[02 - Areas/Roblox Luau Engineering|Roblox Luau Engineering]]
- Active System: [[01 - Projects/Steal A Crate/System Architecture|Steal A Crate System Architecture]]
- Plot Sandbox: [[01 - Projects/PlotTest/Plot System Architecture|Plot System Architecture]]
