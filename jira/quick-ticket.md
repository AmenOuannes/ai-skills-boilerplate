# Create a quick Jira ticket and start work

## What it does
Creates a minimal Jira ticket from a short description and immediately prepares the working context.

## When to use it
Use this skill for small, well-understood tasks where a full spec is unnecessary.

## Inputs
- Short task description
- Project key
- Issue type (default: Task)
- Optional assignee or sprint

## Output
- Created ticket with key and URL
- Local branch or worktree ready for work

## Steps

1. **Create the ticket**
   ```bash
   jira issue create \
     --project "<project-key>" \
     --issuetype "<type>" \
     --summary "<short summary>" \
     --body "<description>"
   ```

2. **Capture the issue key**
   - Parse the created issue key from the CLI output.

3. **Start the working context**
   - Create a branch named after the issue key.
   ```bash
   git checkout -b <issue-key>-<short-slug>
   ```

4. **Confirm**
   - Print the ticket URL and branch name.

## Rules
- Keep the description short but actionable.
- Use this only for changes that fit in one PR.
- If the task is large or ambiguous, use `ticket-to-spec.md` instead.
