# Shared Context — Session Lifecycle

Every command in this plugin reads this file first. It defines *where* session
files live, *how* they are formatted, and the two hard rules that keep the loop
reliable. Keep it open while a command runs.

---

## 1. Where session files live (context-aware placement)

Session files are written to **the active project's folder** — not to one fixed
dump folder. A client-work session and a research session should not pile their
notes in the same place.

The mapping from *session context* to *project folder* is defined by you in a
config note that `/session-setup` creates:

```
<vault>/_session-lifecycle/config.md
```

That file holds a simple table, for example:

| When the session is about... | Write session files to... |
|------------------------------|---------------------------|
| Client work                  | `Areas/Client-Work/`      |
| Research                     | `Areas/Research/`         |
| This vault / product build   | `Projects/Product/`       |
| Anything else / unclear      | ask me                    |

### Step 0 of every start/close/handoff

Determine the session's primary context and resolve `[PROJECT_DIR]` from the
config table. If it is genuinely unclear, ask the user — do not guess.

### File paths (relative to vault root)

Project-scoped files (inside `[PROJECT_DIR]`):

- Session reflection: `[PROJECT_DIR]/[YYYY-MM-DD]-session-reflection.md`
- Session log: `[PROJECT_DIR]/SESSION-LOG-[YYYYMMDD].md`
- State: `[PROJECT_DIR]/STATE.md`
- Next-session starter: `[PROJECT_DIR]/NEXT-SESSION-STARTER.md`
- Handoffs: `[PROJECT_DIR]/handoffs/HANDOFF-[YYYY-MM-DD]-[slug].md`

Fixed path (always the same place):

- Daily notes: `<vault>/Daily/[YYYY-MM-DD].md`

> Folder names (`Areas/`, `Projects/`, `Daily/`) are conventions, not hard
> requirements. Whatever you choose in `config.md` is authoritative — the
> commands only ever read paths from there.

---

## 2. Two hard rules (this is where the loop usually breaks)

### Rule A — Run every step, even if a file was touched earlier

A file having been written *earlier in the session* is **not** a valid reason to
skip its step at close. Every close step executes again in the close pass, with
fresh content that reflects the whole session. If STATE or NEXT-SESSION-STARTER
was touched earlier, read it and overwrite it with the full, current version now.
Never write "already done" as a reason to omit a step.

### Rule B — A missing folder is not a skip reason either

If `[PROJECT_DIR]`, the daily folder, or a target file does not exist, **create
it and write the file.** Degrade by creating what is missing — never by dropping
the step.

The self-test checklist starts with every box empty. A box may only be ticked
`[x]` once you have actually produced that artifact *in this pass*.

---

## 3. Frontmatter (required)

Every markdown file written to the vault must start with YAML frontmatter, or
Obsidian queries and Dataview cannot see it.

```yaml
---
date: "YYYY-MM-DD"
type: [session-note | session-log | session-briefing | state | session-starter | daily-note | handoff]
tags: [relevant, tags]
---
```

Each command below specifies the exact fields for the file it writes.

---

## 4. Wiki-links

Use flat links: `[[note-name]]` — not `[[folder/path/note-name]]`. Obsidian
resolves flat links automatically; paths make links brittle when notes move.

---

## 5. Reading and writing files

Use your standard file tools to read and write inside the vault. If a write
tool cannot reach a path, fall back to whatever file access your environment
provides. Do not fabricate success — confirm each file was written before you
tick its checklist box.
