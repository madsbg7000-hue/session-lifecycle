---
type: session-lifecycle-config
updated: "[YYYY-MM-DD]"
tags: [session-lifecycle, config]
---

# Session Lifecycle — Config

This note is the single source of truth for where session files are written.
`/session-start`, `/session-close`, and `/session-handoff` read the table below
to resolve `[PROJECT_DIR]`. Edit it freely — add rows as you add projects.

## Context -> folder mapping

| When the session is about... | Write session files to... |
|------------------------------|---------------------------|
| [Project A, e.g. Client work]| `Projects/Client-Work/`   |
| [Project B, e.g. Research]   | `Projects/Research/`      |
| [This vault / product]       | `Projects/Product/`       |
| Anything else / unclear      | ask me                    |

## Fixed paths

- Daily notes: `Daily/`
