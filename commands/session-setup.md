---
name: session-setup
description: Scaffold the folder skeleton and config this plugin needs, inside an Obsidian vault. Creates the Daily folder, a _session-lifecycle config note with the context to-folder mapping, and one example project folder with STATE + NEXT-SESSION-STARTER templates. Idempotent — never overwrites existing files. Run once when you install the plugin, or say "set up session lifecycle", "scaffold my vault", "session setup".
---

# Session Setup

Purpose: build the minimum skeleton the other four commands rely on, so
`/session-start` and `/session-close` always have somewhere to read from and
write to. Safe to run more than once — it only creates what is missing.

Read `references/shared-context.md` first.

## Step 1: Find the vault root

Ask the user for their Obsidian vault path if you do not already know it. Confirm
it contains a `.obsidian/` folder (that is what makes it a vault). Call it
`<vault>`.

## Step 2: Ask two questions

1. **Daily-notes folder name?** Default `Daily/`. If they already use Obsidian's
   core Daily Notes plugin, match that folder instead.
2. **Which projects do they run sessions for?** Get a short list (e.g. "job
   search, research, this vault"). You will turn these into the context to-folder
   mapping.

Ask both in one turn. Do not scaffold until answered.

## Step 3: Create folders (only if missing)

- `<vault>/<daily-folder>/`
- `<vault>/_session-lifecycle/`
- `<vault>/Projects/` (parent for project folders)
- One folder per project the user named, e.g. `<vault>/Projects/<Name>/` and
  `<vault>/Projects/<Name>/handoffs/`

Never delete or overwrite an existing folder.

## Step 4: Write the config note (only if missing)

Create `<vault>/_session-lifecycle/config.md` from `templates/config.md`,
filling the mapping table with the projects from Step 2. This note is the single
source of truth for `[PROJECT_DIR]` resolution — every other command reads it.

## Step 5: Seed each project folder (only if missing)

For each project folder, create from the templates:

- `STATE.md`            <- `templates/STATE.template.md`
- `NEXT-SESSION-STARTER.md` <- `templates/NEXT-SESSION-STARTER.template.md`

Fill `[PROJECT_NAME]` and today's date. If a file already exists, leave it
untouched and note that in your summary.

## Step 6: Confirm

Show a tree of what was created vs. skipped, and the resolved config mapping:

```
Session Lifecycle is set up.

Created:
  <vault>/Daily/
  <vault>/_session-lifecycle/config.md
  <vault>/Projects/<Name>/STATE.md
  <vault>/Projects/<Name>/NEXT-SESSION-STARTER.md
  <vault>/Projects/<Name>/handoffs/

Skipped (already existed):
  <vault>/Daily/            (found existing daily notes)

Context -> folder mapping:
  Job search  -> Projects/Job-Search/
  Research    -> Projects/Research/

Next: run /session-start to get your first briefing, or just start working and
run /session-close at the end.
```
