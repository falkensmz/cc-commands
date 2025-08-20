Create a timestamped snapshot of the project memory for audit and recovery.

Steps:
1. Ensure `.claude/memory/memory.md` exists. If not, suggest `/project:create-memory`.
2. Ensure directories exist: `.claude/memory/snapshots/`.
3. Determine metadata (if in a git repo):
   - branch: `git rev-parse --abbrev-ref HEAD`
   - short commit: `git rev-parse --short HEAD`
4. Create snapshot file:
   - Path: `.claude/memory/snapshots/<YYYY-MM-DD-HHMM>--<branch>@<shortsha>.memory.md`
   - If git info not available, use `.claude/memory/snapshots/<YYYY-MM-DD-HHMM>.memory.md`
5. Write snapshot contents:
   - Header with timestamp, branch/commit if available
   - Optional: size stats (lines, bytes) of `memory.md`
   - Full copy of current `.claude/memory/memory.md` content below the header
6. Append a short entry to `## Changelog` in `memory.md` noting the snapshot created.
7. Retention (non-destructive):
   - Keep at least the last 30 snapshots
   - Prefer daily latest for last 90 days
   - Suggest pruning older snapshots via manual cleanup if disk usage is high

Example output confirmation:
```
Created snapshot: .claude/memory/snapshots/2025-08-20-1725--main@abc123.memory.md (842 lines)
```
