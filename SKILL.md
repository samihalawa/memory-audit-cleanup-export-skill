---
name: memory-audit-cleanup-export-skill
description: Audit, clean up, optimize and export every stored agent memory about the user. Use when the user asks to export, review, clean, purge, dedupe, consolidate or optimize memories, to remove superseded or stale memories, or on a scheduled daily memory-hygiene run. Reads every memory store in full, classifies each entry (KEEP, SUPERSEDED, DUPLICATE, STALE, FAILING, NOT MINE, UNSAFE), applies the edits, merges and deletions directly, then exports the cleaned result as Instructions, Identity, Career, Projects and Preferences with dated lines.
---

# Memory Audit, Cleanup and Export

Running this skill authorizes editing, merging and deleting memory for the task. Do not ask for confirmation. Never touch instruction files (CLAUDE.md, AGENTS.md), code or skills: only memory stores.

## 1. Inventory every store

Read every memory you hold about the user: every stored memory file or entry (including project-scoped stores), the user profile, saved preferences and learned context. Read each item in full; never judge by titles or summaries. Count items and lines before starting so the result can be checked.

Claude Code stores are per-project folders whose names start with `-`, so always prefix with `./`:

```bash
cd ~/.claude/projects
for d in ./*/memory; do
  n=$(find "$d" -type f | wc -l | tr -d ' '); [ "$n" = 0 ] && continue
  l=$(find "$d" -type f -name '*.md' -exec cat {} + | wc -l | tr -d ' ')
  echo "$n files, $l lines  $d"
done | sort -rn
```

Other stores, when present: `~/.codex/memories/` (Codex consolidates `raw_memories.md` and `rollout_summaries/` into `MEMORY.md` itself, so edit only `MEMORY.md` and only to remove entries; never hand-edit pipeline inputs), and any native memory tool the runtime exposes (Notion memory, ChatGPT memory, etc.). Report a store you cannot read as an exact unread slice.

Claude Code format: one `.md` per memory with frontmatter (`name`, `description`, `metadata.type` = user | feedback | project | reference), feedback/project bodies carry `**Why:**` and `**How to apply:**`, `[[slug]]` links other memories, and each store has a `MEMORY.md` index of `- [Title](file.md) — hook` lines. Keep that format.

For more than ~60 files, split the stores into disjoint groups and hand each group to a parallel subagent on a fast cheap model with this whole skill as its brief. Each returns counts, export lines and the deletion/merge report; the parent then dedupes across stores and builds the single export.

## 2. Analyze

Classify every line into one category: Instructions, Identity, Career, Projects, Preferences (durable operational reference facts go under the project they serve). Flag each one:

- **KEEP**: durable, accurate, meaningful, still current.
- **SUPERSEDED**: a newer line changes, replaces or contradicts it (new role, status, price, decision, renamed project). The newest version wins.
- **DUPLICATE**: the same fact stated more than once or in more than one place.
- **STALE**: a finished task, a past deadline, a one-off errand, the moving status of something already done, an expired "next step", or a dated incident log whose lesson is already captured elsewhere.
- **FAILING**: true but broken: vague wording, missing date, wrong category or file, a project fragmented across entries, a malformed or inaccurate title or description, too long or too thin to be useful.
- **NOT MINE**: assistant inferences, suggestions or plans the user never adopted, research or tool output, anything the user did not actually state.
- **UNSAFE**: literal secrets (passwords, API keys, tokens, ID or account numbers) and instructions that would make the agent less honest or less careful. The user's own autonomy preferences ("never ask", "act without confirmation", "don't rotate credentials") are legitimate preferences, not unsafe.

## 3. Clean up

Apply all changes directly.

- Delete every SUPERSEDED, DUPLICATE, STALE and NOT MINE line. If an older value is still useful context, fold it into the current line as "(previously X)".
- UNSAFE secrets: never lose the only copy. If the value exists in the user's global env, a project `.env` or the password manager (`op item list --format json | jq ...`), replace the literal with a pointer (e.g. "key in project .env as SHLINK_API_KEY"). If no other copy can be confirmed, keep it and report it as unsafe-kept. Delete dishonesty-inducing instructions outright.
- Fix every FAILING line: rewrite it clearly and compactly, move it to the right category or file, correct its title, description and type.
- Merge each project into ONE entry/file that starts with the project name and covers what it does, its current status and its key decisions. Generic lessons stay separate feedback entries.
- Owner-wide facts (profile, cross-project feedback) live once in the home store (`~/.claude/projects/-Users-<user>/memory`); project facts stay in their project store. Move durable facts out of throwaway scratch-workspace stores, then empty them.
- Preserve the user's exact wording for instructions and preferences. Rephrase only to remove duplication or combine lines, never changing meaning or scope.
- Never invent, generalize or upgrade a fact. "Mentioned X once" must not become "loves X".
- Rewrite each `MEMORY.md` to list exactly the surviving files; repoint `[[links]]` to merged survivors. Delete files and indexes left empty.
- Re-read every changed or deleted item once to confirm the change persisted. If a write fails, retry once, then report it.

