---
name: session-close
description: Close a session by updating every continuity system in one structured pass — reflection, log, STATE, next-session starter, daily note, and promote-flow. Runs all steps every time, even for files touched earlier in the session. Say "close session", "wrap up", "session close", "end the session", "shut it down".
---

# Session Close

Purpose: a structured close that leaves the next session with everything it needs.
Run **all** steps, in order. No shortcuts. Read `references/shared-context.md`
first.

**Rule A — Idempotency (critical):** a file having been written *earlier in the
session* is NOT a valid reason to skip its step. Every step below executes again
in this close pass with fresh content reflecting the whole session. If STATE or
NEXT-SESSION-STARTER was touched earlier, read it and overwrite it with the full,
current version now. Never write "already done" to omit a step.

**Rule B — Missing folders are not a skip reason.** If `[PROJECT_DIR]`, the daily
folder, or a target file does not exist, create it and write the file. Degrade by
creating what is missing, not by dropping the step.

## Step 0: Resolve the active project folder

Determine the session's context and resolve `[PROJECT_DIR]` from
`_session-lifecycle/config.md`. Ask if unclear.

## Self-test checklist

Every box starts empty. Tick `[x]` only once you have actually produced that
artifact **in this pass** — not because the file was touched earlier. If an
artifact was not produced in the close pass, the box stays `[ ]` and you do the
step before finishing.

- [ ] Step 2: Session reflection written in [PROJECT_DIR] (fresh this pass)
- [ ] Step 3: Session log written in [PROJECT_DIR] (fresh this pass)
- [ ] Step 4: STATE overwritten in [PROJECT_DIR] (fresh this pass)
- [ ] Step 5: NEXT-SESSION-STARTER overwritten in [PROJECT_DIR] (fresh this pass)
- [ ] Step 6: Daily note updated (fresh this pass)
- [ ] Step 7: Promote-flow checked (fresh this pass)

---

## Step 1: Gather session data

Review the conversation and identify: goal (what was the plan?), done (what
actually happened?), results (metrics, outputs), decisions (and rationale),
learnings (what worked, what failed?), next steps, promotable outputs.

## Step 2: Write the session reflection

Write to `[PROJECT_DIR]/[YYYY-MM-DD]-session-reflection.md`:

```markdown
---
date: "[YYYY-MM-DD]"
type: session-note
session_type: [research | build | content | cleanup | planning | mixed]
duration_estimate: "[estimate]"
tags: [session, YYYY-MM, project-tags]
---

# Session [YYYY-MM-DD]

## Goal
[What was the plan?]

## Done
[Bullet points — factual]

## Results
| Output | Before | After | Status |
|--------|--------|-------|--------|

## Learnings
[What worked? What failed?]

## Next session should
[Prioritised list]
```

Include at least 5 wiki-links to notes touched, related sessions, references.

## Step 3: Write the session log

Write to `[PROJECT_DIR]/SESSION-LOG-[YYYYMMDD].md`:

```markdown
---
date: "[YYYY-MM-DD]"
type: session-log
tags: [session-log, YYYY-MM]
---

# Session Log — [YYYY-MM-DD]

## Done
[Numbered list with detail]

## Fixes along the way
[Problems and solutions]

## Files changed / created
[List with wiki-links]
```

## Step 4: Update STATE

Overwrite `[PROJECT_DIR]/STATE.md`. It must carry frontmatter:

```yaml
---
type: state
updated: "[YYYY-MM-DD]"
tags: [state, project-tags]
---
```

Update these sections: status table (done vs. remaining), last session (date +
one line), current priorities, next-session action items. STATE is the first
thing every session reads — be precise.

## Step 5: Write NEXT-SESSION-STARTER

Overwrite `[PROJECT_DIR]/NEXT-SESSION-STARTER.md`:

```markdown
---
date: "[expected next date]"
type: session-starter
focus: "[main focus]"
estimated_duration: "[estimate]"
tags: [session-starter, YYYY-MM]
---

# Next Session — [Title]

## Context
[2-3 sentences: last time + why this is next]

## Goals
[1-3 concrete goals]

## Strategy
[Numbered steps]

## Success criteria
- [ ] [Measurable criterion 1]
- [ ] [Measurable criterion 2]
```

## Step 6: Update the daily note

Create `<vault>/Daily/[YYYY-MM-DD].md` if it does not exist, with frontmatter:

```yaml
---
type: daily-note
date: "[YYYY-MM-DD]"
tags: [daily, YYYY-MM]
---
```

Append under `## What happened today` — do not overwrite existing content:

```markdown
### [HH:MM] — [Session theme, max 10 words]
- **Context:** [1-2 lines]
- **Key output:** [2-4 bullets]
- **Follow-up:** [next step]
- **Filed to:** [[relevant notes]]
```

## Step 7: Promote-flow

Check whether any finished outputs belong elsewhere in the vault (a reference
folder, a published-notes area). Move or link them. If nothing is promotable, say
so — do not skip the check.

---

## Final response

Show the completed checklist plus a one-line next-session focus:

```
## Session close checklist
- [x] Step 2: Session reflection -> [PROJECT_DIR]
- [x] Step 3: Session log -> [PROJECT_DIR]
- [x] Step 4: STATE -> [PROJECT_DIR]
- [x] Step 5: NEXT-SESSION-STARTER -> [PROJECT_DIR]
- [x] Step 6: Daily note
- [x] Step 7: Promote-flow

**Next session:** [one-line focus]
```
