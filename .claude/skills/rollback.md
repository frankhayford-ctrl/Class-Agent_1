---
name: rollback
trigger: /rollback [checkpoint-name?]
description: Restore workspace to a named Entire checkpoint. Always stashes current work first — nothing is ever discarded without explicit user consent.
---

# Skill: rollback

## Purpose
Safely restore the workspace to a previously saved checkpoint. The skill is conservative by design: it never discards uncommitted work without explicit permission.

## Trigger
- Explicit: `/rollback` or `/rollback my-checkpoint-label`

## Steps

```
1. LOAD available checkpoints
   Sources (merged and deduplicated):
   a. entire checkpoint list (run the command)
   b. git tag -l "checkpoint/*"
   c. memory/checkpoints.md (may have labels for Entire IDs)
   
   IF no checkpoints found:
   Output: "No checkpoints found. Create one with /checkpoint."
   EXIT

2. IF no label provided by user:
   Display checkpoint list:
   ┌─ AVAILABLE CHECKPOINTS ─────────────────────────────────┐
   │ # │ Label            │ Date             │ Git SHA        │
   │ 1 │ pre-auth-refactor│ 2024-01-15 14:23 │ a3f2c81        │
   │ 2 │ retro-2024-01-14 │ 2024-01-14 17:00 │ 8d91e44        │
   │ 3 │ cp-2024-01-13    │ 2024-01-13 09:15 │ 2b67f23        │
   └──────────────────────────────────────────────────────────┘
   ASK: "Which checkpoint would you like to restore?"

3. CONFIRM with user
   Output:
   "Rolling back to '[label]' will:
    • Restore all files to their state at [timestamp] (SHA: [short SHA])
    • Your current uncommitted changes will be STASHED (not deleted)
    
    Continue? [Yes / No]"
   
   IF No: abort, output "Rollback cancelled."

4. STASH current work (if any uncommitted changes)
   Run: git stash push -m "before-rollback-to-[label]-[timestamp]"
   IF nothing to stash: skip this step

5. RESTORE via Entire
   Run: entire checkpoint restore [checkpoint-id]

6. RESTORE via git (align code to checkpoint SHA)
   Run: git checkout [checkpoint-tag] -- .
   OR: git reset --hard [SHA] (only if user confirmed hard reset in step 3)

7. VERIFY
   Run: git diff [checkpoint-sha]...HEAD
   IF diff is empty: "Restore successful — workspace matches checkpoint."
   IF diff not empty: "Note: [N] files differ from checkpoint. This may be expected if the checkpoint was memory-only."

8. ASK about stashed work (if step 4 ran)
   Output:
   "Your work before the rollback is safely stashed as: 'before-rollback-to-[label]-[timestamp]'
   
   Would you like to:
   a) Keep the stash (recover it later with git stash pop)
   b) Discard the stash (cannot be undone)
   c) Show me what was stashed"
   
   IF b (discard): require explicit confirmation "Are you sure? This cannot be undone."
```

## Outputs
- Workspace restored to checkpoint state
- Stash of pre-rollback work (preserved unless user explicitly discards)
- Verification diff

## Guards
- **Never** discard uncommitted work — always stash first (step 4 is mandatory)
- **Never** use `git reset --hard` without calling it out explicitly in step 3
- **Never** overwrite `.claude/` or `.entire/` directories during rollback
- IF Entire and git SHA are misaligned (Entire restore succeeds but git tag missing): warn user and restore git state manually