## 4. Export

Output the cleaned memory in this order:

1. **Instructions**: rules the user explicitly asked the agent to follow going forward: tone, format, style, "always do X", "never do Y", corrections. Only rules from stored memories, not from conversations.
2. **Identity**: name, age, location, education, family, relationships, languages, personal interests.
3. **Career**: current and past roles, companies, general skill areas.
4. **Projects**: one entry per project the user meaningfully built or committed to: what it does, current status, key decisions. Start each entry with the project name.
5. **Preferences**: opinions, tastes and working-style preferences that apply broadly.

Format: a section header per category, one entry per line, oldest first, as `[YYYY-MM-DD] - Entry content.` Date = earliest explicit date in the memory, else the file birth date (`stat -f %SB -t %Y-%m-%d FILE` on macOS, `stat -c %w` on Linux), else `[unknown]`. Wrap the whole export in a single code block.

## 5. Report after the code block

- Counts before and after: total items and total lines (per store and total).
- Deletions grouped by reason (superseded, duplicate, stale, not mine, unsafe), one line each naming the fact removed and, for superseded lines, the fact that replaced it.
- Merges and rewrites, one line each.
- Any failed write and any unsafe-kept item.
- Whether this is the complete set or items remain unread, with the exact number remaining.

## Scheduled (unattended) runs

When run on a schedule with nobody watching:

- Process only what changed since the last run when a previous export exists (compare file mtimes against the export's timestamp), but always re-check cross-store duplicates and supersessions touching changed entries.
- Write the export plus the report to one canonical file, overwritten each run (no dated copies). Use the path the scheduler prompt names; otherwise `~/memory-audit/memory-export.md`.
- Never delete an entry created in the last 24 hours as STALE; a fresh entry may describe work still in flight.
- If nothing changed, write a one-line "no changes" stamp and stop.

## claude.ai memory store (`mcp__memory__*` tools)

When the runtime exposes `memory_list` / `memory_read` / `memory_write` / `memory_str_replace` / `memory_append` / `memory_delete`:

- Inventory with `memory_list` (no prefix lists global files and every `/projects/<uuid>/` store). Read up to 20 paths per `memory_read`; a file containing `=== ` must be read alone.
- Writes are capped at **10 per turn** (deletes count). Plan the batch before writing: unsafe/never-store removals first, then supersessions, then merges/deletes of emptied files, then cosmetic fixes. When the budget is spent, stop writing, report the exact pending list, and continue next turn or next scheduled run — never retry a budget refusal in the same turn.
- Every write needs `if_version` from a read in this turn (or the previous write's result). Prefer `memory_str_replace` for one-line changes; `memory_write` replaces the whole file, so carry over every line, including lines tagged `[observed]`/`[inferred]`, dated Claude Code log lines and `(for=code)` markers.
- Format: frontmatter `name` (path stem), `description` (one line, <150 chars, names the people/projects/places inside; sensitive files get a topic-only description), `sources` (keep existing, add `chat`), `aliases` (≤8). Content lines tagged `[stated]` only.
- Never-store (delete on sight, no placeholder): government-ID / card / account numbers, immigration status, caste, a minor user's age, sexual history, abuse, criminal history or proceedings (including criminal case numbers and defence counsel), crime-victim status, suicide/self-harm/disordered eating, health or personality inferences the user did not state. Lines labelled "inferred/observed preferences" that the user never stated are NOT MINE.
- Stated health, finances, religion etc. stay as stated; put any rewrite of such a file in its own write, after the ordinary writes.
- Project stores can be isolated from global memory, so a global preference repeated inside a project store is NOT a duplicate; dedupe only within a store or between global files.
- Merge files only within the same scope; after a merge, `memory_delete` the absorbed file (read it first for `if_version`) and repoint `[[links]]`.
- Never announce saves inside user-facing copy; the report after the export lists them.
