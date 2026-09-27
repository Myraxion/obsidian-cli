---
name: obsidian-cli
description: Use Obsidian's official desktop CLI for live full-text search, link-safe note rename/move, metadata, daily notes, tasks, templates, Bases, commands, history, and workspace management. Prefer filesystem tools for plain file operations that do not need the running app.
---

# Obsidian CLI

Use the CLI for Obsidian's live indexes, settings, plugins, and workspace; use filesystem tools for plain file operations. This CLI controls the desktop app, not Obsidian Headless.

## Protect data and the agent session

Never reload or restart the Obsidian app/window from an agent session. Never reload, disable, or uninstall the plugin hosting the agent, even through `command`: doing so can terminate the session.

Require explicit user intent for permanent deletion, history/Sync restoration, publishing or unpublishing, plugin/theme installation or removal, and restricted-mode changes. Prefer reversible actions; inspect targets before bulk mutations. Reference examples do not authorize changes.

## Read only the relevant guide

Load only the reference(s) directly needed for the task; do not load unrelated guides.

| Task | Reference |
|------|-----------|
| Read, open, write, files/folders, daily notes, templates, history, diff, rename, delete | [Note operations](references/note-operations.md) |
| Search, tags, properties, tasks aggregation, backlinks, bookmarks, recents, Bases | [Search, metadata, tasks, and Bases](references/search-metadata.md) |
| Discover and execute core and community plugin commands | [Commands](references/commands.md) |
| Workspace layout, tabs, plugins, themes, vault info, multi-vault targeting, Sync | [Vault, workspace, and environment](references/vault-management.md) |
