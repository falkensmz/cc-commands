# cc-commands

A curated set of Claude Code commands to supercharge day-to-day development. This repo focuses on a durable, high-signal project memory system that replaces ad-hoc notes and ephemeral sessions.

- Location (local): `~/.claude/commands/`
- Memory root: `~/.claude/memory/`

## Features
- **Memory-first workflow** with structured `memory.md`
- **Automatic updates** after each request (toggleable)
- **Git-aware changelog entries**
- **Architecture Decision Records (ADRs)**
- **Snapshots & pruning** for long-term hygiene
- **Powerful search** across memory and ADRs

## Installation
1. Copy these command files to `~/.claude/commands/`.
2. Ensure Claude Code is configured to read custom commands from that directory.
3. Optional: version-control your `~/.claude` folder or just the `memory/` subtree in your project repo.

## Quick Start
```bash
/project:create-memory           # Initialize structured memory
/project:memory-auto on/off          # Enable/disable auto-update entries ( by default it is ON )
/project:load-memory             # View a concise status dashboard
```

## Command Index
- **create-memory.md**
  - Initializes `~/.claude/memory/memory.md` with a robust skeleton and folders:
    - `adr/`, `snapshots/`, `archive/`

- **load-memory.md**
  - Prints status: last updated, auto-update state, active goals, invariants, recent changes, ADRs.
  - Defines auto-update behavior (when ON) to append git-aware changelog entries after each answered request.

- **memory-auto.md**
  - Toggle or check automatic updates using `~/.claude/memory/.auto-update`.
  - Usage: `/project:memory-auto on|off|status`.

- **memory-update.md**
  - Structured updates to `memory.md` with a changelog entry (and optional section edits):
    - `goal:+ <text>` → add to Active
    - `goal:done <text>` → move to Done (dated)
    - `invariant:+ <text>` → add stable facts
    - `open:+ <question>` → add open questions
    - `decision:+ <title>` → create ADR and link
    - `convention:+ <rule>` → add/update conventions

- **memory-search.md**
  - Search across `memory.md` and `adr/*.md`, optionally by `section:`, with concise results.

- **memory-snapshot.md**
  - Create timestamped snapshot files in `memory/snapshots/` with optional git metadata.

- **memory-adr.md**
  - Create/update ADRs under `memory/adr/YYYYMMDD-slug.md`, and index them in `Decisions`.

- **memory-prune.md**
  - Non-destructive pruning/archiving (changelog, done goals) with dry-run and confirmation.

## The Memory File (`memory.md`)
Structured to stay readable over months of work:
- **Overview** — project name, scope, repo
- **Invariants** — pinned facts that rarely change
- **Goals** — Active, Upcoming, Done
- **Decisions (ADR Index)** — links to ADRs
- **Architecture** — context, constraints, modules, data, external services
- **Conventions** — styles, branching, directory layout
- **Environments** — dev/stage/prod specifics
- **Tooling** — build, test, CI; secrets referenced only
- **Open Questions** — unresolved items
- **Glossary**, **References**
- **Changelog** — compact, git-aware updates

## Typical Workflow
1. Initialize memory and turn on auto-update.
2. Work as usual; after each answered request, a small changelog entry is appended (if auto-update is ON).
3. Use `memory-update` to promote transient work into stable sections (Goals, Invariants, Conventions).
4. Capture decisions as ADRs; link from `Decisions`.
5. Create snapshots periodically and prune monthly to keep `memory.md` lean.

## Examples
```bash
# Add a change with directives
/project:memory-update Implement signup; goal:done Implement login; open:+ How to handle email verification?

# Search across memory + ADRs
/project:memory-search q:"database schema" context:2 limit:5

# Create an ADR
/project:memory-adr Choose Postgres status:accepted context:"Need transactions"

# Snapshot & Prune
/project:memory-snapshot
/project:memory-prune dry_run:true
```

## Design Principles
- **Concise, deterministic updates** — small stable entries beat verbose logs
- **Separation of concerns** — transient updates in Changelog; durable info in sections/ADRs
- **Never store secrets** — link to secret managers or env docs
- **Git context when available** — branch, commit, A/M/D counts
