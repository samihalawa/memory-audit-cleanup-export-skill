---
name: memory-audit-cleanup-export-skill
description: Audit, reconcile, clean up and optionally export in-scope agent memories. Use for requested memory review, deduplication, correction, consolidation, deletion or scheduled hygiene. Inventory and fully read the bounded population, preserve source chronology and useful learning, apply only runtime-authorized changes, verify results and distinguish applied changes from queued correction requests.
---

# Memory Audit, Cleanup and Export

## Authority and runtime first

Bind the user's task mode, accounts, stores, scope, exclusions and output. Apply current owner authority to evident in-scope audit fixes while respecting an explicit read-only or report-only request and higher-priority runtime rules. This skill supplies a procedure; it grants no independent permission to edit or delete memory. An export request alone does not authorize unrelated cleanup.

Inspect the current runtime's native memory instructions, exposed tools, schemas, authentication and persistence contract before selecting a route. Discovering a similarly named tool does not establish authority over this runtime's memory. Never substitute an unrelated application's memory namespace, including Notion, or infer that no memories exist from its empty result.

Use the supported native route. If direct mutation is forbidden, submit precise correction/deletion notes through the allowed route and report their actual state. Never use another executor, tool or filesystem route to bypass that boundary. Do not edit instruction files, code, skills or unrelated stores during a memory audit unless separately requested.

## Inventory and source coverage

1. Recover the existing relevant audit, review or export and its coverage, decisions, unresolved corrections and source locators. Reuse verified findings; inspect the changed delta and affected dependencies instead of restarting completed work.
2. Enumerate every discoverable in-scope store and item, including project scopes and nested payloads. Record stable IDs/paths, versions, counts, pagination cursors and inaccessible slices in runtime context. Do not create a parallel tracker.
3. Read every in-scope item in full through bounded pages or chunks before classification. Titles, descriptions, snippets and summaries are locators, not full coverage. Never force one giant dump or equate a sample with completion.
4. Count items and, for text stores where meaningful, lines per store and in total. Distinguish entries, files and lines; state unknown counts rather than inventing them.
5. Use available delegation only when permitted and useful for context or independent work. Assign disjoint read-only ranges and concise evidence returns; keep one mutation owner per store. No fixed file-count threshold mandates agents.

Recover decisive original conversations or source passages for material conflicts, owner preferences and changing project facts. Search exact entities/IDs and read the relevant complete segments. Use current primary records for present provider state. Chronicle, Screenpipe or other history can locate evidence when available and relevant; they do not supersede the underlying conversation, file or provider.

Resolve chronology by the actual statement or event time and scope. A copied file's latest modification time, an assistant's later summary or the newest search hit does not supersede an earlier owner decision. Distinguish source dates, observation dates and import dates; preserve uncertainty where the original date is unavailable.

## Classification

Classify each substantive fact with its source, scope, date, reason and proposed survivor or correction:

- **KEEP:** accurate durable user knowledge, current instructions or useful verified project/technical learning. Proven working routes, failed routes with causes and tool behavior can be valid project knowledge even when the user did not personally state them.
- **SUPERSEDED:** an authoritative later correction or verified change replaces the same fact in the same scope. Identify the replacement and retain useful provenance.
- **DUPLICATE:** materially equivalent content within compatible visibility and scope. Identify a complete survivor; isolated project/global visibility may justify repetition.
- **STALE:** an obsolete transient status, completed errand or expired next step with no remaining operational value. Age alone is insufficient.
- **FAILING:** useful content needs a precise correction, date, title, category, scope, source or clearer wording; repair it rather than discarding it.
- **NOT MINE:** misattributed identity or an unadopted assistant suggestion, plan or inferred preference presented as the owner's position. Do not classify verified technical evidence as NOT MINE merely because it came from a tool.
- **UNSAFE:** content prohibited by the actual current provider/runtime memory policy, exposed secrets requiring its supported handling, or instructions that require fabricated evidence or bypass a real boundary. Apply current policy rather than a foreign provider's fixed sensitive-data list.

Preserve the meaning, limits and dates of explicit owner instructions. Do not turn a one-time mention into a preference, a hypothesis into a fact, or an assistant proposal into an adopted decision. Legitimate autonomy preferences are not automatically unsafe and do not override runtime restrictions.

Keep active future deadlines, genuine external waits, obligations, receipt/proof locators and still-relevant owner corrections. A filing receipt proves filing, not admission or award. Dated incidents may retain a compact reusable lesson even when their transient narrative can be removed.

## Apply authorized cleanup

Read each mutation target and its current version; preserve unrelated content, other authors and concurrent changes. Prefer exact fact-level edits over deleting an entire mixed entry or task block. Before removing a duplicate or superseded fact, prove its survivor is complete and will remain readable in the required scope.

