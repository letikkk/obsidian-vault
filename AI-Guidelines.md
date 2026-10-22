---
title: AI Agent Guidelines
tags:
  - meta
  - system
  - ai-agent
---

# 🤖 AI Agent Guidelines for This Vault

If you are an AI assistant or autonomous agent working in this vault, follow these rules:

### 1. File Placement
- **Unsure or Uncategorized:** Always write new notes into `00 - Inbox/`.
- **Project Specific:** Place inside `01 - Projects/<Project-Name>/`.
- **Atomic Concept / Knowledge:** Place inside `03 - Resources/`.
- **Daily Summaries / Logs:** Append to `Daily/YYYY-MM-DD.md`.
- **Media / Attachments:** Save images or binary files into `Assets/`.

### 2. Linking Conventions
- Use Obsidian's bidirectional format: `[[Target Note Name]]` or `[[Target Note Name|Display Text]]`.
- Do not use URL-encoded file links like `[link](Target%20Note.md)` unless explicitly requested.
- Maintain existing links when editing notes.

### 3. Frontmatter & Metadata
- Every new note should contain standard YAML frontmatter:
  ```yaml
  ---
  title: Note Title
  date: YYYY-MM-DD
  tags:
    - topic-name
  ---
  ```

### 4. Non-Destructive Edits
- When updating existing notes, preserve user notes, thoughts, and structure.
- When generating complex multi-step reasoning, use the format in `Templates/AI Agent Scratchpad Template.md`.

### 5. Strict Luau Code Commenting Standard
- **Only section header comments are permitted in Luau code:**
  Format: `--[SECTION_NAME]--` (e.g. `--[SERVICES]--`, `--[MODULES]--`, `--[VARIABLES]--`, `--[FUNCTIONS]--`, `--[INITIALIZATION]--`).
- **Zero inline chatter:** No docstrings, explanatory inline comments, or debug prints (`print`, `warn`) in production snippets. Keep the code clean and strictly organized by sections so the developer immediately knows where they are in the file.

### 6. Analytics & Onboarding Funnels
- Every key game milestone or player loop must declare a dedicated **`Funnel`** section.
- Inside the section, enumerate all sequential steps explicitly (e.g., `Tutorial` with steps `Purchase`, `Collect`, `Sell`).
- Link to [[03 - Resources/Analytics & Onboarding Funnel Architecture|Analytics & Onboarding Funnel Architecture]].

### 7. Core Production Libraries
- **Networking:** Always default to [[03 - Resources/Packet Networking Library|Packet]] (binary buffer serialization, type safety).
- **Spatial Zones:** Always default to [[03 - Resources/ZonePlus Spatial Engine|ZonePlus v3.2.0]] (dynamic zones, zero idle physics drag).
- **Data Persistence:** Always default to [[03 - Resources/PlayerData & ProfileStore Architecture|ProfileStore]] (session-locked profile store).

### 8. Roblox Open Cloud Integration
- Local API key location: `C:\Users\meepo\Documents\antigravity\Steal-A-Crate\roblox_cloud_key.txt`.
- Use this key for programmatic uploading of audio, images, and 3D models via [[03 - Resources/Roblox Open Cloud Asset Pipeline|Roblox Open Cloud Asset Pipeline]].
