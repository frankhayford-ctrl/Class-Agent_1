---
name: migrate
trigger: /migrate [from] [to]
description: Batch migration workflow. Dry-run first, shows full diff, applies only after user approval. Supports library swaps, API changes, naming conventions, and framework migrations.
---

# Skill: migrate

## Purpose
Perform safe, reviewable batch migrations across a codebase. Every migration runs as a dry-run first — the user sees the complete diff before a single file is touched.

## Trigger
- Explicit: `/migrate lodash native` | `/migrate fetch axios` | `/migrate snake_case camelCase` | `/migrate react vue`
- General: `/migrate [description]`

## Steps

```
1. PARSE migration intent
   - Extract: FROM pattern/library/convention, TO target
   - Classify migration type:
     a. Library swap (lodash → native, moment → dayjs)
     b. API/syntax change (fetch → axios, callbacks → async/await)
     c. Naming convention (snake_case → camelCase, PascalCase → kebab-case)
     d. Framework migration (React → Vue, Express → Fastify)
     e. Language upgrade (Python 2 → 3, JS → TS)
   
   IF intent is ambiguous: ask "What exactly should change? From [X] to [Y]?"

2. SCOPE the migration
   - Grep for all occurrences of FROM pattern
   - Count: files affected, total occurrences
   - Output:
     "Migration scope: [N] occurrences across [M] files.
      Files: [list]"
   
   IF scope > 20 files: warn "This is a large migration. Consider migrating file-by-file."
   IF scope = 0: "Pattern '[from]' not found in codebase. Nothing to migrate."

3. DRY RUN — generate diff without writing anything
   For each occurrence:
   - Compute the exact replacement
   - Accumulate as a unified diff

4. SHOW full diff to user
   Output:
   "Here's what will change (dry run — nothing written yet):
   [full unified diff]
   
   [N] files, [M] changes total.
   Proceed with migration? [Yes / No / Migrate specific files only]"

5. IF "Migrate specific files only":
   - Show file list, let user select subset
   - Re-show diff for selected files only
   - Re-confirm

6. CHECKPOINT (before applying)
   - Auto-run checkpoint skill: label "pre-migrate-[from]-to-[to]"

7. APPLY migration
   - Write changes file by file
   - Report progress: "[N/M] files migrated..."

8. POST-MIGRATION checks
   - IF test runner detected: run tests and report results
   - IF linter detected: run linter and report any new errors
   - Report:
     "Migration complete.
      ✓ [N] files updated
      [test results if run]
      [lint results if run]"

9. ASK
   "Want me to update any documentation or comments that still reference '[from]'?"
```

## Outputs
- Dry-run diff (always shown before writing)
- Updated source files
- Test/lint results
- Checkpoint before migration
- Optional: documentation updates

## Guards
- **Never** write files without showing full dry-run diff first
- **Never** apply migration without user confirmation
- **Always** create a checkpoint before applying (enables /rollback if migration causes issues)
- IF migration affects test files: warn separately "This also affects [N] test files. Include them?"
- Framework migrations (React → Vue, etc.): always warn "Framework migrations are complex. I'll migrate incrementally and we'll review each component. This may take multiple sessions."
