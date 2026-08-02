# Memory Templates

Skeleton files for the four memory types used by the auto-memory system. Consumed by the `weekly-interview` and `loop-memory-bridge` skills when writing new memory entries.

## Usage

Copy these into your memory directory (for Claude Code: `~/.claude/projects/<project-slug>/memory/templates/`) on first use. The skills read from there when writing new entries.

## Types

| Type | When to use |
|------|-------------|
| `user` | The user's role, preferences, responsibilities, or knowledge |
| `feedback` | Guidance the user has given about how to approach work — what to avoid and what to keep doing |
| `project` | Ongoing work, goals, decisions, or incidents not derivable from the code or git history |
| `reference` | Pointers to external systems (Linear, Slack channels, dashboards, docs) |

## Schema notes

- Every memory file has frontmatter: `name` (a short kebab-case slug), `description`, and `metadata.type` (one of `user`, `feedback`, `project`, `reference`). The harness reads `metadata.type` for recall filtering, so keep it nested under `metadata:` — not a top-level `type:` field.
- `feedback` and `project` types include `**Why:**` and `**How to apply:**` lines below the body. The *why* lets future-you judge edge cases instead of blindly following the rule.
- `user` and `reference` types use a single body paragraph plus optional `**Why it matters:**` for reference.
- Link related memories with `[[their-slug]]` where relevant. A link that doesn't match an existing file yet is fine — it marks something worth writing later, not an error.
- The `MEMORY.md` index is one line per file, under ~150 chars. It is loaded into context every session, so keep it lean.

## What not to save

- Code patterns, conventions, architecture, file paths — derivable from the codebase.
- Git history, recent changes, who-changed-what — `git log` and `git blame` are authoritative.
- Debugging solutions or fix recipes — the fix is in the code, the context is in the commit message.
- Ephemeral task state — use tasks, not memory.