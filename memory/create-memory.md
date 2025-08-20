Initialize a robust project memory. Do NOT overwrite existing memory without explicit confirmation.

Steps:
1. Ensure directories exist:
   - `.claude/memory/`
   - `.claude/memory/adr/`
   - `.claude/memory/snapshots/`
   - `.claude/memory/archive/`
2. If `.claude/memory/memory.md` exists: confirm with the user before resetting. Otherwise, create it from the skeleton below.
3. After creation, append an initial entry to the `Changelog` section noting the initialization time.
4. Remind: never store secrets in memory; store references only.

Skeleton to write to `.claude/memory/memory.md`:

```markdown
# Project Memory

Last updated: <YYYY-MM-DD HH:MM TZ>

## Overview
- Project: <name>
- Scope: <what we’re building>
- Repo: <url or path>

## Invariants (Pinned Facts)
- [ ] <important fact to keep in view>

## Goals
### Active
- [ ] <goal>
### Upcoming
- [ ] <goal>
### Done
- [ ] <goal>

## Decisions (ADR Index)
- [Pending] Create ADRs via /project:memory-adr and list them here

## Architecture
- Context
- Constraints
- Modules / Ownership
- Data model
- External services

## Conventions
- Languages / versions
- Code style / formatting
- Branching & commit style
- Directory layout

## Environments
- Dev / Staging / Prod and notable differences

## Tooling
- Package manager, build, test, CI
- Secrets: referenced via <vault/manager>; never store secrets here

## Open Questions
- [?] <question>

## Glossary
- <term>: <definition>

## References
- <link or doc path>

## Changelog
### <YYYY-MM-DD HH:MM TZ> — Initialized memory
- Summary: Created structured project memory
- Git: branch <name> @ <short-commit> (if available)
- Files: +1 memory.md
```

Output: confirm the memory was created (or already exists) and point to `/project:load-memory` for a status view.
