---
name: checkpoint
trigger: /checkpoint [label?]
description: Create a named Entire checkpoint + git tag. Safe, reversible snapshot of current state.
---

# Skill: checkpoint

## Purpose
Create a named, reversible snapshot of the current session state using both Entire's checkpoint system and a git tag. This is the "save game" of the development workflow.

## Trigger
- Explicit: `/checkpoint` or `/checkpoint my-label`
- Inline: called by `retrospective` and `guardrails` skills automatically

## Steps

```
1. VALIDATE working tree
   - Run: git status --short
   - IF dirty (uncommitted changes exist):
     a. ASK: "You have uncommitted changes. What would you like to do?"
        Option A: "Commit first, then checkpoint" (recommended)
        Option B: "Checkpoint memory/session state only (not code changes)"
        Option C: "Cancel"
     b. IF Option A: stage → prompt for commit message → commit → continue
     c. IF Option B: skip git tag, proceed with Entire checkpoint only
     d. IF Option C: abort with message "Checkpoint cancelled."

2. RESOLVE label
   - IF label provided by user: use as-is (sanitize: lowercase, hyphens only)
   - IF no label: generate "cp-YYYY-MM-DD-HHmm" from current timestamp

3. CREATE Entire checkpoint
   - Run: entire checkpoint create --label "[label]"
   - Capture: checkpoint ID from output

4. CREATE git tag (only if step 1 resulted in clean tree)
   - Run: git tag "checkpoint/[label]" HEAD
   - IF tag already exists: append "-v2", "-v3", etc.

5. RECORD in memory/checkpoints.md
   - Append entry: | [label] | [ISO timestamp] | [git SHA] | [Entire checkpoint ID] | [user note if any] |

6. CONFIRM to user
   Output: "Checkpoint '[label]' created.
            Git SHA: [short SHA]
            Entire ID: [id]
            Restore with: /rollback [label]"
```

## Outputs
- Entire checkpoint
- Git tag `checkpoint/[label]`
- Appended row in `memory/checkpoints.md`

## Guards
- **Never** force-push or overwrite existing tags — always version-suffix instead
- **Never** auto-commit without showing the user what will be staged
- **Never** delete uncommitted work
