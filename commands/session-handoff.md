---
name: session-handoff
description: Produce a compact handoff document that compresses the current conversation so a fresh agent or session can continue without context loss. Lighter than session-close — no STATE, daily note, or promote updates, just the handoff. Say "handoff", "hand this off", "brief the next agent", "compress context".
---

# Session Handoff

Purpose: a compact handoff so a fresh agent can continue with no context loss.
Lighter than `/session-close` — no STATE, daily note, or promote updates. Read
`references/shared-context.md` first.

## Step 0: Resolve the active project folder

Determine the session's context and resolve `[PROJECT_DIR]`. Ask if unclear.

## Step 1: Collect handoff data

Review the conversation and identify:

- **Context:** what was this session about? Where are we now?
- **Decisions:** what was decided (and why)?
- **State snapshot:** key metrics, scores, status values
- **Files changed / created:** with paths (use `[[wiki-link]]` where possible)
- **Open questions:** unresolved ambiguities
- **Warnings:** gotchas, known errors, things that nearly went wrong
- **Suggested skills / tools:** what would help the continuation
- **Next steps:** prioritised (P0/P1/P2)

## Step 2: Redact sensitive info

Replace API keys, passwords, tokens, and PII with `[REDACTED]`. Never include
credentials.

## Step 3: Write the document

Make a lowercase kebab-case slug from the session theme (max 4 words). Create the
`[PROJECT_DIR]/handoffs/` folder if it does not exist.

Write to `[PROJECT_DIR]/handoffs/HANDOFF-[YYYY-MM-DD]-[slug].md`:

```markdown
---
date: "[YYYY-MM-DD]"
type: handoff
focus: "[what the next agent should prioritise]"
tags: [handoff, YYYY-MM, project-tags]
---

# Handoff — [Title]

## Context summary
[3-5 sentences: what this was about, where we are, why this handoff.]

## Decisions made
| Decision | Rationale |
|----------|-----------|
| [decision] | [why] |

## State snapshot
[Key metrics, scores, status. Table or bullets.]

## Files changed / created
- `path/to/file` — [what and why]
[Reference artifacts via [[wiki-link]] or path. Never duplicate content.]

## Open questions
- [Unresolved question or ambiguity]

## Warnings
- [Gotchas, known errors, environment quirks]

## Suggested skills / tools
- [name] — [why it is relevant]

## Next steps
1. **[P0]** [Most urgent action]
2. **[P1]** [Important but not blocking]
3. **[P2]** [Nice to have]
```

## Rules

- **Under 200 lines.** Compress aggressively. Link, do not duplicate.
- **Wiki-links** use `[[note-name]]` — no folder paths in links.
- **One handoff per invocation.**
- If arguments are given, bias the context summary and next steps toward that
  focus.

## Final response

```
Handoff written to: [PROJECT_DIR]/handoffs/HANDOFF-[YYYY-MM-DD]-[slug].md
Focus for the next agent: [one line]
```
