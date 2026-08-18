# Implement from a spec

## What it does
Reads an approved spec and implements the change incrementally, keeping the work aligned with the acceptance criteria.

## When to use it
Use this skill when a spec exists and the implementation phase begins.

## Inputs
- Spec file path
- Optional ticket/issue key
- Existing codebase context

## Output
- Working code that satisfies the spec
- Commits with clear messages
- A short summary of what was implemented

## Steps

1. **Read the spec**
   - Goal, scope, acceptance criteria, technical approach, risks.
   - Note any linked architecture doc (e.g., from `clean-code/design.md`).

2. **Explore the codebase**
   - Identify the files and components the spec touches.
   - Look for existing patterns to follow.

3. **Plan the implementation order**
   - Break the spec into small, reviewable steps.
   - Start with tests or scaffolding when it makes sense.

4. **Implement incrementally**
   - Make one logical change at a time.
   - Run tests, lint, and type checks after each step.
   - Commit each meaningful step.

5. **Verify against acceptance criteria**
   - Check each criterion from the spec.
   - Add or update tests to prove the criteria are met.

6. **Review the diff**
   - Run a self-review for readability, edge cases, and spec alignment.
   - Use `clean-code/security.md` for a quick security pass.

7. **Summarize**
   - List what was done, what changed, and what remains.

## Rules
- Never drift from the spec scope. If the spec is wrong or incomplete, stop and update the spec first.
- Prefer small commits over one large commit.
- Keep the implementation reviewable.
