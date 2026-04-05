---
name: onboard
trigger: /onboard
auto_trigger: session-start when memory/user_profile.md does not exist
description: Collect user profile, goals, and preferences. Suggest relevant skills. Run automatically for new users.
---

# Skill: onboard

## Purpose
Bootstrap the agent's understanding of who the user is so every subsequent interaction can be tailored to their role, experience level, and goals.

## Trigger
- Explicit: `/onboard`
- Automatic: `SessionStart` hook fires and `memory/user_profile.md` does not exist

## Steps

```
1. CHECK memory/user_profile.md
   - If file exists AND onboarded = true → skip to step 6 (returning user)
   - If file exists but onboarded = false → resume from last incomplete step

2. GREET
   Output: "Welcome! I'm your AI development partner built on Claude Code + Entire.
            I don't have a profile for you yet — mind if I ask 3 quick questions?
            (Takes ~30 seconds)"

3. ASK (AskUserQuestion — 3 questions, one message)
   Q1: "Which best describes you?"
       Options: student | professional dev | researcher | hobbyist
   Q2: "How would you rate your coding experience?"
       Options: beginner | intermediate | senior | expert
   Q3: "What's your main goal for this project?" [free text]

4. WRITE profile to memory/user_profile.md
   Fields: display_name, role, experience_level, goals[], onboarded=true, session_count=1

5. SCAN workspace
   - Glob **/* (top-level structure)
   - Read README if present
   - Read package.json / pyproject.toml / go.mod if present
   - Write summary to memory/project_context.md

6. SUMMARIZE
   Output: "Here's what I know about you and this project: [2–3 sentence summary]"

7. SUGGEST top 3 skills based on role + project state
   - student/beginner → explain, debug, scaffold
   - professional/senior → review, checkpoint, migrate
   - researcher → explain, testgen, docs
   - hobbyist → scaffold, debug, explain
   Output: "Recommended next steps: ..."

8. EXIT — hand control back to user
```

## Outputs
- `memory/user_profile.md` (created/updated)
- `memory/project_context.md` (created/updated)

## Guards
- **Never** re-ask questions that are already answered in the profile
- **Never** modify any source files during onboarding
- If user skips a question, record `null` for that field and proceed
