<div align="center">

# obsidian-cli

Agent skill for the [official Obsidian desktop CLI](https://obsidian.md/help/cli).

[![Skills](https://img.shields.io/badge/skills.sh-Myraxion%2Fobsidian--cli-purple?style=flat-square)](https://skills.sh/)
[![Obsidian](https://img.shields.io/badge/Obsidian-1.12.7%2B-705dcf?style=flat-square&logo=obsidian&logoColor=white)](https://obsidian.md/)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](LICENSE)

[English](README.md) | [简体中文](README_zh.md)

</div>

---

Connects AI coding agents (Claude Code, Antigravity, OpenHands, etc.) with the official Obsidian desktop CLI. Enables full-text search, link-safe note refactoring, metadata updates, daily notes, tasks, Bases databases, workspace management, and local file history.

## Features

- **User focus**: Strictly targeted at everyday knowledge management, graph navigation, and task workflows. Developer-only commands (`eval`, DOM inspection, debugger controls) found in other alternatives are omitted to prevent context bloat and execution hallucinations.
- **Pragmatic tool division**: Avoids forcing multiline text creation through CLI parameters—a common pitfall in other alternatives that leads to shell escaping and truncation issues. Standard filesystem tools handle note content, while the CLI handles what only Obsidian can do (link-safe renames/moves, active tabs, and live index queries).
- **Minimal context overhead**: Features a lightweight ~1.7 KB entry point with modular domain guides loaded only on demand, in contrast to other alternatives that inject 20–30+ KB monolithic manuals into the prompt.
- **Agent session guardrails**: Protects against self-terminating operations (such as app reloads or disabling the host plugin), ensuring stability when the agent operates from within Obsidian plugins.
- **Accurate modern syntax (v1.12.7+)**: Aligns directly with official desktop CLI releases, eliminating obsolete workarounds and redundant flags from early preview builds.
- **KISS design**: Avoids complex startup probe scripts or repetitive verification checks, reducing token cost and environmental friction.

## Prerequisites

1. **Obsidian 1.12.7 or newer**: Download and install the desktop app from [obsidian.md/download](https://obsidian.md/download) (updating within the app may not update the installer version).
2. **Enable the CLI**: In Obsidian, turn on **Settings → General → Command line interface** and approve the registration prompt.
3. **Verify connectivity**: Ensure Obsidian is running, then verify in a terminal:

   ```sh
   obsidian version
   obsidian vault info=path
   ```

## Installation

### Using the skills CLI (recommended)

```sh
npx skills add Myraxion/obsidian-cli
```

### Manual installation

Copy `SKILL.md` and the `references/` directory into your agent's skill directory:

- Project: `.agents/skills/obsidian-cli/` (or `.claude/skills/obsidian-cli/`)
- Global: `~/.agents/skills/obsidian-cli/` (or `~/.claude/skills/obsidian-cli/`)

## Documentation structure

The skill uses on-demand references to keep base context consumption minimal:

| File | Scope |
|------|-------|
| [`SKILL.md`](SKILL.md) | Safety guardrails and routing logic |
| [`references/note-operations.md`](references/note-operations.md) | Reading, creating, link-safe renaming/moving, daily notes, and file history |
| [`references/search-metadata.md`](references/search-metadata.md) | Live search, Bases, frontmatter properties, tags, backlinks, and tasks |
| [`references/commands.md`](references/commands.md) | Command palette discovery and execution |
| [`references/vault-management.md`](references/vault-management.md) | Workspaces, tabs, plugins, themes, multi-vault targeting, and Sync |

## Troubleshooting

For general issues, refer to the [official CLI troubleshooting guide](https://obsidian.md/help/cli#Troubleshooting).

- **Windows**: If executing `obsidian` launches the GUI window or produces no terminal output, use `Obsidian.com` (the registered console redirector) instead of `Obsidian.exe`.
- **macOS**: Registration links `/usr/local/bin/obsidian` to the binary. Ensure `/usr/local/bin` is in your `PATH`.
- **Linux**: The binary is placed at `~/.local/bin/obsidian`. Ensure `~/.local/bin` is in your `PATH`.
- **After app updates**: If the CLI unlinks after an Obsidian update, toggle the CLI option off and back on in **Settings → General**, then restart the terminal.

## License

This project is licensed under the [MIT License](LICENSE).
