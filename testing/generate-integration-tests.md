# Generate integration tests for a service or module

## What it does
Reads a service, module, or component with real dependencies and generates integration tests that verify interactions and data behavior.

## When to use it
Use this skill for code that touches a database, repositories, cross-service flows, or external clients with mocked boundaries.

## Inputs
- Source file path
- Dependency injection or fixture conventions
- External client interface to mock

## Output
- Integration test file with realistic setup and assertions

## Steps

1. **Read the source file**
   - Identify public methods, collaborators, and data flows.

2. **Read existing integration tests**
   - Match setup patterns, fixture usage, and assertion style.

3. **Identify the test boundary**
   - Real database and repositories when possible.
   - Mock external clients at the client interface, not internal logic.

4. **Plan test cases**
   - Success flows
   - Cross-service interactions
   - Error paths and specific exception types
   - Permission, tenant isolation, or authorization checks
   - State changes in the database

5. **Write the tests**
   - Use the project’s dependency container or fixture system.
   - Reset state between tests.
   - Name tests with `test_<action>_<context>_<expected>` if that convention exists.

6. **Run the tests**
   ```bash
   make test
   pytest path/to/test_file.py
   ```

7. **Fix failures**
   - Adjust fixtures, setup, or source code as needed.

8. **Summarize**
   - What flows are covered, what remains uncovered, and why.

## Rules
- Never mock repositories unless the project explicitly requires it.
- Keep each test independent.
- Prefer realistic data over minimal stubs.
- Integration tests should be slower than unit tests but still predictable.
