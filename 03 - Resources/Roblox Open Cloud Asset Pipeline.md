---
title: Roblox Open Cloud Asset Pipeline
tags:
  - resource
  - roblox
  - open-cloud
  - assets
  - automation
created: 2026-10-22
status: active
---

# ☁️ Resource: Roblox Open Cloud Asset Pipeline

> **Automated asset publishing directly to Roblox Studio via Open Cloud API.**  
> API Key Location: `C:\Users\meepo\Documents\antigravity\Steal-A-Crate\roblox_cloud_key.txt`

---

## 🔑 Authentication & Configuration

The secret Open Cloud API Key is stored locally at:
```
C:\Users\meepo\Documents\antigravity\Steal-A-Crate\roblox_cloud_key.txt
```

This key authorizes direct programmatic uploading of:
- **Audio:** `.mp3`, `.ogg`
- **Images & Decals:** `.png`, `.jpeg`, `.tga`
- **3D Meshes & Models:** `.fbx`, `.obj`

---

## 🚀 Python Automated Asset Uploader Script

Save and run this script to instantly upload sound effects, UI icons, or 3D models into Roblox and obtain their asset IDs:

```python
import os
import json
import requests

KEY_PATH = r"C:\Users\meepo\Documents\antigravity\Steal-A-Crate\roblox_cloud_key.txt"

with open(KEY_PATH, "r", encoding="utf-8") as f:
    API_KEY = f.read().strip()

def upload_asset(file_path: str, asset_type: str, display_name: str, description: str = ""):
    url = "https://apis.roblox.com/assets/v1/assets"
    
    headers = {
        "x-api-key": API_KEY,
    }
    
    payload = {
        "assetType": asset_type,
        "displayName": display_name,
        "description": description,
        "creationContext": {
            "creator": {
                "userId": "YOUR_USER_ID"
            }
        }
    }
    
    with open(file_path, "rb") as f:
        files = {
            "request": (None, json.dumps(payload), "application/json"),
            "fileContent": (os.path.basename(file_path), f, "application/octet-stream")
        }
        
        response = requests.post(url, headers=headers, files=files)
        
    if response.status_code == 200:
        data = response.json()
        print("Asset Upload Initiated:", data)
        return data
    else:
        print("Upload Failed:", response.status_code, response.text)
        return None
```

---

## 🛠️ Open Cloud Asset Types Reference

| File Extension | Open Cloud `assetType` | Roblox Class | Use Case |
| :--- | :--- | :--- | :--- |
| `.mp3`, `.ogg` | `Audio` | `Sound` | SFX удара биты, сбор ящика, фоновый саундтрек. |
| `.png` | `Decal` | `Decal` / `ImageLabel` | Check-UI иконки, текстуры ящиков, градиенты. |
| `.fbx`, `.obj` | `Model` | `MeshPart` | Низкополигональные ящики, воксельные персонажи. |

---

## 🔗 Integrated Catalog

After obtaining asset IDs via Open Cloud, record them into:
- [[03 - Resources/Local Audio & UI Asset Catalog|Local Audio & UI Asset Catalog]]
- [[01 - Projects/Steal A Crate/Technical Reference|Steal A Crate Technical Reference]]
