---
name: retrospective
trigger: /retro
auto_trigger: SessionEnd hook
description: End-of-session summary. Captures decisions, files changed, next steps. Saves persistent memory and creates checkpoint.
---

# Skill: retrospective

## Purpose
Close a session cleanly. Summarize what was accomplished, surface key decisions, generate a prioritized "next steps" list, and persist the important context to memory so the next session can hit the ground running.

## Trigger
- Explicit: `/retro`
- Automatic: `SessionEnd` hook fires

## Steps

```
1. READ session history
   a. Run: entire session log --current (or read .entire/logs/current)
   b. Run: git log --oneline --since="session start time"
   c. Read memory/project_context.md for baseline state at session start

2. SUMMARIZE session
   Structure:
   ┌─ SESSION SUMMARY ──────────────────────────────────────┐
   │ Duration: [start time] → [end time]                    │
   │                                                        │
   │ Files changed:                                         │
   │   • [file] — [brief description of change]             │
   │                                                        │
   │ Decisions made:                                        │
   │   • [decision] (rationale: [why])                      │
   │                                                        │
   │ Skills used: [list]                                    │
   │                                                        │
   │ Problems encountered:                                  │
   │   • [problem] → [resolution or status]                 │
   └────────────────────────────────────────────────────────┘

3. GENERATE next steps (prioritized)
   Format:
   NEXT SESSION — START HERE:
   1. [Most important next action] — [why it's first]
   2. [Second priority]
   3. [Optional / lower priority]

4. ASK
   "Should I save this summary to memory for next session?"
   Options: "Yes, save it all" | "Save next steps only" | "No thanks"
   
   IF yes (any variant):
   - APPEND to memory/project_context.md (timestamped section, never overwrite)
   - WRITE/OVERWRITE memory/next_steps.md (always current)

5. CREATE checkpoint (runs checkpoint skill inline)
   Label: "retro-[YYYY-MM-DD]" or "retro-[session-label]"
   Skip if user declines

6. CLOSE
   Output: "Session complete.
            Next time, I'll start with: [top next step]
            Checkpoint: [label] saved."
```

## Outputs
- Session summary printed to terminal
- `memory/project_context.md` updated (appended)
- `memory/next_steps.md` updated (overwritten with current list)
- Checkpoint created

## Guards
- **Never** delete prior memory entries — always append with ISO timestamp header
- **Never** auto-save without asking in step 4 (user may have sensitive notes)
- **Never** create a checkpoint with dirty working tree unless user explicitly approves commit
- IF session duration < 5 minutes: output abbreviated summary, skip checkpoint offer
