---
name: review
trigger: /review [--against <branch>?]
description: Structured code review of the current diff. Classifies findings as CRITICAL / WARNING / SUGGESTION / POSITIVE.
---

# Skill: review

## Purpose
Perform a thorough, structured code review of the current branch's diff. Surface security issues, logic errors, missing tests, and style problems — prioritized so the developer knows what must be fixed vs. what's optional.

## Trigger
- Explicit: `/review` or `/review --against main`
- Default base branch: `main` (or detected default branch)

## Steps

```
1. DETECT base branch
   - IF --against flag provided: use that branch
   - ELSE: git symbolic-ref refs/remotes/origin/HEAD → extract branch name
   - Fallback: ask user "Compare against which branch? [main / master / other]"

2. COLLECT diff
   - Run: git diff [base]...HEAD
   - Run: git log [base]...HEAD --oneline
   - IF diff is empty: output "No changes detected vs [base]. Nothing to review." and EXIT

3. ANALYZE (Claude reads diff and classifies findings)
   Checklist:
   - OWASP Top 10: injection, broken auth, XSS, insecure deserialization, etc.
   - Logic errors: off-by-one, null dereference, unhandled promise rejections
   - Missing tests: new functions/routes with 0 test coverage
   - Dead code: imports, variables, functions added but never used
   - Style/naming: inconsistencies with surrounding code conventions
   - Performance: N+1 queries, missing indices, synchronous blocking calls
   - Documentation: exported public APIs with no docstrings

4. STRUCTURE output
   Format:
   ┌─ CRITICAL (block merge) ────────────────────────────┐
   │ [file]:[line] — [issue]                              │
   │   Risk: [why this matters]                           │
   └──────────────────────────────────────────────────────┘
   ┌─ WARNINGS (should fix) ─────────────────────────────┐
   │ ...                                                  │
   └──────────────────────────────────────────────────────┘
   ┌─ SUGGESTIONS (nice to have) ────────────────────────┐
   │ ...                                                  │
   └──────────────────────────────────────────────────────┘
   ┌─ POSITIVES ─────────────────────────────────────────┐
   │ ...                                                  │
   └──────────────────────────────────────────────────────┘

5. ASK
   "Would you like me to fix any of the CRITICAL or WARNING items?"
   Options: "Yes, fix all CRITICAL" | "Let me choose" | "No, just the report"

6. IF fix requested:
   - Enter plan mode
   - Show exact diffs for each proposed fix
   - Wait for user approval before applying
   - After applying: run tests if test runner detected
   - Create checkpoint with label "post-review-fixes"
```

## Outputs
- Structured review report printed to terminal
- Optional: fixes applied (only after user approval in plan mode)
- Optional: checkpoint `post-review-fixes`

## Guards
- **Never** auto-commit review fixes
- **Never** modify files before showing plan
- **Never** claim a file is insecure without citing the specific line and pattern
- If diff > 2000 lines: warn user and ask whether to review all or select files
