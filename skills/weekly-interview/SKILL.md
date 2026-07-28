---
name: weekly-interview
description: Run a structured weekly interview with the user to surface and persist durable memory — role changes, feedback received, project decisions, references discovered, anything stale to forget. Writes new memory files using the templates in memory/templates/ and updates the MEMORY.md index. Trigger when the user asks for a weekly review, memory refresh, or runs /weekly-interview.
---

# Weekly Interview

Run a structured interview to update long-term memory. Memory lives in the auto-memory directory (for Claude Code: `~/.claude/projects/<project-slug>/memory/`). Templates live in this repo's `memory/templates/` — copy them into the memory directory on first use.

Memory types: `user`, `feedback`, `project`, `reference`. The index is `MEMORY.md` — one line per file, under ~150 chars.

## Steps

1. **Read current state.** Read `MEMORY.md` and every file it points to. Note which types already exist and what looks stale (project/feedback files older than ~30 days with no recent edits, or content describing closed/abandoned work).

2. **Run the interview.** Ask these questions one at a time. Wait for each answer before asking the next. Skip any the user says "skip" to.

   1. **Role & responsibilities:** Has anything about your role, team, or what you own changed this week?
   2. **Projects & decisions:** Did you start, close, or pivot any projects this week? Any decisions made that future-you needs to remember?
   3. **Feedback received:** Did anyone correct your approach, validate a non-obvious choice, or give you guidance you'd want applied next time?
   4. **References discovered:** Any new external systems, dashboards, docs, or channels future-you should know about?
   5. **Things to forget:** Anything in memory that's now stale, wrong, or no longer relevant?
   6. **Surprises:** Anything that surprised you this week that isn't captured above?

3. **Write memory.** For each answer with new information:
   - Pick the right type: `user` (role/prefs), `feedback` (guidance to apply), `project` (decisions/initiatives), `reference` (external systems).
   - Read the matching template from `memory/templates/`.
   - Write a new file or update an existing one — prefer updating over creating duplicates.
   - For `feedback` and `project` types, fill in **Why:** and **How to apply:** lines. Memory without the *why* rots fast.
   - Convert relative dates ("Thursday", "last week") to absolute (2026-07-24).
   - File naming: `<topic-slug>.md` (e.g., `feedback-testing.md`, `reference-grafana.md`). Group by topic, not by date.

4. **Update the index.** Add or update one-line entries in `MEMORY.md`:
   ```
   - [Title](file.md) — one-line hook
   ```
   Keep entries under ~150 chars. The index is loaded into context every session, so keep it lean.

5. **Forget.** For items the user flagged in step 5: confirm each deletion explicitly, then delete the memory file and remove its line from `MEMORY.md`. Never delete without confirmation.

6. **Summary.** Print a one-paragraph summary: files added, files updated, files deleted, and any surprises worth a follow-up next week.

## What not to save

- Code patterns, conventions, architecture, file paths — derivable from the codebase.
- Git history, recent changes, who-changed-what — `git log` and `git blame` are authoritative.
- Debugging solutions or fix recipes — the fix is in the code, the context is in the commit message.
- Ephemeral task state — use tasks, not memory.

If an answer is "nothing this week," don't force a memory. Blank weeks are fine.

## Scheduling

To run this weekly automatically, schedule it with a durable cron (Mondays ~9am local):
```
0 9 * * 1
```
Pin the minute off the :00/:30 marks when scheduling for yourself to avoid thundering-herd load on the API.

## Pair with

- `loop-memory-bridge` — harvests durable lessons from closed Loops into the same memory directory.