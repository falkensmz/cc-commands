Show a concise status view of project memory and enable auto-updates after each request.

Steps:
1. Check `.claude/memory/memory.md` exists. If not, suggest `/project:create-memory`.
2. If it exists, produce a compact status:
   - Last updated timestamp
   - Auto-update: ON/OFF (read from `.claude/memory/.auto-update`, default OFF if missing)
   - Active goals (top 5)
   - Invariants (top 5)
   - Recent changes (last 3 entries from Changelog)
   - ADR index: list latest 3 from `.claude/memory/adr/`
3. Output must be terse and actionable.

Auto-update behavior (after EACH answered user request; only when Auto-update is ON):
1. Open `.claude/memory/memory.md` and update `Last updated:` to current time.
2. Append to `## Changelog` a new entry:
   - `### <YYYY-MM-DD HH:MM TZ> — <1-line summary>`
   - Git (if repo present):
     * branch: `<git rev-parse --abbrev-ref HEAD>`
     * last commit: `<git log -1 --oneline>`
     * changes: summarize `git status --porcelain` (added/modified/deleted counts)
   - Details: 2-5 bullets of what changed/decided
3. Maintain sections intelligently:
   - Goals: mark completed/in-progress; add next actions if clear
   - Invariants/Conventions: add/update only if stable, not transient
   - Open Questions: add new questions; when resolved, move the answer to Decisions/ADR
   - Decisions: when a meaningful decision is made, create/update an ADR via `/project:memory-adr` and link it
4. Keep entries stable, deterministic, and concise. Prefer links/paths over large dumps. Never store secrets.
5. Respect the toggle: only perform auto-updates when `.claude/memory/.auto-update` contains `on` (case-insensitive). Use `/project:memory-auto` to change it.

Example status output:
```
Memory — Last updated: 2025-08-20 17:22 +03:00
Auto-update: ON
Active goals: 3 (ship MVP auth, add tests, containerize)
Invariants: 2 (Node 20; PostgreSQL 15)
Recent: 2025-08-20—Added login page; 2025-08-19—Chose Next.js; 2025-08-18—Set up CI
ADRs: 20250819-choose-nextjs, 20250818-ci-stack, 20250817-db-choice
```
