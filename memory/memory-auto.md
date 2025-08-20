Toggle or check automatic memory updates.

Behavior:
- Stores state in `.claude/memory/.auto-update` with content `on` or `off`.

Usage:
- `/project:memory-auto on`     → enable auto-updates
- `/project:memory-auto off`    → disable auto-updates
- `/project:memory-auto status` → show current state

Steps:
1. Ensure `.claude/memory/` exists; suggest `/project:create-memory` if missing.
2. Parse $ARGUMENTS: `on|off|status` (default: status).
3. For `on|off`:
   - Write that value (lowercase) to `.claude/memory/.auto-update`
   - Confirm the new state
4. For `status`:
   - Read `.claude/memory/.auto-update`; default to `off` if file missing
   - Print concise status

Notes:
- `load-memory.md` and `memory-update.md` respect this flag.
- Auto-update should be conservative: only append stable, succinct changes.
