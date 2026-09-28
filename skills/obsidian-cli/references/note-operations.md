# Note operations

Target notes with exact vault-relative paths (`path="Folder/Note.md"`). Prefer `path=` over `file=` (fuzzy wikilink) to ensure deterministic targeting.

> [!IMPORTANT]
>
> - **Plain read & write**: Prefer native filesystem tools for reading or writing known-path notes and batch Frontmatter updates. Do NOT use `obsidian create` to pass complex or multiline markdown through shell parameters.
> - **When to use CLI**:
>   - Dynamic lifecycle notes: `obsidian daily` (opens/creates with templates auto-rendered), `obsidian daily:path` (resolves path without guessing directories), `obsidian daily:append/prepend`
>   - Read active note without knowing path: `obsidian read` (no path)
>   - Rename or move: `obsidian rename`, `obsidian move` (crucial: auto-updates backlinks across the vault)
>   - Parse structure/stats: `obsidian outline`, `obsidian wordcount`
>   - Templates & UI opening: `obsidian create template=...`, `open` or `newtab`
>   - File history & diff: `obsidian history`, `obsidian diff`, `obsidian history:restore` (version rollback)

## Read, open, and inspect

For notes with a known path, use filesystem tools directly. Use the CLI for the active file, opening in UI, app-parsed metadata, or listing files/folders:

```sh
obsidian read                                      # read currently active file in app
obsidian open path="Folder/Note.md" newtab         # open in new tab (avoids replacing active tab)
obsidian outline path="Folder/Note.md" format=json # heading structure (format=tree|md|json, total)
obsidian wordcount path="Folder/Note.md" words     # word count (words, characters)
obsidian file path="Folder/Note.md"                # file info and timestamps
obsidian files folder="Projects/" ext=md           # list files (supports ext=md, total)
obsidian folders folder="Projects/"                # list folders (supports total)
```

`open` **replaces the active tab** by default; always include `newtab` to protect the user's current workspace. `read`, `outline`, and `wordcount` default to the active file. `folder path=... info=files|folders|size` returns specific folder statistics.

## Create and edit

Always create new notes directly using filesystem tools. Use the CLI only when instantiating Obsidian templates or targeting frontmatter:

```sh
obsidian create template="Travel" name="Trip" open # instantiate template
obsidian prepend path="Ideas.md" content="## New"  # inserts after frontmatter
obsidian append path="Journal.md" content="- Item"
```

`create` requires `overwrite` to replace existing files (**confirm before overwriting**). Add `open` or `newtab` to view it in the app. `prepend` inserts after frontmatter; `inline` on append/prepend omits trailing newlines. Neither needs a `silent` flag.

## Rename, move, delete

Prefer CLI commands here over filesystem operations so Obsidian can automatically update internal links across the vault:

```sh
obsidian rename path="Drafts/Note.md" name="New Name"
obsidian move path="Drafts/Note.md" to="Published/Note.md"
obsidian delete path="Scratch.md"                  # system trash by default
```

`rename` preserves the extension if omitted; `move to=` accepts a folder or full destination path. Link updates depend on the vault's automatic-update setting. Check the target before deleting; `delete permanent` bypasses trash and requires explicit intent.

## Daily notes

Commands for the core Daily notes plugin. Automatically resolves the configured date format and folder.

```sh
obsidian daily:path                                # get today's note path (even before creation)
obsidian daily:read                                # read today's daily note content
obsidian daily:append content="- [ ] Log item"     # append entry (creates note if absent; silent by default)
obsidian daily:prepend content="## Morning goals"  # prepend entry
obsidian daily                                     # open today's daily note in app UI
```

`daily` opens today's note; `daily:append` and `daily:prepend` automatically create today's note if it does not exist yet, and write silently without opening unless `open` is specified. They support `inline` (omit newline) and `paneType=tab|split|window`. No `silent` flag is needed. `daily` automatically triggers configured templates (e.g., Templater); never crawl directories to locate or create daily notes manually.

## Templates

Commands for core Templates.

```sh
obsidian templates                                 # list all available templates
obsidian template:read name="Daily" resolve        # read template with {{date}}/{{time}} resolved
obsidian template:insert name="Meeting Notes"      # insert template into the active file
```

`resolve` automatically replaces `{{date}}`, `{{time}}`, and `{{title}}`. `template:insert` inserts into the **active file** only. To create a new note directly from a template, use `obsidian create template="Name" name="New Note"`.

## Local file history (File recovery)

Free local version snapshots from the core File recovery plugin. Versions are numbered **newest to oldest**. Inspect and compare before restoring.

```sh
obsidian history path="Projects/Plan.md"
obsidian diff path="Projects/Plan.md" from=2 to=1
obsidian history:read path="Projects/Plan.md" version=2
```

Use `history:list` to find all files with local snapshots. `history:restore` recovers a version (requires explicit user intent). `history:open` opens the File recovery view in the app.

## Plugin-dependent and random notes

```sh
obsidian random:read folder="Zettelkasten/"        # read without changing workspace
obsidian random                                    # open random note in app UI
```

`unique` requires the Unique note creator plugin (`name=`, `content=`, `paneType=`, `open`). `random:read` defaults to whole vault if `folder=` is omitted.
