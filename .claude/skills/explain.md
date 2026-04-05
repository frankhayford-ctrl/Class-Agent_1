---
name: explain
trigger: /explain [file | function | concept]
description: Deep-explain a file, function, or concept. Adapts depth and style to user's experience level from their profile.
---

# Skill: explain

## Purpose
Provide a thorough, tailored explanation of any code artifact or concept. The explanation style adapts automatically based on the user's `experience_level` in their profile.

## Trigger
- Explicit: `/explain auth/middleware.ts` or `/explain BPE tokenization` or `/explain getUser`

## Steps

```
1. RESOLVE target type
   - Check if argument matches a file path (Glob search)
   - Check if argument matches a function/class name (Grep search)
   - Otherwise: treat as a concept

2a. IF file/function target:
   a. READ target file(s) fully
   b. TRACE call graph:
      - Grep for all usages of the target in the codebase
      - Grep for all imports of the target file
      - Identify what the target calls (outbound dependencies)
   c. FIND tests:
      - Glob **/test*/**/*[target]* and **/__tests__/**
      - Note which behaviors are tested vs. untested
   d. CHECK memory for prior explanations of this target
      (avoid repeating explanations already given this session)

2b. IF concept target:
   a. Grep codebase for related terms
   b. Check if the concept is implemented locally or just referenced
   c. Use Claude's knowledge to explain the concept in the context of this codebase

3. LOAD user experience level from memory/user_profile.md
   - IF no profile: default to "intermediate"

4. GENERATE explanation tailored to experience level:
   BEGINNER:
   - Start with a plain-English analogy
   - Walk through the code line by line for key sections
   - Avoid jargon; define terms when introduced
   - Use "think of it like..." framing

   INTERMEDIATE:
   - Focus on the pattern used (e.g., "this is a middleware chain")
   - Explain trade-offs vs. alternatives
   - Point out non-obvious behaviors and edge cases

   SENIOR/EXPERT:
   - Lead with architecture and design decisions
   - Discuss performance characteristics (complexity, I/O, memory)
   - Surface known limitations and potential failure modes
   - Reference relevant papers, specs, or prior art if applicable

5. HANDLE missing target gracefully
   - IF Glob/Grep finds no match:
     Output: "I couldn't find [target] in this project.
              Closest matches: [list up to 3 similar names]
              Did you mean one of these, or is [target] a file you're planning to create?"
   - NEVER fabricate an explanation for a nonexistent file or function

6. OFFER follow-up actions
   "Want me to:
   a) Add inline comments to this file?
   b) Generate tests for the untested paths?
   c) Draw an ASCII diagram of the call graph?
   d) Explain a specific part in more depth?"
```

## Outputs
- Explanation text in terminal
- Optional (user-requested): annotated file, generated tests, ASCII diagram

## Guards
- **Never** modify files unless user explicitly requests it in step 6
- **Never** fabricate explanations for nonexistent targets
- **Never** repeat a full explanation that was already given this session (summarize and offer to go deeper)
