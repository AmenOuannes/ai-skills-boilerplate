# Generate unit tests for a source file

## What it does
Reads a source file and generates focused unit tests that match the project’s testing conventions.

## When to use it
Use this skill for pure logic, models, validators, and utilities that have no database or external I/O dependency.

## Inputs
- Source file path
- Existing test file conventions
- Optional coverage gaps or missing line numbers

## Output
- Unit test file with one test per distinct behavior or edge case

## Steps

1. **Read the source file**
   - Identify public functions, classes, methods, validators, and edge cases.

2. **Read existing tests**
   - Find a similar test file in the same directory.
   - Match naming, imports, fixtures, and assertion style.

3. **List behaviors to test**
   - Happy path
   - Boundary values
   - Invalid inputs
   - Error cases
   - Branch conditions

4. **Write the tests**
   - One test per behavior.
   - Use the naming convention `test_<action>_<context>_<expected>` when available.
   - Avoid tests that only assert “does not crash.”

5. **Run the tests**
   ```bash
   # project-specific test command, e.g.:
   make test
   pytest path/to/test_file.py
   npm test
   ```

6. **Fix failures**
   - If the test reveals a bug in source code, fix it or flag it.

7. **Summarize**
   - What was covered, what was skipped, and why.

## Rules
- Do not mock internal collaborators unless necessary.
- Do not write integration-level tests here (no DB, no HTTP, no I/O).
- Keep tests fast (< 100ms each when possible).
- Each test must verify a distinct behavior.
