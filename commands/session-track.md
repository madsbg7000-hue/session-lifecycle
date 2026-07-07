---
name: session-track
description: Capture progress mid-session so nothing is lost at close. Quick-logs what was done, the result, and any decisions into a running buffer that /session-close later structures into the log and reflection. Say "note this", "log progress", "track that", "what have we done", or run when a sub-task finishes.
---

# Session Track

Purpose: capture progress as it happens so `/session-close` has clean material to
work from.

## When to run

When the user says "note this" / "log progress", or when a sub-task finishes.

## What to capture

For each tracked item:

- **What** was done (factual, brief)
- **Result** (output, metric, file created)
- **Decisions** made along the way (and why)
- **Problems** hit (and any fix)

## Response format

Keep it short. Confirm with:

```
Tracked: [one-line description].
[N] items tracked this session.
```

## Important

Do not write files yet — tracked items live in the session buffer and are
structured into the session log and reflection when `/session-close` runs. If the
user asks for the running list, show it compactly:

```
## Tracked this session ([N] items)
1. [HH:MM] — [description]
2. [HH:MM] — [description]
```
