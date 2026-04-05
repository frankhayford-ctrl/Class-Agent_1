---
name: docs
trigger: /docs [target | --update | --readme]
description: Generate or update documentation for a file, function, module, or the project README. Matches existing doc style.
---

# Skill: docs

## Purpose
Generate documentation that actually helps readers — not just restated function signatures, but explanations of WHY, edge cases, and usage examples. Reads existing docs first to match style.

## Trigger
- Explicit: `/docs src/auth/middleware.ts`
- README: `/docs --readme`
- Update existing: `/docs --update` (scan for stale/missing docs)
- Function: `/docs validateUser`

## Steps

```
1. DETECT documentation style
   - Glob **/*.md → check for existing README, CONTRIBUTING, API docs
   - Read 1–2 existing docstrings/JSDoc/docblocks to learn style
   - Detect format: JSDoc | TSDoc | Python docstrings | Go doc comments | Markdown

2. RESOLVE target
   a. IF file path: read full file, identify all exported/public symbols
   b. IF function name: grep for definition, read containing file
   c. IF --readme: read entire project structure + existing README
   d. IF --update: scan for public symbols with missing or stale docs

3. ASSESS what's missing
   For --update or --readme mode:
   - List: public functions/classes/routes with no docs
   - List: docs that reference nonexistent parameters or outdated behavior
   Output:
   "Found [N] undocumented symbols and [M] stale doc entries.
    Generate all? [Yes / Select / Cancel]"

4. GENERATE documentation
   For each function/class/module:
   - Summary: one sentence, plain English, explains PURPOSE not just name
   - Parameters: name, type, description, whether optional
   - Returns: type + what it means
   - Throws/raises: what errors and under what conditions
   - Example: concrete usage code snippet
   - Notes: gotchas, performance notes, deprecation warnings if applicable
   
   For README:
   ┌─ README structure ─────────────────────────────────────┐
   │ # [Project name]                                       │
   │ [One-sentence description]                             │
   │                                                        │
   │ ## Quick Start                                         │
   │ [Install + run in < 5 steps]                           │
   │                                                        │
   │ ## Features                                            │
   │ ## Configuration                                       │
   │ ## API Reference (link or inline)                      │
   │ ## Development                                         │
   │ ## License                                             │
   └────────────────────────────────────────────────────────┘

5. SHOW generated docs to user
   "Here's what I'll add/update: [preview]
    Apply? [Yes / Adjust / Cancel]"

6. WRITE
   - Inline docs: edit source files to add docstrings/JSDoc
   - README: write/overwrite README.md
   - API docs: write to docs/ directory if it exists

7. CONFIRM
   Output: "Documentation updated. [N] symbols documented, [M] stale entries updated."
```

## Outputs
- Updated source files with inline documentation
- Updated README.md (if --readme)
- API documentation files (if docs/ directory exists)

## Guards
- **Never** write documentation that just restates the function name in prose
  BAD: "getUserById — gets a user by ID"
  GOOD: "getUserById — Fetches a single user record from the database. Returns null if the user does not exist; throws DatabaseError if the connection fails."
- **Never** write docs without reading the source first
- **Never** overwrite existing docs without showing a diff
- IF user's experience_level is beginner: add more examples and plain-English notes
- IF user's experience_level is expert: keep docs concise, focus on non-obvious behavior
