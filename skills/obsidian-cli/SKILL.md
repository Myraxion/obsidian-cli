---
name: obsidian-cli
description: Use Obsidian's official desktop CLI for live full-text search, link-safe note rename/move, metadata, daily notes, tasks, templates, Bases, commands, history, and workspace management. Prefer filesystem tools for plain file operations that do not need the running app.
---

# Obsidian CLI

Use the CLI for Obsidian's live indexes, settings, plugins, and workspace; use filesystem tools for plain file operations. This CLI controls the desktop app, not Obsidian Headless.

## Protect data and the agent session

Never reload or restart the Obsidian app/window from an agent session. Never reload, disable, or uninstall the plugin hosting the agent, even through `command`: doing so can terminate the session.

Require explicit user intent for permanent deletion, history/Sync restoration, publishing or unpublishing, plugin/theme installation or removal, and restricted-mode changes. Prefer reversible actions; inspect targets before bulk mutations. Reference examples do not authorize changes.

Assume installed plugins, core settings, and templates work as intended. Unless an explicit error occurs or the user explicitly asks for debugging, DO NOT proactively inspect vault configurations (`.obsidian/`), template scripts, or external APIs. Trust commands to execute their internal logic automatically; verify outcomes via the generated note or exit status.

## Decision Paradigms & Guide Routing

For multi-step workflows, decompose the task and apply the matching paradigm at each step. Before executing CLI commands in any paradigm, view its referenced guide for exact syntax and flags; **use only documented commands, NEVER guess or invoke unlisted CLI subcommands**.

1. **In-place content I/O** (Intent: read known notes, edit body paragraphs, batch-update frontmatter/YAML tags):
   - *Rule*: ALWAYS use native filesystem tools directly to read, edit, or replace content (including entire YAML blocks).
   - *Guide*: **None** (use native workspace tools directly; do not load CLI guides).

2. **Note lifecycle & safe mutation** (Intent: daily/periodic notes, template instantiation, read active note, open in UI/newtab, rename/move, history diff & rollback):
   - *Rule*: ALWAYS use CLI when app runtime context is essential: executing template rendering, triggering daily notes, maintaining wikilink integrity on rename/move, or inspecting version history. Trust commands to handle lifecycle logic internally.
   - *Guide*: [Note operations](references/note-operations.md)

3. **Live search, metadata & Bases** (Intent: full-text search, query backlinks/tags/tasks/properties, Bases database queries):
   - *Rule*: ALWAYS query Obsidian's in-memory live index and graph cache. NEVER perform raw filesystem grep/walk for whole-vault searches or task aggregations.
   - *Guide*: [Search, metadata, tasks, and Bases](references/search-indexes.md)

4. **Host automation & commands** (Intent: run Linter, format note, toggle views, trigger community plugin actions):
   - *Rule*: Dispatch actions through Obsidian's command palette system. Treat execution as a black box; do not inspect internal scripts.
   - *Guide*: [App commands](references/app-commands.md)

5. **Vault, workspace & environment** (Intent: workspace layout save/load, tabs management, plugin/theme toggling, multi-vault targeting, Sync check):
   - *Rule*: Manage workspace tabs, app layout, and vault settings via CLI. NEVER restart the app window or disable the agent's host plugin.
   - *Guide*: [Vault, workspace, and environment](references/workspace-vault.md)
