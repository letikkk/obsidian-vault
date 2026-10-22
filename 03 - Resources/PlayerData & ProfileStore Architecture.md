---
title: PlayerData & ProfileStore Architecture
tags:
  - resource
  - roblox
  - datastore
  - profilestore
  - luau
created: 2026-10-22
status: active
---

# 💾 Resource: PlayerData & ProfileStore Architecture

> **Production DataStore persistence layer using ProfileStore.**  
> Enforces atomic session locking, auto-reconciliation, safe studio/live segregation, and clean initialization.

---

## 🏛️ Strict ProfileStore DataService Implementation

```luau
--[SERVICES]--
local ServerScriptService = game:GetService("ServerScriptService")
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

--[MODULES]--
local PlayerService = require(script.Parent:WaitForChild("PlayerService"))
local DataManager = require(script:WaitForChild("DataManager"))
local ProfileStore = require(ReplicatedStorage:WaitForChild("Shared"):WaitForChild("Libraries"):WaitForChild("ProfileStore"))
local Template = require(script:WaitForChild("Template"))

--[DATASTORE]--
local DataStore = ProfileStore.New(RunService:IsStudio() and "Test" or "Live", Template)

--[VARIABLES]--
local DataService = {}

--[FUNCTIONS]--
local function Initialize(plr: Player, profile: typeof(DataStore))
	local leaderstats = Instance.new("Folder")
	leaderstats.Parent = plr
	leaderstats.Name = "leaderstats"
	
	for name, value in Template.leaderstats do
		local val = Instance.new("NumberValue")
		val.Parent = leaderstats
		val.Name = name
		val.Value = profile.Data.leaderstats[name] or value
	end
	PlayerService.SetupPlayer(plr)
end

local function OnPlayerAdded(plr: Player)
	local profile = DataStore:StartSessionAsync(`Player_{plr.UserId}`,
		{Cancel = function()
			return plr.Parent ~= Players
		end,
		})
	
	if profile ~= nil then
		profile:AddUserId(plr.UserId)
		profile:Reconcile()
		
		profile.OnSessionEnd:Connect(function()
			DataManager.Profiles[plr] = nil
			plr:Kick("Session ended")
		end)
		
		if plr.Parent == Players then
			DataManager.Profiles[plr] = profile
			warn(`Loaded profile for {plr.Name}`)
			
			Initialize(plr, profile)
		else
			plr:Kick("error occured, please rejoin")
		end
	end
end

local function OnPlayerRemoving(plr: Player)
	local profile = DataManager.Profiles[plr]
	if not profile then return end
	
	profile:EndSession()
	DataManager.Profiles[plr] = nil
end

--[INITIALIZATION]--
function DataService.Init()
	for _, plr in Players:GetPlayers() do
		task.spawn(OnPlayerAdded, plr)
	end
	
	Players.PlayerAdded:Connect(function(plr: Player)
		task.spawn(OnPlayerAdded, plr)
	end)
	
	Players.PlayerRemoving:Connect(function(plr: Player)
		task.spawn(OnPlayerRemoving, plr)
	end)
end

return DataService
```

---

## 📋 Data Template Schema (`Template.luau`)

```luau
--[TEMPLATE]--
local Template = {
	leaderstats = {
		Cash = 0,
		Speed = 16,
		Rebirths = 0,
	},
	Inventory = {
		EquippedBat = "WoodenBat",
		EquippedBackpack = "CanvasBag",
		Traps = {},
	},
	Settings = {
		MuteAudio = false,
		RagdollAutoRecover = true,
	},
}

return Template
```

---

## 🗃️ Session Cache Manager (`DataManager.luau`)

```luau
--[TYPES]--
local DataManager = {
	Profiles = {} :: { [Player]: any },
}

return DataManager
```
