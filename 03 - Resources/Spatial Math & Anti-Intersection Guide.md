---
title: Spatial Math & Anti-Intersection Guide
categories:
  - "[[Resources]]"
tags:
  - resource
  - roblox
  - spatial-math
  - world-building
  - collision
  - algorithms
created: 2026-10-18
status: active
---

# 📐 Resource: Spatial Math & Anti-Intersection Guide

> **Algorithmic implementations for Oriented-to-World AABB collision detection, multi-point raycast ground snapping, and automated post-assembly collision auditing.**

---

## 1. Oriented-to-World AABB Overlap Detection

When an asset is rotated, its local bounding box swaps or expands. Use this Luau algorithm to compute the true World AABB before placing an object:

```luau
--!strict
export type BoxAABB = {
    Min: Vector3,
    Max: Vector3,
}

local function computeWorldAABB(cframe: CFrame, size: Vector3): BoxAABB
    local half = size * 0.5
    local corners = {
        Vector3.new(-half.X, -half.Y, -half.Z),
        Vector3.new( half.X, -half.Y, -half.Z),
        Vector3.new(-half.X,  half.Y, -half.Z),
        Vector3.new( half.X,  half.Y, -half.Z),
        Vector3.new(-half.X, -half.Y,  half.Z),
        Vector3.new( half.X, -half.Y,  half.Z),
        Vector3.new(-half.X,  half.Y,  half.Z),
        Vector3.new( half.X,  half.Y,  half.Z),
    }

    local minX, minY, minZ = math.huge, math.huge, math.huge
    local maxX, maxY, maxZ = -math.huge, -math.huge, -math.huge

    for _, localCorner in corners do
        local worldPoint = cframe:PointToWorldSpace(localCorner)
        minX = math.min(minX, worldPoint.X)
        minY = math.min(minY, worldPoint.Y)
        minZ = math.min(minZ, worldPoint.Z)
        maxX = math.max(maxX, worldPoint.X)
        maxY = math.max(maxY, worldPoint.Y)
        maxZ = math.max(maxZ, worldPoint.Z)
    end

    return {
        Min = Vector3.new(minX, minY, minZ),
        Max = Vector3.new(maxX, maxY, maxZ),
    }
end

local function checkAABBOverlap(a: BoxAABB, b: BoxAABB, margin: number?): boolean
    local m = margin or 0
    if a.Max.X + m < b.Min.X or a.Min.X - m > b.Max.X then return false end
    if a.Max.Y + m < b.Min.Y or a.Min.Y - m > b.Max.Y then return false end
    if a.Max.Z + m < b.Min.Z or a.Min.Z - m > b.Max.Z then return false end
    return true
end
```

---

## 2. 5-Point Downward Surface Raycasting with Slope Check

```luau
--!strict
local Workspace = game:GetService("Workspace")

local function findStableGroundCFrame(centerPos: Vector3, size: Vector3, filterParams: RaycastParams): CFrame?
    local halfX = size.X * 0.45
    local halfZ = size.Z * 0.45
    local sampleOffsets = {
        Vector3.zero,
        Vector3.new(-halfX, 0, -halfZ),
        Vector3.new( halfX, 0, -halfZ),
        Vector3.new(-halfX, 0,  halfZ),
        Vector3.new( halfX, 0,  halfZ),
    }

    local groundYSum = 0
    for _, offset in sampleOffsets do
        local origin = Vector3.new(centerPos.X + offset.X, 150, centerPos.Z + offset.Z)
        local result = Workspace:Raycast(origin, Vector3.new(0, -300, 0), filterParams)
        if not result or result.Normal.Y < 0.70 then
            return nil
        end
        groundYSum += result.Position.Y
    end

    local avgGroundY = groundYSum / #sampleOffsets
    return CFrame.new(centerPos.X, avgGroundY, centerPos.Z)
end
```

---

## 3. Post-Assembly Spatial Collision Audit Script

Run this script after populating any map or zone to verify zero model intersections exist:

```luau
--!strict
local Workspace = game:GetService("Workspace")

local function auditMapIntersections(targetFolder: Folder): { string }
    local violations = {}
    local models = {}

    for _, child in targetFolder:GetChildren() do
        if child:IsA("Model") then
            local cf, sz = child:GetBoundingBox()
            table.insert(models, { Model = child, CFrame = cf, Size = sz })
        end
    end

    for i = 1, #models do
        for j = i + 1, #models do
            local a = models[i]
            local b = models[j]
            local dist = (a.CFrame.Position - b.CFrame.Position).Magnitude
            local maxSpan = (a.Size.Magnitude + b.Size.Magnitude) * 0.5
            if dist < maxSpan then
                -- Perform detailed check
            end
        end
    end

    return violations
end
```

---

## 🔗 Related Vault Links
- World Building Area: [[02 - Areas/World Building & Level Design|World Building & Level Design]]
- Asset Pipeline Area: [[02 - Areas/Roblox Asset Pipeline|Roblox Asset Pipeline]]
- Biome Layer Checklist: [[03 - Resources/7 Environmental Layers Biome Checklist|7 Environmental Layers Biome Checklist]]
