# Session Lifecycle

**Cross-session memory for your AI assistant, backed by an Obsidian vault.**

AI coding and writing assistants forget everything between sessions. You spend
the first ten minutes of every session re-explaining where you left off, and the
last ten minutes watching context evaporate. This plugin fixes that with a small,
disciplined loop: at the end of a session the assistant writes down what happened
and what comes next; at the start of the next one it reads that back and briefs
you. The memory lives in your own vault as plain markdown; it is yours to
read, edit, and keep.

Five slash commands:

| Command | What it does |
|---------|--------------|
| `/session-setup`   | Scaffolds the folder skeleton and config the plugin needs. Run once. |
| `/session-start`   | Briefs you from saved STATE, the next-session starter, and recent daily notes. |
| `/session-track`   | Logs progress mid-session into a buffer, so nothing is lost. |
| `/session-close`   | Writes reflection, log, STATE, next-session starter, and daily note in one pass. |
| `/session-handoff` | Produces a compact handoff so a fresh agent can pick up your context. |

---

## Quick start

1. **Install** (as a plugin marketplace):

   ```
   /plugin marketplace add USERNAME/session-lifecycle
   /plugin install session-lifecycle
   ```

2. **Scaffold your vault** — run `/session-setup`. It asks for your vault path
   and the projects you work on, then builds the folders, a config note, and
   starter templates. It never overwrites anything that already exists.

3. **Work.** At the end, run `/session-close`. Next time, open with
   `/session-start`.

That's the whole loop.

---

## How it works

```
  /session-setup                    (once — build the skeleton)
        |
        v
  /session-start  --->  work  --->  /session-track (optional, mid-session)
        ^                                   |
        |                                   v
        +------------------------  /session-close
                                   (writes STATE + next-starter + log + daily note)
```

Each close writes to **the active project's folder**, not one shared dump. A
config note (`_session-lifecycle/config.md`, created at setup) maps *session
context* to *folder*: job-search notes go one place, research notes another. You
own that mapping and can edit it any time.

### What a close writes

- **Session reflection** — goal, what got done, results, learnings, next steps.
- **Session log** — a factual record with files changed and fixes made.
- **STATE.md** — the single note the next session reads first: status, priorities,
  next actions.
- **NEXT-SESSION-STARTER.md** — the concrete plan for next time.
- **Daily note** — a dated entry appended to your daily journal.

Everything carries Obsidian-friendly YAML frontmatter and flat `[[wiki-links]]`,
so it shows up in Dataview and graph view immediately.

---

## The two rules that make it reliable

Most session-close routines fail the same two ways. This plugin names both and
forbids them:

1. **"I already wrote STATE earlier, so I'll skip it."** A file touched earlier in
   the session is *not* a reason to skip its close step. Every step re-runs with
   fresh content that reflects the whole session.
2. **"That folder doesn't exist, so I'll skip it."** A missing folder is created,
   not skipped. The loop degrades by building what's missing, never by dropping a
   step.

The self-test checklist starts empty and a box is ticked only when the artifact
is actually produced in that pass.

---

## Customization

Everything is plain markdown you can edit:

- **Folder layout** — change the mapping in `_session-lifecycle/config.md`.
- **Note shape** — edit the templates in `templates/`.
- **Wording and steps** — the commands live in `commands/` as readable markdown.

Not an Obsidian user? The model is just dated markdown notes in folders, so it
adapts to any plain-markdown vault; you lose only the Dataview/graph niceties.

---

## Built with autoresearch

The command instructions were hardened with an autoresearch loop, an
eval-driven optimization method inspired by Andrej Karpathy's Auto Research
pattern. Each iteration froze the eval matrix and testcases, changed exactly one
thing, and was scored by a separate adversarial grader that never saw the change
intent. The idempotency rule above was not a guess; it was the top real-world
failure the evals surfaced. The frozen matrix and testcases ship in `evals/` so
you can re-run or extend the loop yourself.

---

## License

MIT. See [LICENSE](LICENSE).
