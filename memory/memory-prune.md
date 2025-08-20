Prune and archive project memory to keep it concise and high-signal.

Safety: Non-destructive by default. Show a preview and require confirmation unless `confirm:true` provided.

Steps:
1. Ensure `.claude/memory/memory.md` exists. If not, suggest `/project:create-memory`.
2. Parse args (all optional):
   - `changelog:keep=<N>`          → keep last N entries in `## Changelog` (default: 100)
   - `done:keep=<M>`               → keep most recent M items in `### Done` goals (default: 50)
   - `snapshots:keep_days=<D>`     → suggest deleting snapshots older than D days (default: 90) — show list, do not delete unless `confirm:true`
   - `archive:true|false`          → write pruned content to files in `.claude/memory/archive/` (default: true)
   - `compress:true|false`         → if true, gzip archived files (default: false)
   - `dry_run:true|false`          → show diff only (default: true unless `confirm:true`)
   - `confirm:true`                → apply changes
3. Actions:
   - Changelog: move entries older than the last N to `.claude/memory/archive/changelog-<YYYY-MM>.md` (append, newest first in primary file)
   - Goals Done: move older-than-M items to `.claude/memory/archive/done-goals.md` with a timestamp
   - Open Questions: leave untouched unless explicitly directed (avoid losing context); consider tagging stale items instead of pruning
   - Snapshots: list candidates older than `keep_days`; only delete on `confirm:true`
4. After applying, update `Last updated:` and append a short `## Changelog` entry describing the pruning.
5. Never remove Invariants, Decisions, or Conventions automatically.

Example usage:
- `/project:memory-prune changelog:keep=80 done:keep=20`
- `/project:memory-prune snapshots:keep_days=60 confirm:true`
- `/project:memory-prune dry_run:true` (preview only)
