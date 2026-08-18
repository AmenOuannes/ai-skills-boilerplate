# Pull a Jira ticket to start a spec

## What it does
Fetches a Jira ticket and converts its summary and description into a structured spec draft in Markdown.

## When to use it
Use this skill at the start of a feature or bug fix when the Jira ticket is the source of truth.

## Inputs
- Issue key (e.g., `PROJ-123`)
- Optional spec destination path

## Output
- A Markdown spec draft saved in the project’s specs directory.

## Steps

1. **Fetch the ticket**
   ```bash
   jira issue view <issue-key> --json
   ```

   Or via REST API:
   ```bash
   curl -H "Authorization: Bearer $JIRA_API_TOKEN" \
     --url "$JIRA_BASE_URL/rest/api/3/issue/<issue-key>?fields=summary,description,issuetype,labels,assignee,status"
   ```

2. **Extract the spec inputs**
   - Goal and scope
   - User-facing behavior
   - Acceptance criteria
   - Technical notes or constraints
   - Open questions

3. **Draft the spec document**

   Use this template:

   ```markdown
   # Spec: <ticket-summary>

   ## Source
   - Ticket: <issue-key>
   - URL: <jira-url>

   ## Goal
   <one-paragraph summary>

   ## Scope
   - In scope: ...
   - Out of scope: ...

   ## Acceptance criteria
   - [ ] ...
   - [ ] ...

   ## Technical notes
   - ...

   ## Open questions
   - ...
   ```

4. **Save the spec**
   - Write to `specs/<issue-key>.md` or the project’s preferred path.

5. **Confirm**
   - Print the spec path and a short summary.

## Rules
- Do not change the ticket’s meaning; rephrase for clarity only.
- Flag missing acceptance criteria explicitly.
- If the ticket is too vague, note open questions and ask the user for input.
