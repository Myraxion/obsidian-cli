# Search, metadata, tasks, and Bases

Query live in-memory indexes for vault search, backlinks, tags, properties, tasks, and Bases without scanning raw files.

## Search

Perform live full-text search across the vault:

```sh
obsidian search query="API" path="Projects/" limit=10 format=json
obsidian search:context query="TODO" path="Projects/"
obsidian search query="review" total
```

`search` performs full-text search and returns matching **file paths**; `search:context` returns matching lines (`path:line: text`). Both support Obsidian search syntax, `case`, and `format=text|json`; `total` is for `search` only. `search:open query="todo"` opens the UI. There is no `matches` flag on `search`.

## Bases (Structured databases)

Commands for Bases (`.base` files). Requires the Bases core plugin.

```sh
obsidian bases                                        # list all .base files in the vault
obsidian base:views path="Projects.base"              # list views in the specified base
obsidian base:query path="Projects.base" format=json  # query base records (default: json)
obsidian base:create path="Projects.base" name="Task" # add a new item to base
```

`base:views` defaults to the active base if no path is given. `base:query` supports `view=<name>` and `format=json|csv|tsv|md|paths`. `base:create` accepts `view=<name>`, `name=<name>`, `content=<text>`, and `open`/`newtab`. Unattended `base:create` should specify both `path=` and `view=`.

## Links and graph health

```sh
obsidian backlinks path="Projects/Plan.md" counts format=json
obsidian links path="Projects/Plan.md" total
obsidian orphans total              # no incoming links
obsidian deadends total             # no outgoing links
obsidian unresolved verbose        # broken links and their sources
```

`backlinks` and `unresolved` accept `counts`, `total`, and `format=json|tsv|csv` as documented; `orphans` and `deadends` accept `total`, not `all`. See live help for other flags.

## Tags, aliases, properties

```sh
obsidian tags counts sort=count
obsidian tags path="Projects/Plan.md"           # or `active`
obsidian tag name="project" verbose
obsidian aliases path="Projects/Plan.md"        # omit path for vault-wide
obsidian properties path="Projects/Plan.md"     # omit path for vault-wide
obsidian property:read name="status" path="Projects/Plan.md"
obsidian property:set name="priority" value="1" type=number path="Projects/Plan.md"
```

Without `path=` or `active`, `tags`, `aliases`, and `properties` return vault-wide results (no `all` flag needed). Use `counts`, `total`, and `format=` only on commands that document them. Property types: `text`, `list`, `number`, `checkbox`, `date`, `datetime`; use `property:remove name=... path=...` to remove a property. Inspect frontmatter before changing it.

## Tasks

`tasks` aggregates tasks across the **whole vault** (no `all` flag needed); filter with `path=`, `file=`, `daily`, `active`, `todo`, `done`, or `status="<char>"`.

```sh
obsidian tasks todo verbose                        # list incomplete tasks with paths and lines
obsidian tasks daily total                         # count tasks in today's daily note
obsidian task ref="Projects/Plan.md:8" toggle      # toggle task completion
obsidian task file="Plan" line=8 done              # mark specific task line as done
```

`task` inspects or updates status using `ref="path:line"` or `path=... line=...`; use `done`, `todo`, or `status="<char>"` for custom status marks. Confirm the target before modifying, and refresh line numbers after editing notes.

## Bookmarks and recent files

Commands for the core Bookmarks plugin and app navigation history:

```sh
obsidian bookmarks                   # list saved bookmarks
obsidian bookmarks verbose format=json
obsidian bookmark file="Projects/Plan.md" # bookmark a file (supports subpath=, folder=, search=, url=, title=)
obsidian recents                     # recently opened notes in active vault
```

`bookmarks` accepts `total`, `verbose`, and `format=json|tsv|csv`. `bookmark` can bookmark a file, folder, search query, or URL.
