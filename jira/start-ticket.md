# Start work from a Jira ticket

## What it does
Fetches a Jira ticket, creates a branch or worktree, and sets up the working context so implementation can begin.

## When to use it
Use this skill when you want to begin implementation from an existing ticket.

## Inputs
- Jira issue key
- Preferred branch naming convention
- Whether to use a worktree or a normal branch

## Output
- Fetched ticket summary
- New branch or worktree
- A brief implementation checklist

## Steps

1. **Fetch the ticket**
   ```bash
   jira issue view <issue-key> --json
   ```

2. **Summarize the ticket**
   - Title, description, acceptance criteria, status, linked issues.

3. **Create the working branch**
   ```bash
   git checkout -b <issue-key>-<short-slug>
   ```

   Or create a worktree:
   ```bash
   git worktree add ../<issue-key>-<short-slug>
   ```

4. **Prepare a checklist**
   - List acceptance criteria as checkboxes.
   - Note any prerequisites (spec, design, dependencies).

5. **Confirm**
   - Print the branch/worktree path, issue URL, and checklist.

## Rules
- If the ticket lacks acceptance criteria, create placeholders and flag them to the user.
- Do not start coding until the context is confirmed.
- Prefer worktrees when working across multiple tickets at once.
