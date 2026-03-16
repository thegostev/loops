<img width="2816" height="1536" alt="loops_by_alex_gostev" src="https://github.com/user-attachments/assets/59acc66a-cfef-482f-8ebb-69d96c794929" />


[![Claude Code](https://img.shields.io/badge/Claude_Code-compatible-8B5CF6?logo=anthropic&logoColor=white)](https://claude.ai/code) [![Claude](https://img.shields.io/badge/Claude-co--work-8B5CF6?logo=anthropic&logoColor=white)](https://claude.ai) [![Slack](https://img.shields.io/badge/Slack-integrated-4A154B?logo=slack&logoColor=white)](https://slack.com) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# Loops

Track open Slack threads and conversation commitments - so Claude Code does the follow-up, not you.

---

## Who It's For

Loops is for professionals who live in Slack (or similar messengers) and need to track what they've committed to, what they're waiting on, and what's been resolved across dozens of concurrent threads.

It's specifically built for:

- **Managers and team leads** fielding async decisions, cross-team asks, and ongoing incidents
- **Executives** who are looped into many conversations but own only some of them
- **ICs** tracking review cycles, approval threads, and multi-party discussions across channels

You're the target user if:

- You handle multiple active Slack threads every day and can't always reply immediately
- You get mentioned frequently and lose track of which mentions still need action
- Your conversations stretch across days or weeks, often spanning multiple threads
- Topics you're following are spread across DMs, group chats, and channels simultaneously

---

## How It Helps

Loops offloads conversation tracking to Claude Code. Instead of mentally juggling which threads need a reply, which are parked waiting on someone else, and which have quietly resolved - Claude tracks all of it for you.

You open a loop when you get pulled into a conversation that will require follow-up. Claude logs it, assigns keywords, and maintains a live registry. At any point you can ask Claude what's open, what's urgent, and what's been resolved.

---

## The Value

- **Zero dropped threads** - every open conversation is logged until explicitly closed
- **Instant situational awareness** - ask Claude for a status snapshot at any time
- **Clear ownership** - each loop has a defined blocker: you or someone else
- **Durable record** - closed loops are never deleted; they're a searchable archive of decisions
- **Low overhead** - paste a conversation, describe what's needed, and you have a loop

---

## Use Cases

**Fielding async decisions as a PM**
You're tagged in a Slack thread about whether to proceed with a feature scope change. You weigh in but need a decision from engineering lead before you can close it. You open a loop marked `Waiting` - when the reply comes in, you close it with the outcome logged.

**Managing a cross-team incident**
An ops issue surfaces in three separate Slack threads with different stakeholders. You open one loop that captures all three, track who owns the resolution, and mark it closed once the post-mortem is complete.

**Tracking review cycles as an IC**
You submitted a design doc for review and are waiting on feedback from two people in different threads. One responded; one hasn't. Loops lets you see at a glance that one thread is still open and who's blocking it.

**Executive thread triage**
You're cc'd on a product escalation thread. You're not the decision-maker but need to follow up if nothing moves in 48 hours. You open a `Waiting` loop so you don't forget to check back.

**Coordinating across time zones**
A conversation starts Monday in one channel, moves to a DM on Wednesday, and lands in a group chat on Friday. Loops ties it to a single record with keywords, so you can find it regardless of where the latest message landed.

---

## Getting Started

**Prerequisites:** [Claude Code](https://claude.ai/code) (or Claude with tool use) and an MCP server for your communication tool (Slack, Teams, etc.) already configured.

1. **Clone this repo** and open it in your workspace
2. **Read [SETUP.md](SETUP.md)** — one-time configuration: choose where to place files, auto-discover your Slack channels, set up scan sources
3. **Open your first loop** — paste a conversation or run a bulk scan to populate existing threads
4. **Use [LOOPS.md](LOOPS.md) daily** — your registry of all open, waiting, and closed loops

Setup takes about 15 minutes. After that, Loops runs from LOOPS.md with near-zero overhead.

---

## How Loops Work

Every loop has three states:

| Status | Meaning |
|--------|---------|
| `Open` | You need to act - ball is in your court |
| `Waiting` | You acted, now waiting on someone else |
| `Closed` | Resolved, no further action needed |

Loops also carry a **priority**:

| Priority | Meaning |
|----------|---------|
| 🔴 | Needs attention now |
| 🟡 | Open / follow-up needed |
| ⚪ | Parked, no action now |
| 🟢 | Resolved (Closed table) |

The registry is sorted by priority (🔴 first), not by date.

Loops are tracked in `LOOPS.md` - a registry table that stays up to date as conversations evolve. Each loop also has its own file in `/Loops/` with a full entry history, so you can see how a thread progressed from start to resolution.

Loops are numbered per month: `YY-MM L01`, `YY-MM L02`, and so on. The counter resets each month. Closed loops are never deleted - they're moved to the Closed table and kept as a permanent record.

For the full working rules, see [LOOPS.md](LOOPS.md). For initial setup, see [SETUP.md](SETUP.md).
