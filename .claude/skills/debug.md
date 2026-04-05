---
name: debug
trigger: /debug [error text | file | "it's broken"]
description: Systematic root-cause investigation. Generates ranked hypotheses, confirms with user, then fixes with user approval.
---

# Skill: debug

## Purpose
Replace "guess and check" debugging with a structured, hypothesis-driven workflow. The agent investigates before suggesting fixes, and always confirms the diagnosis with the user before touching code.

## Trigger
- Explicit: `/debug` (with or without additional context)
- With context: `/debug TypeError: Cannot read property 'id' of undefined`
- Vague: `/debug it's broken`

## Steps

```
1. COLLECT context
   a. IF error text provided: parse stack trace for file:line references
   b. IF no error text: ask "What's the symptom? Paste the error or describe what's wrong."
   c. READ the affected file(s) identified from stack trace or user description
   d. RUN: git diff HEAD~1 -- [affected files] (what changed most recently?)
   e. CHECK: git log --oneline -10 (recent commits that could be relevant)

2. HYPOTHESIZE
   Generate 1–3 root cause hypotheses, ranked by confidence:
   Format:
   Hypothesis 1 (HIGH confidence): [description]
     Evidence: [what in the code supports this]
     Location: [file:line]
   
   Hypothesis 2 (MEDIUM confidence): [description]
     Evidence: [...]
     Location: [...]

3. INVESTIGATE each hypothesis
   - Read surrounding code for the hypothesized location
   - Grep for related patterns that could confirm/deny
   - Check for known antipatterns (null dereference, off-by-one, async/await gaps, etc.)
   - Look for similar patterns elsewhere in the codebase (was this done correctly elsewhere?)

4. CONFIRM with user
   Output: "I believe the issue is [hypothesis 1] because [evidence].
            Specifically: [file]:[line] — [exact problem].
            Does this match what you're seeing? [Yes / No / Partially]"
   
   IF No or Partially:
   - Ask: "What's different from what I described?"
   - Iterate: read more context, refine hypothesis, re-confirm
   - Maximum 3 iterations before asking user to provide more information

5. FIX (only after user confirms hypothesis)
   - Enter plan mode
   - Show exact diff of proposed fix
   - Explain WHY the fix works, not just what it changes
   - Wait for user approval
   - Apply fix
   - Run tests if test runner is detected

6. POST-FIX
   - Verify fix resolves the symptom
   - ASK: "Want me to add a test that would have caught this bug?"
   - IF yes: run testgen skill inline for this specific case
   - Offer checkpoint: "Want to save a checkpoint now that the bug is fixed?"
```

## Outputs
- Root cause explanation with file:line citations
- Fix (plan mode, user-approved)
- Optional: regression test
- Optional: checkpoint

## Guards
- **Never** apply a fix without user confirmation of the hypothesis
- **Never** assume a fix works — always verify or run tests
- **Never** guess at a root cause without citing specific evidence in the code
- IF stack trace mentions external libraries: check if it's actually a user code bug first
