Search across project memory (`memory.md`) and ADRs for a query.

Steps:
1. Ensure `.claude/memory/memory.md` exists. If not, suggest `/project:create-memory`.
2. Parse args (optional):
   - `q:` the search query (default: use $ARGUMENTS as the query)
   - `files:` `memory|adr|all` (default: `all`)
   - `section:` restrict to memory.md headings (e.g., `Goals`, `Invariants`, `Conventions`, `Open Questions`, `Changelog`, `Architecture`)
   - `context:` number of context lines around matches (default: 1)
   - `limit:` max results (default: 10)
3. Search targets:
   - memory: `.claude/memory/memory.md`
   - adr: `.claude/memory/adr/*.md`
4. Output concise results: `path:line — snippet`, grouped by file, newest first when timestamps are available.
5. If `section:` provided, detect heading ranges in `memory.md` and only return matches within the section.
6. End with suggested next actions (e.g., `goal:+`, `decision:+`) if the query surfaced actionable items.

Example usage:
- `/project:memory-search q:login files:all limit:5`
- `/project:memory-search section:Open Questions q:deployment`
- `/project:memory-search q:"database schema" context:2`

Example output:
```
.claude/memory/memory.md:72 — Added login page and session cookie
.claude/memory/adr/20250819-choose-nextjs.md:14 — Decision: Use Next.js for SSR
```
