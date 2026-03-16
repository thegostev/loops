# Loops

> **Last scanned:** _not yet scanned_
> **Scan config:** [[slack-sources]]

## Rules

**Before creating a new loop:**

1. Check the **Open** and **Waiting** loops below — the thread may already be tracked
2. Check **Closed** loops — the thread may have been resolved already
3. Only if not found: create a new loop file in `/Loops/` and add it to the registry below

**When updating a loop:**

1. Open the loop file from the registry link below
2. Add a new entry **at the top** of the Entries section (reverse chronological — newest first)
3. Update **P**, **Status**, **Last Update**, and **Owner/Blocker** in the registry table below to match

**Status definitions:**

| Status | Meaning |
|--------|---------|
| `Open` | You need to act — ball is in your court |
| `Waiting` | You acted, now waiting on someone else |
| `Closed` | Resolved, no further action needed |

**Priority (P column):** 🔴 needs attention now · 🟡 open/follow-up needed · ⚪ parked, no action now · 🟢 resolved (Closed table only)

**Registry sort order:** 🔴 first, then 🟡, then ⚪. Sort by priority, not chronologically.

**Closing a loop:**

- Change status to `Closed` and P to 🟢 in both the registry table and the loop file header
- Add a final entry in the loop file with the resolution
- Move the row from Open/Waiting table to the Closed table
- Loops are never deleted — they serve as a record

**Numbering:**

- Loops are numbered sequentially per month: `YY-MM L01`, `YY-MM L02`, etc.
- The counter resets each month

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

Quick-reference for searching threads and linking to loops.

| # | Keywords |
|---|----------|
