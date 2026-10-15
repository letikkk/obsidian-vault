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
