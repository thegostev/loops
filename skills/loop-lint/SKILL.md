---
name: loop-lint
description: Validate LOOPS.md and the Loops/ directory for consistency — registry sort order, Status/P match between registry and loop-file headers, duplicate or gap loop IDs, empty loops, stale Waiting loops beyond thresholds, Closed rows stranded in the Open table, and orphan files/rows. Reports issues grouped by severity and offers to apply safe mechanical fixes after confirmation. Trigger when the user asks to check, lint, or audit loops, or runs /loop-lint.
---

# Loop Lint

The registry is hand-edited markdown; drift is inevitable. This skill catches it before it misleads you. Run it after a scan, after closing several loops, or any time the registry feels off.

## Inputs

- `LOOPS.md` — the registry. Source of truth for the table view.
- `Loops/<loop-id>.md` — per-loop files. Source of truth for headers and entries.

## Checks

1. **Sort order** — the Open/Waiting table is sorted 🔴 → 🟡 → ⚪, and within a priority Open rows sit above Waiting rows, then newest `Last Update` first. Report out-of-order rows; offer to re-sort.
2. **Status/header match** — for each registry row, the `Status` and `P` columns equal the `Status:` and P in the corresponding loop-file header. Report mismatches; confirm sync direction per row before fixing (usually the file is newer — confirm, don't assume).
3. **ID integrity** — loop IDs are unique, sequential per month with no gaps, format `YY-MM LNN`. Report duplicates, gaps, and Open rows whose ID month doesn't match its `Opened:` date.
4. **Empty loops** — any loop file whose Entries section is empty (header only). Report; an open loop with no entry is a sign creation was interrupted.
5. **Stale Waiting** — any `Waiting` loop whose `Last Update` is older than the threshold (default 3 days). Flag for 🔴 escalation or a follow-up entry. (Pair with the staleness rule in LOOPS.md.)
6. **Orphan rows / files** — registry rows with no corresponding file in `Loops/`, or files with no registry row. Report both directions.
7. **Closed hygiene** — Closed-status rows appear only in the Closed table; no `Closed` status in the Open/Waiting table. Report stragglers; offer to move the row.

## Output

Group findings by severity:

- 🔴 **blocks trust** — mismatched Status/P, duplicate IDs, orphan row/file, empty open loop.
- 🟡 **drift** — out-of-order rows, stale Waiting, wrong-month ID, Closed row in Open table.
- ⚪ **polish** — gaps in the monthly sequence, cosmetic header differences.

For each safe, mechanical fix (re-sort, move a Closed row, sync header ↔ registry), offer to apply after confirmation. Never delete a loop file. For ambiguous fixes (which direction to sync Status), ask before acting.

## Pair with

- `loop-scan` — scan keeps loops current; lint keeps the registry honest. Run lint after every scan.