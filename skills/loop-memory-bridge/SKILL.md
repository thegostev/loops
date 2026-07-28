---
name: loop-memory-bridge
description: When a loop in LOOPS.md closes with a notable decision, incident, or feedback, write a corresponding entry to long-term memory (project or feedback type). Scans closed loops in /Loops/, asks the user which resolutions are memory-worthy, and writes using templates from memory/templates/. Trigger when the user asks to "harvest loops into memory" or runs /loop-memory-bridge.
---

# Loop Memory Bridge

Loops tracks open commitments. Memory tracks durable lessons. When a loop closes, sometimes its resolution is worth remembering long after the loop itself is archived. This skill bridges the two: it walks recently closed loops, asks which resolutions are memory-worthy, and writes those to the long-term memory directory.

## Inputs

- `LOOPS.md` — the registry. Source of truth for closed-loop metadata.
- `/Loops/<loop-id>.md` — per-loop files. Source of truth for resolution detail.
- `memory/templates/` — skeletons for `project.md`, `feedback.md`, `reference.md`.
- `MEMORY.md` — the memory index, updated as new entries are written.

## Steps

1. **Find recently closed loops.** Read `LOOPS.md` and look at the Closed table. Look for a `Last bridged` stamp near the top of the file. If present, only consider loops closed after that date. If absent, treat all closed loops as candidates and ask the user for a starting cutoff ("bridge everything since YYYY-MM-DD?").

2. **For each candidate, open the loop file** in `/Loops/` and read the resolution entry (the final entry in the file's Entries section).

3. **Filter and ask.** For each closed loop, present a one-line summary and ask whether to save:
   ```
   Loop 26-07 L04 — "Slack thread on auth migration timing"
   Closed: 2026-07-24
   Resolution: Decided to ship behind a feature flag, defer cutover to Q3.
   Save to memory? (yes / no / skip-rest)
   ```

   Skip noise — routine approvals, "answered a question", status updates with no decision.

   Surface — decisions that change approach, incidents with postmortem-worthy lessons, feedback that should shape future behavior, new external references discovered.

4. **For each "yes" answer, write a memory file:**
   - Decision or incident → `project.md` type
   - Guidance that should shape future work → `feedback.md` type
   - New dashboard/channel/doc → `reference.md` type
   - Read the matching template from `memory/templates/` and fill in.
   - For `feedback` and `project` types, include:
     - **Why:** the loop ID + date (e.g., "Loop 26-07 L04, closed 2026-07-24") so future-you can trace back to the source.
     - **How to apply:** when this should shape future suggestions.
   - File naming: `<topic-slug>.md`. If a memory file already covers this topic, update it instead of creating a new one.

5. **Update the MEMORY.md index** with one-line entries for each new file. Keep entries under ~150 chars.

6. **Update LOOPS.md** with a `Last bridged: YYYY-MM-DD` stamp near the top (next to `Last scanned`). This lets the next run skip already-processed loops.

7. **Summary.** Print a one-paragraph summary: how many loops scanned, how many bridged, how many skipped as noise, and any patterns (e.g., "3 loops about the same auth migration — consider a single project memory instead of three").

## What not to bridge

- Loops that closed without a real decision ("answered", "acknowledged", "approved with no change").
- Loops whose resolution is already covered by an existing memory file — update that file instead.
- Loops about ephemeral state — that belongs in tasks, not memory.

Memory noise is worse than no memory. When in doubt, skip.

## Pair with

- `weekly-interview` — the bridge is one input to memory; the weekly interview is the other. The interview catches things that never became loops; the bridge catches things that did.