- Apply only changes allowed by the task mode and current runtime contract. Repair FAILING facts and consolidate compatible fragments without forcing every project into one oversized entry.
- Merge only compatible scopes. Preserve source links, aliases, intentional labels and cross-references; update indexes to the actual surviving records. Do not empty scratch stores by assumption.
- Preserve exact identity and genuine evidence. Never create a credential or source claim. Handle secrets according to current policy and authorized credential storage; a pointer requires a verified destination and must not expose the value in an export.
- Use supported version/concurrency guards. On conflict, read the changed delta and rebase the exact intended change. Respect actual provider quotas, refusal meanings and retry guidance; do not import a fixed write quota from another runtime or retry unchanged failures.
- Re-read each changed target once, and verify deletions through the supported absence check. A write response or queued note alone does not prove consolidation. Continue independent permitted changes while a genuine dependency remains.

When only notes are allowed, write one concise idempotent correction request per coherent change through the prescribed route. Include exact target IDs/paths or source locators, the incorrect fact, requested replacement/removal, evidence/date, scope and survivor. Check existing notes first; verify the saved note. Do not copy secrets into the request. State that correction was requested and whether consolidation remains unverified.

## Store adapters

### Native Codex memory

Use the runtime-provided memory root and instructions for retrieval. If the contract permits only update notes, use that exact route (for example, the supplied `extensions/ad_hoc/notes/` directory and filename convention). Do not directly edit or delete `MEMORY.md`, raw memories, rollout summaries or pipeline inputs. Do not claim the requested deletion happened merely because its note persisted. If the runtime grants different capabilities, follow its current explicit contract rather than assuming universal filesystem rights.

### Existing Claude/local indexed stores

Operate only on discovered, authorized stores. Preserve their existing frontmatter, types, source metadata, aliases, `[[links]]` and index conventions rather than imposing a foreign schema. A Claude project memory directory may use one Markdown file per topic and a `MEMORY.md` index of linked one-line descriptions; preserve that format when present. Quote paths and prefix relative paths beginning with `-` with `./`.

For exposed native memory tools, inspect their current list/read/write/delete schema, pagination, version guards, visibility boundaries and policy. Retain meaningful observed/project evidence in its proper category; label explicit user statements accurately. Never impose a historical tool batch size, ten-write limit or sensitive-data blacklist as a current contract.

### Explicit Desktop Commander workspace memory

Use `${workspacePath}/.memory/` only when the actual runtime supplies that workspace path, authorizes this store and provides a valid `dc://` source-link contract. Do not infer those values or bootstrap a workspace graph inside Codex as a substitute for native memory.

Read the existing `index.md` first, then relevant `topics/*.md`. Preserve a legitimate topic index with one-line links and topic entries containing a date, a concise durable event/decision and its original `dc://` provenance link. Create/update a topic only when authorized and genuinely new; do not duplicate source content or invent a source URL. Preserve valid source links during cleanup and use them when relevant to an answer. Routine retrieval and writes stay quiet; do not append a canned “Saved to memory” footer.

## Export only when requested or scheduled

Reuse the requested canonical artifact and destination, or the applicable reporting policy's destination. Preserve other authors' and cloud/local sections; each executor updates only its owned section. Do not create exports, dated variants, logs or local scratch files for an audit that does not request them.

Organize the requested export as Instructions, Identity, Career, Projects and Preferences unless the user specifies another format. Put verified operational learning under its project; distinguish it from owner-stated instructions/preferences. Start project entries with the project name. Preserve useful density without repeating facts across categories.

Use one entry per line, oldest first, formatted `[YYYY-MM-DD] - Entry content.` Use the actual earliest supported statement/event date for that fact; use `[unknown]` when unavailable, not a file-copy or modification date. An inline export may use one code block; preserve an existing artifact's section and formatting contract.

Before publishing, check exact copy, attribution, dates, source coverage, counts, active waits and the applied/requested distinction. Open/read the persisted artifact once. A local save does not prove cloud synchronization; report the verified layer only.

## Scheduled execution and closure

A scheduler prompt should invoke this canonical skill with scope, ownership and output destination rather than embedding a second policy. Reuse the previous verified baseline and process changed items plus affected cross-store duplicates/supersessions; an mtime is a delta locator, never proof of factual chronology or full coverage. If the baseline is incomplete, cover the missing slice before claiming completeness.

Retain recent in-flight work until source evidence proves it obsolete; no arbitrary age cutoff replaces that check. If nothing substantive changed, avoid rewriting the export merely to stamp a date unless the scheduler specifically requires it. Do not overwrite other executors' sections.

Return the outcome with per-store and total before/after counts, exact coverage and unread slices, applied edits/deletions by reason, survivors, merges/rewrites, source conflicts resolved, failed writes and pending note-based requests. Separate reviewed, directly changed, correction requested and verified consolidated. Do not report “cleaned” or “deleted” for changes merely proposed or awaiting native consolidation. Finish feasible in-scope work and name only the genuine remaining dependency.
