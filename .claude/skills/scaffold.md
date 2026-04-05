---
name: scaffold
trigger: /scaffold [type] [--module name?] [--lang language?]
description: Generate idiomatic boilerplate for a component, API, module, or test suite. Detects project stack automatically.
---

# Skill: scaffold

## Purpose
Generate production-quality boilerplate that follows the conventions already established in the project. Never dumps a generic template — always reads the existing codebase first to match style, naming, and structure.

## Trigger
- Explicit: `/scaffold api` | `/scaffold component` | `/scaffold module auth` | `/scaffold cli`
- Common types: `api`, `component`, `module`, `service`, `cli`, `worker`, `test`

## Steps

```
1. DETECT project stack (if not in memory/project_context.md)
   - Read package.json → detect Node.js framework (Express, Fastify, NestJS, etc.)
   - Read pyproject.toml / requirements.txt → detect Python framework (FastAPI, Flask, Django)
   - Read go.mod → Go
   - Read Cargo.toml → Rust
   - Glob **/*.tsx → React/Next.js
   - Glob **/*.vue → Vue
   - Write detected stack to memory/project_context.md

2. SCAN existing examples
   - Find 1–2 existing files of the same type (e.g., existing API routes if scaffolding an API)
   - Read them to extract: naming conventions, import patterns, error handling style, test patterns
   - Note: use EXISTING patterns, not generic templates

3. RESOLVE scaffold type and name
   - IF type ambiguous: ask user to clarify
   - IF --module name provided: use it; else derive from type ("authModule", "UserService", etc.)
   - IF --lang provided: use it; else use detected stack language

4. CHECK for conflicts
   - Glob for existing files that would be overwritten
   - IF conflict found:
     "These files already exist: [list]
      Options: a) Overwrite  b) Add suffix (e.g., auth-v2)  c) Cancel"
   - (See Sequence N5 for repeat-scaffold detection)

5. DETECT idempotent-scaffold abuse
   - Check memory for recent scaffold calls (same type, < 5 minutes ago)
   - IF detected: "You scaffolded [type] [N] minutes ago. The previous output is at [path].
     Did you want to iterate on that, or start fresh?"

6. GENERATE scaffold
   Files to generate depend on type:
   
   API (Node.js/Express example):
   - src/routes/[module].routes.ts     (route definitions)
   - src/controllers/[module].ctrl.ts  (handler functions)
   - src/services/[module].service.ts  (business logic)
   - src/models/[module].model.ts      (data model/schema)
   - tests/[module].test.ts            (test stubs)
   
   Component (React example):
   - src/components/[Module]/index.tsx
   - src/components/[Module]/[Module].tsx
   - src/components/[Module]/[Module].test.tsx
   - src/components/[Module]/[Module].module.css
   
   Python API (FastAPI example):
   - app/routers/[module].py
   - app/schemas/[module].py
   - app/services/[module].py
   - tests/test_[module].py

7. SHOW what will be created (before writing)
   Output:
   "I'll create these files:
   • [file 1] — [description]
   • [file 2] — [description]
   ...
   Generate? [Yes / No / Customize]"

8. WRITE files (after user confirms)

9. SUMMARIZE
   Output:
   "Scaffold complete. Key files:
   • [main file] — start here
   • [test file] — run with [test command]
   Next: /explain [main file] for a walkthrough"
```

## Outputs
- Generated source files (matching project conventions)
- Generated test stubs

## Guards
- **Never** write files before showing what will be created (step 7)
- **Never** overwrite existing files without user confirmation
- **Never** use generic templates when existing examples are available to learn from
- **Never** scaffold without first reading at least one existing file of the same type
