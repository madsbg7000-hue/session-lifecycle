---
name: session-start
description: Start a session with a briefing built from persisted state. Reads STATE and NEXT-SESSION-STARTER from the active project folder plus recent daily notes, and proposes a focus for today. Run at the beginning of a session or say "start session", "what are we doing today", "brief me".
---

# Session Start

Purpose: get up to speed and aligned with the user's priorities before any work
begins. Read `references/shared-context.md` first.

## Step 0: Resolve the active project folder

Determine the session's context and resolve `[PROJECT_DIR]` from
`_session-lifecycle/config.md`. Ask if unclear. If setup was never run, suggest
`/session-setup`.

## Steps

1. **Vault check** — confirm the vault and `[PROJECT_DIR]` exist.
2. **Read STATE** from `[PROJECT_DIR]/STATE.md`.
3. **Read NEXT-SESSION-STARTER** from `[PROJECT_DIR]/NEXT-SESSION-STARTER.md`.
4. **Skim recent daily notes** in `<vault>/Daily/` (last 1-3 days) for loose
   threads.
5. **Present the briefing** in this format:

```markdown
---
date: "[YYYY-MM-DD]"
type: session-briefing
tags: [briefing, YYYY-MM]
---

## Session Briefing — [date]

**Last session:** [date] — [one-line summary]
**Project folder:** [PROJECT_DIR]

### Priorities from STATE
1. [P1]
2. [P2]
3. [P3]

### Suggested focus today
1. [Activity 1] (~[X] min)
2. [Activity 2] (~[X] min)

**Estimated session length:** ~[total]

Shall we run with this, or do you have something else in mind?
```

Use `[[note-name]]` wiki-links when you reference notes in the briefing.
If STATE or NEXT-SESSION-STARTER is missing, say so plainly and offer to create
them (via `/session-setup`) rather than inventing their contents.
