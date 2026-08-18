# Manage Jira tickets

## What it does
Creates, closes, reopens, or updates Jira tickets using the Jira REST API or a configured MCP server.

## When to use it
Use this skill to track work, follow up on reviews, close stale tickets, or prepare tasks from a spec or bug report.

## Inputs
- Jira project key
- Action: create, close, reopen, or update
- Ticket summary, description, issue type, labels, assignee, sprint, epic link

## Output
- Confirmation of the action taken and a link to the ticket.

## Steps

1. **Determine project context**
   - Read the project key from the environment, user input, or `jira.project` config.

2. **Run the chosen action**

   **Create**
   ```bash
   jira issue create \
     --project "<project-key>" \
     --issuetype "<type>" \
     --summary "<summary>" \
     --body "<description>"
   ```

   Or via REST API:
   ```bash
   curl -X POST \
     -H "Authorization: Bearer $JIRA_API_TOKEN" \
     -H "Content-Type: application/json" \
     --url "$JIRA_BASE_URL/rest/api/3/issue" \
     -d '{
       "fields": {
         "project": {"key": "<project-key>"},
         "summary": "<summary>",
         "description": {"type": "doc", "version": 1, "content": [...]},
         "issuetype": {"name": "<type>"}
       }
     }'
   ```

   **Close / Done**
   ```bash
   jira issue transition <issue-key> --status "Done"
   ```

   **Reopen**
   ```bash
   jira issue transition <issue-key> --status "To Do"
   ```

   **Update**
   ```bash
   jira issue edit <issue-key> --summary "<summary>" --body "<description>"
   ```

3. **Confirm**
   - Print the ticket URL and a short summary of the action.

## Rules
- Always confirm destructive transitions (close, reopen) with the user first.
- Use issue types and labels consistently with the project’s taxonomy.
- When creating from a spec or bug report, keep the description focused and actionable.
- If the Jira CLI or MCP is not available, fall back to the REST API using environment tokens.
