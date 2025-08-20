Update the project memory with a structured changelog entry and optional section edits.

Steps:
1. Ensure `.claude/memory/memory.md` exists. If not, suggest `/project:create-memory`.
2. Determine summary:
   - If $ARGUMENTS provided, use as 1–2 line summary.
   - Otherwise, generate a terse summary of what was just done/decided.
3. Update `Last updated:` in `.claude/memory/memory.md` to current time.
4. Append to `## Changelog`:
   - `### <YYYY-MM-DD HH:MM TZ> — <summary>`
   - Git (if repo present):
     * branch: `<git rev-parse --abbrev-ref HEAD>`
     * last commit: `<git log -1 --oneline>`
     * changes: summarize `git status --porcelain` counts (A/M/D)
   - Details: 2–5 concise bullets of changes/decisions
5. Apply targeted section updates if directives are present in $ARGUMENTS (each on a new line):
   - `goal:+ <text>`           → add to Active goals
   - `goal:done <text>`        → move from Active to Done (append with date)
   - `invariant:+ <text>`      → add to Invariants (only stable truths)
   - `open:+ <question>`       → add to Open Questions
   - `decision:+ <title>`      → create ADR via `/project:memory-adr <title>` and link it
   - `convention:+ <rule>`     → add/update in Conventions
6. Never store secrets. Prefer links/paths over large dumps. Keep stable and deterministic.

Example usage:
- `/project:memory-update Implemented signup flow; goal:done Implement login page; open:+ How to handle email verification?`
- `/project:memory-update` (no args → auto-summarize recent change)
