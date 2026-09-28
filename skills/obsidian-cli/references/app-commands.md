# App commands

Obsidian's Command Palette includes all actions registered by both core features and installed community plugins.

## Discover and execute commands

```sh
obsidian commands filter="markdown"            # filter command IDs by keyword or plugin prefix
obsidian command id="editor:toggle-source"     # execute a command by its ID
obsidian command id="app:toggle-left-sidebar"  # toggle UI elements
```

Always use `filter=<prefix>` with `commands` to discover valid IDs; running bare `obsidian commands` can return thousands of IDs and blow out the context window. `command id=...` immediately executes the specified command in the running app.

> [!IMPORTANT]
> The command execution syntax is strictly `obsidian command id="..."`. There is NO `command:execute` subcommand.
