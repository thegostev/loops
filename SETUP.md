# Loops Setup Guide

Complete this guide once to configure Loops for your workflow. After setup, your daily operations happen in [LOOPS.md](LOOPS.md).

---

## Step 1: Choose where to place Loops

Decide where your Loops files will live. Common options:

| Location | When to use |
|----------|-------------|
| Workspace root | Simple projects, single-repo setups |
| Obsidian vault | If you use Obsidian for notes and want loops alongside your knowledge base |
| Dedicated folder | If you want loops isolated from other project files |

Your target file layout:

```
your-chosen-location/
├── LOOPS.md              ← Loop registry (daily operations)
├── slack-sources.md      ← Scan configuration (created in Step 4)
└── Loops/                ← Individual loop files
```

> Copy `LOOPS.md` from this repo to your chosen location. Create the `Loops/` directory there.

---

## Step 2: Verify MCP access

Loops relies on MCP (Model Context Protocol) to read your conversations. You should already have an MCP server configured for your communication tool.

**What Loops needs from your MCP setup:**

| Capability | Why |
|------------|-----|
| Search messages | Find threads where you were mentioned or participated |
| Read channels | Scan specific channels for new activity |
| Read DMs | Check direct messages for open threads |
| Read user profiles | Resolve names and IDs |

Verify by asking Claude to search a channel you're active in. If it works, you're good.

**Supported tools:** Slack (primary), Teams, Discord, or any messenger with an MCP server. Loops also works with Jira MCP and Linear MCP for teams where discussions happen in tickets.

---

## Step 3: Discover your Slack activity

Before manually listing channels, let Claude do the initial discovery. Ask Claude:

> "Search Slack to find: (1) my Slack @name and user ID, (2) all public and private channels where I posted or was mentioned in the last 1 month, (3) DM conversations I was active in during the last 1 month. List everything you find."

Claude will return:
- Your Slack display name and user ID (e.g., `U09XXXXXXXX`)
- A list of channels with your recent activity
- A list of people you've been DMing

**Review the results.** Remove channels that are noise (e.g., #random, #social). Add any channels Claude missed that you know are important. This becomes the input for your scan configuration in Step 4.

---

## Step 4: Create your folder structure

If you haven't already:

1. Copy `LOOPS.md` from this repo to your chosen location
2. Create a `Loops/` directory next to it

```bash
mkdir Loops
```

---

## Step 5: Create your scan configuration

Create `slack-sources.md` in your Loops location. Use the channel list from Step 3 as your starting point.

### Format

```markdown
# Slack Sources — Loop Scanning Config

> Referenced by the scanning skill.
> Update this file when channels or people change.

## Your Slack ID

`UXXXXXXXXXX`

## Channel Batches

### Batch 1: Broad Sweeps

Catch-all searches across all channel types:
- `to:<@YOUR_SLACK_ID>` — anyone mentioning/DMing you
- `from:<@YOUR_SLACK_ID>` — threads you started (catch hanging loops with no reply)

### Batch 2: Primary Channels

| Channel | Purpose |
|---------|---------|
| #your-team-channel | Your team's main channel |
| #cross-team-channel | Cross-team discussions |

### Batch 3: Secondary Channels

| Channel | Purpose |
|---------|---------|
| #project-channel | Project-specific |
| #other-team | Adjacent team |

### Batch 4: Low-Traffic Channels

| Channel | Purpose |
|---------|---------|
| #announcements | Announcements |
| #temp-initiative | Temporary initiative channel |

## DMs

People who DM you directly — search with `channel_types: "im,mpim"`:

| Person | Context |
|--------|---------|
| Jane Smith | Your manager |
| Bob Jones | Tech lead |

## Group DMs

People in group DMs — search with `channel_types: "mpim"`:

| Person | Context |
|--------|---------|
| Alice Chen | Cross-team stakeholder |

## Search Tips

- Use `include_context: false` for channel sweeps (reduces noise)
- Use `include_context: true` for DM searches (thread context matters)
- If a search returns 20+ results, paginate with cursor
- Group DMs have no channel names — search by participant with `channel_types: "mpim"`
- Always append `after:YYYY-MM-DD` using the `Last scanned` date from LOOPS.md
```

### Why batches?

Scanning all channels in one search can hit API rate limits. Batches let Claude:
- Parallelize searches within a batch
- Sequence across batches (high-traffic first)
- Surface urgent items before low-traffic channels

Organize channels from Step 3 into batches: put your team channels and frequent DMs in early batches, announcement channels and temp channels in later batches.

---

## Step 6: Set up a scanning skill (optional)

If your Claude Code setup supports custom skills/commands, you can automate periodic scanning. A scanning skill should:

1. Read `Last scanned` date from LOOPS.md
2. Read channel/people config from `slack-sources.md`
3. Search each batch using `after:` the last scanned date
4. For each finding: create a new loop, update an existing loop, or skip noise
5. Update the LOOPS.md registry (sorted by priority: 🔴 → 🟡 → ⚪)
6. Update the `Last scanned` timestamp in LOOPS.md

Without a skill, you can do this manually by asking Claude to scan your channels.

---

## Step 7: Personalize your setup

### Naming conventions

Establish a consistent way to reference people in loop files. A common pattern:

- **First name + surname initial:** "Jane S.", "Bob J."
- Use this everywhere: loop files, registry, keywords

### Squads / teams

If you track loops across multiple teams, define squad names for the registry's Squad column:

| Squad name | Scope |
|------------|-------|
| _Your Team A_ | _Description_ |
| _Your Team B_ | _Description_ |
| _Cross-squad_ | _Items spanning teams_ |

### Loop file template

Each loop file follows this structure:

```markdown
# Loop Title

> **Loop:** YY-MM LNN
> **Status:** Open | Waiting | Closed
> **Opened:** YY-MM-DD
> **Last Update:** YY-MM-DD
> **Squad:** Team Name
> **Jira:** [TICKET-ID](url) _(optional)_
> **Slack:** [Thread](url) _(optional)_
> **People:** Person A., Person B.
> **Keywords:** keyword1, keyword2, keyword3

**Summary:** One-sentence description of what this loop is about.

**Current state:** What's happening right now and who's blocking.

---

## Entries

---

### YY-MM-DD — Entry title

Source: link to thread or meeting notes

What happened. Key decisions, quotes, or context.

**Next action:** Who needs to do what.

---
```

---

## Step 8: Open your first loop

Two options:

**Option A — Single loop from a conversation:**
Paste a Slack thread into Claude and ask:

> "Here's a Slack thread I'm involved in. Please open a loop for it."

Claude will create a loop file in `/Loops/`, add it to the registry in LOOPS.md, and generate keywords.

**Option B — Bulk scan to populate existing threads:**
Ask Claude to scan your recent Slack activity and create loops for any open threads:

> "Scan my recent Slack activity using slack-sources.md and create loops for any threads that need follow-up."

Claude will identify threads where you're waiting on someone or need to act, and create loops for each one.

---

After setup, all daily operations happen in [LOOPS.md](LOOPS.md). You can refer back to this guide if you need to add channels, update your scan config, or onboard a teammate.
