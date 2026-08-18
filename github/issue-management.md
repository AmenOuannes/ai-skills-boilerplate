# Manage GitHub issues

## What it does
Creates, closes, reopens, or updates GitHub issues using the GitHub CLI.

## When to use it
Use this skill to track work, follow up on PRs, close stale issues, or prepare tasks from a spec or bug report.

## Inputs
- Repository context (current repo or explicit owner/repo)
- Action: create, close, reopen, or update
- Issue title, body, labels, assignees, milestone

## Output
- Confirmation of the action taken and a link to the issue.

## Steps

1. **Determine the repo**
   ```bash
   gh repo view --json owner,name
   ```

2. **Run the chosen action**

   **Create**
   ```bash
   gh issue create --title "<title>" --body "<body>" --label "<label>" --assignee "<user>"
   ```

   **Close**
   ```bash
   gh issue close <number>
   ```

   **Reopen**
   ```bash
   gh issue reopen <number>
   ```

   **Update**
   ```bash
   gh issue edit <number> --title "<title>" --body "<body>" --add-label "<label>"
   ```

3. **Confirm**
   - Print the issue URL and a short summary of the action.

## Rules
- Always confirm destructive actions (close, reopen) with the user first.
- Use labels consistently with the project’s existing taxonomy.
- When creating from a spec or bug report, keep the body focused and actionable.
