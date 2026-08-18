# Review a local PR

## What it does
Runs a focused code review on the current local PR using the GitHub CLI and the working branch diff.

## When to use it
Use this skill before asking for human review or before finalizing a PR.

## Inputs
- PR number, URL, or current branch
- Optional review focus (logic, readability, tests, security, performance)

## Output
- A Markdown review summary with inline-ready comments and top-level concerns.

## Steps

1. **Identify the PR**
   ```bash
   gh pr view --json number,title,headRefName,baseRefName,body,url
   ```

2. **Fetch the diff**
   ```bash
   gh pr diff <number>
   ```

3. **Read the PR context**
   - Title, description, linked issues, labels.

4. **Review the diff for**
   - Correctness against the PR description
   - Readability and maintainability
   - Missing tests or docs
   - Security red flags
   - Performance or scalability concerns
   - Consistency with project conventions

5. **Produce the review**
   - Summarize overall verdict: approve, comment, or request changes.
   - List specific findings grouped by file or theme.
   - Suggest inline comments in the format `file:line: suggestion`.

## Rules
- Be specific. Cite file paths and line numbers.
- Distinguish blockers from nitpicks.
- Do not rewrite code unless the separate fix-pr-reviews skill is used.
