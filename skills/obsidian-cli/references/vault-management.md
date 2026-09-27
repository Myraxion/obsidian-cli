# Vault, workspace, and environment

For low-frequency operations, use `obsidian help <command>` or the [official command reference](https://obsidian.md/help/cli) instead of guessing parameters.

## Workspace and tabs

Inspect and control open tabs and split pane layouts.

```sh
obsidian tabs ids                    # open tabs in active window
obsidian workspace ids               # live split/pane layout tree
obsidian workspaces                  # list saved workspace layouts
obsidian workspace:load name="Study" # switch workspace layout
```

`workspace:save`, `workspace:load`, `workspace:delete`, and `tab:open` change window layouts (Workspaces plugin). Inspect live help before use.

## Plugins, themes, snippets

```sh
obsidian plugins:enabled filter=community
obsidian plugin id=my-plugin         # plugin info
obsidian theme                       # active theme
obsidian snippets:enabled
```

`plugin:enable`, `plugin:disable`, `plugin:install`, `plugin:uninstall`, `plugin:reload`, `plugins:restrict`, `theme:set`, `theme:install`, `theme:uninstall`, `snippet:enable`, and `snippet:disable` change app settings. Inspect IDs/names and live help first; installation/removal and restricted-mode changes require explicit user intent.

## Vault info and multi-vault targeting

If the terminal is inside a vault directory, the CLI uses it by default; otherwise it falls back to the active vault. Inspect vault stats or target another vault explicitly:

```sh
obsidian vault info=size                 # vault info (name, path, files, folders, size)
obsidian vault="My Vault" <command>      # prefix to target a specific vault
obsidian vaults verbose                  # list all known vaults and paths
```

`vault:open` switches vaults **only in the TUI**.

## Sync and Publish (Paid services)

Requires active **Obsidian Sync** or **Publish** subscriptions (desktop Sync is not Obsidian Headless). Mutating operations (`restore`, `add`, `remove`, `sync on|off`) alter remote/published state and require explicit user intent. Inspect available commands and parameters dynamically using `obsidian help sync` or `obsidian help publish`.
