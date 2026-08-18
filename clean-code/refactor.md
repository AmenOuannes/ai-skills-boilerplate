# Refactor a piece of code

## What it does
Takes an existing function, class, or file and rewrites it to be more readable, maintainable, and idiomatic without changing its external behavior.

## When to use it
Use this skill when code works but is hard to read, review, extend, or test. Do not use it for behavior changes or large architectural rewrites.

## Inputs
- The code to refactor (inline or file path)
- The language/framework conventions to follow
- Any project-specific style rules the agent should respect

## Output
- Refactored code
- A short summary of what changed and why
- A diff-friendly before/after comparison when useful

## Steps

1. **Read and understand**
   - Identify the public interface and behavior.
   - Note side effects, inputs, outputs, and error paths.

2. **List concrete problems**
   - Long functions, deep nesting, unclear names, duplication, magic values, missing error handling, tight coupling, etc.

3. **Pick safe refactorings**
   - Rename variables/functions for clarity.
   - Extract helpers or small functions.
   - Reduce nesting using early returns or guard clauses.
   - Replace magic numbers/strings with named constants.
   - Remove dead code and unnecessary comments.
   - Improve error handling without changing behavior.

4. **Rewrite the code**
   - Keep the public signature and observable behavior unchanged unless explicitly asked.
   - Follow the project’s style and language idioms.
   - Make the smallest meaningful change that addresses the listed problems.

5. **Verify behavior preservation**
   - If tests exist, run them.
   - If no tests exist, add minimal tests for the current behavior before refactoring.

6. **Summarize**
   - Explain what was changed and why.
   - Highlight any trade-offs or follow-up work.

## Rules
- Never refactor and change behavior in the same pass.
- Do not optimize prematurely. Readability first.
- Keep the change reviewable; if a file is too large, refactor incrementally.
