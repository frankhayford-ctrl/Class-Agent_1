---
name: testgen
trigger: /testgen [file | function | --coverage]
description: Generate unit and integration tests for a target file or function. Reads existing tests to match framework, style, and naming. Prioritizes untested paths.
---

# Skill: testgen

## Purpose
Generate meaningful, non-trivial tests that actually catch bugs — not just happy-path stubs that give false coverage confidence. Reads existing tests to match the project's testing conventions exactly.

## Trigger
- Explicit: `/testgen src/auth/middleware.ts`
- Function-level: `/testgen getUser`
- Coverage-driven: `/testgen --coverage` (find and fill gaps)

## Steps

```
1. DETECT test framework
   - Read package.json → jest, vitest, mocha, jasmine, pytest, go test, etc.
   - Glob **/jest.config.* | **/pytest.ini | **/vitest.config.*
   - Read 1–2 existing test files to learn: describe/it style, assertion style, mocking approach, file naming pattern

2. RESOLVE target
   a. IF file path: read the full file
   b. IF function name: grep for definition, read containing file
   c. IF --coverage mode:
      - Run test coverage report: [jest --coverage | pytest --cov | go test -cover]
      - Parse output to find uncovered functions/branches
      - Prioritize: public functions > private, critical paths > edge cases

3. ANALYZE the target for testable behaviors
   For each function/method/route:
   - Happy path: normal valid input → expected output
   - Edge cases: empty input, null/undefined, zero values, max values
   - Error paths: invalid input, missing dependencies, exception handling
   - Async behavior: promise rejection, timeout, concurrent calls
   - Security paths: injection attempts, auth bypass, permission checks (if applicable)
   
   Output:
   "I identified [N] behaviors to test in [target]:
   ✓ Happy path: [description]
   ✓ Edge case: [description]
   ✓ Error path: [description]
   [N more...]
   Generate tests for all, or select specific behaviors?"

4. GENERATE tests
   - Match existing test file naming: [file].test.ts | test_[file].py | [file]_test.go
   - Use SAME assertion style as existing tests (expect/assert/should)
   - Use SAME mock/stub patterns as existing tests
   - Each test: one behavior, one assertion (or tight grouping)
   - Include descriptive test names: "returns 404 when user not found"

5. SHOW generated tests to user
   Output: full test file content
   "Does this look right? [Yes / Adjust / Cancel]"
   
   IF Adjust: ask what to change, regenerate

6. WRITE test file
   - IF test file already exists: offer to append vs. overwrite
   - Write file
   
7. VERIFY (run the new tests)
   - Run: [test command] [test file]
   - IF all pass: "All [N] tests pass."
   - IF some fail:
     "Tests [X, Y] are failing. This is expected if the functionality has bugs.
      Would you like to fix the implementation or mark these tests as known-failing?"
```

## Outputs
- Generated test file (matching project conventions)
- Test run results

## Guards
- **Never** generate tests that only assert "it doesn't throw" — tests must assert specific behavior
- **Never** write tests before showing them to the user
- **Never** mock things that don't need mocking (e.g., don't mock pure functions)
- IF coverage mode reveals > 50% uncovered: warn "This file has very low coverage. I'll prioritize the most critical paths. Full coverage may take multiple sessions."
