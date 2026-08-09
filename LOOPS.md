# Loops

> **Last scanned:** _not yet scanned_
> **Last bridged:** _not yet bridged_
> **Scan config:** [slack-sources](slack-sources.md)

## Rules

**Before creating a new loop:**

1. Check the **Open** and **Waiting** loops below — the thread may already be tracked
2. Check **Closed** loops — the thread may have been resolved already
3. Only if not found: create a new loop file in `/Loops/` and add it to the registry below

**When updating a loop:**

1. Open the loop file from the registry link below
2. Add a new entry **at the top** of the Entries section (reverse chronological — newest first)
3. Update **P**, **Status**, **Last Update**, and **Owner/Blocker** in the registry table below to match

**Keywords index:** when you create or update a loop, add or refresh its row in the Keywords Index (keywords → loop ID link) so the index stays a working cross-reference, not a flat list.

**Status definitions:**

| Status | Meaning |
|--------|---------|
| `Open` | You need to act — ball is in your court |
| `Waiting` | You acted, now waiting on someone else |
| `Closed` | Resolved, no further action needed |

**Priority (P column):** 🔴 needs attention now · 🟡 open/follow-up needed · ⚪ parked, no action now · 🟢 resolved (Closed table only)

**Registry sort order:** 🔴 first, then 🟡, then ⚪. Sort by priority, not chronologically.

**Staleness & escalation:**

- A `Waiting` loop with no new entry for **3+ days** auto-escalates to 🔴 on the next scan — the follow-up you promised is slipping.
- An `Open` loop untouched for **5+ days** drops to 🟡 until you re-confirm it's still active.
- `loop-lint` flags any loop crossing these thresholds so nothing ages silently. Escalation changes P only; it never closes a loop for you.

**Closing a loop:**

- Change status to `Closed` and P to 🟢 in both the registry table and the loop file header
- Add a final entry in the loop file with the resolution
- Move the row from Open/Waiting table to the Closed table
- Loops are never deleted — they serve as a record

**Numbering:**

- Loops are numbered sequentially per month: `YY-MM L01`, `YY-MM L02`, etc.
- The counter resets each month

**Archive rotation:**

- At month end, move Closed rows into a monthly archive file `LOOPS-archive-YY-MM.md` (same Closed table format). LOOPS.md's Closed table keeps only the current month's closures plus a one-line pointer to recent archives.
- Closed loop files stay in `/Loops/` permanently — they are never deleted.

**Month-boundary behavior:**

- An open loop keeps its original ID across the month boundary: a `26-07 L03` still open in August stays `26-07 L03`. IDs are never renumbered.
- The sequential counter starts fresh at `L01` for the first new loop opened in each month.

---

## Loop Registry

### Open / Waiting

| # | P | Loop | Status | Opened | Last Update | Owner/Blocker | Squad |
|---|---|------|--------|--------|-------------|---------------|-------|

### Closed

| # | P | Loop | Status | Opened | Closed | Resolution |
|---|---|------|--------|--------|--------|------------|

---

## Keywords Index

Quick-reference for finding a loop by topic. Each row links keywords to its loop so you can locate a thread without grepping every file. The scan and loop-memory-bridge skills keep this in sync as loops are created and updated.

| Keywords | Loop |
|----------|------|
