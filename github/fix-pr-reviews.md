# Fix unresolved PR review comments

## What it does
Pulls a PR, reads unresolved review threads, proposes fixes for each, implements them, and replies to resolve the threads.

## When to use it
Use this skill when a PR has open review comments that need code changes.

## Inputs
- PR number or URL
- Optional constraints (what to change vs. defer)

## Output
- Implemented code changes
- Replies posted to resolved review threads
- A summary of what was done

## Steps

### Step 1: Pull the PR threads
Stop and ask the user to confirm before continuing.

```bash
gh pr view <number> --json number,title,headRefName,baseRefName,reviewThreads
```

```bash
gh api repos/{owner}/{repo}/pulls/<number>/comments --jq '.[] | select(.state == "PENDING" or .state == "ACTIVE") | {id, path, line, body, user}'
```

- Summarize the unresolved threads.
- Ask the user to confirm the scope of fixes.

### Step 2: Propose fixes
Stop and present the plan.

For each unresolved thread:
- Re-read the relevant file.
- Propose a concrete code change.
- Note any threads that should be deferred with a reason.

Present the plan as:

```markdown
| Thread | File | Proposed fix | Action |
|--------|------|--------------|--------|
| ...    | ...  | ...          | fix / defer / discuss |
```

Wait for user approval before implementing.

### Step 3: Implement fixes
Stop after applying changes and run checks.

- Apply the approved fixes.
- Add or update tests if needed.
- Run the project’s lint/tests/type checks.
- Stage and commit the changes.

```bash
# apply fixes
# run tests/lint
# git add / commit
```

### Step 4: Reply and resolve threads
Stop after posting replies.

For each addressed thread:
- Post a concise reply explaining the change.
- Mark the thread as resolved.

```bash
gh api repos/{owner}/{repo}/pulls/comments/<comment-id>/replies -f body="Fixed in <commit-sha>: <short explanation>"
```

### Step 5: Push and summarize
- Push the new commit.
- Provide a final summary of changes and resolved threads.

## Rules
- Never implement without user approval at each stop.
- If a review comment is ambiguous, ask for clarification instead of guessing.
- Do not resolve a thread unless the underlying concern is actually addressed.
- Keep replies short and tied to specific commits.
