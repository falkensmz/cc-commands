Create or update an Architecture Decision Record (ADR) and index it in memory.

Purpose:
Capture durable decisions with context and consequences.

Steps:
1. Ensure `.claude/memory/memory.md` exists. If not, suggest `/project:create-memory`.
2. Ensure directory `.claude/memory/adr/` exists.
3. Parse $ARGUMENTS:
   - Title (required)
   - Optional flags: `status:proposed|accepted|deprecated|superseded`, `supersedes:<adr-id>`, `context:<short>`, `decision:<short>`
4. Create ADR filename:
   - ID: `<YYYYMMDD>`
   - Slug: kebab-case of the title
   - Path: `.claude/memory/adr/<ID>-<slug>.md`
   - If file exists, append a new "Update" section with timestamp.
5. Write ADR template if new:
```
# ADR <ID>: <Title>

Status: <status|accepted>
Date: <YYYY-MM-DD>
Supersedes: <adr-id or none>
Superseded-by: <none>

## Context
<context or expand later>

## Decision
<decision>

## Consequences
- <positive/negative consequence>

## Alternatives Considered
- Option A — pros/cons
- Option B — pros/cons

## References
- <link or doc path>

## Updates
- <YYYY-MM-DD HH:MM TZ> — Created
```
6. Update `## Decisions (ADR Index)` in `.claude/memory/memory.md`:
   - Add a new top entry linking to the ADR path with short one-line summary.
   - Keep newest first.
7. Append to `## Changelog` an entry noting the ADR addition/update.
8. If `supersedes:` provided, open the prior ADR and set `Superseded-by` to the new ADR ID and optionally set its Status to `superseded`.

Example:
- `/project:memory-adr Choose Next.js for SSR status:accepted`
- `/project:memory-adr Switch DB to Postgres status:proposed context:"Need transactions"`
