# Pull a GitHub issue to start a spec

## What it does
Fetches a GitHub issue and converts its description into a structured spec draft in Markdown.

## When to use it
Use this skill at the start of a feature or bug fix when the issue is the source of truth.

## Inputs
- Issue number or URL
- Optional spec destination path

## Output
- A Markdown spec draft saved in the project’s specs directory.

## Steps

1. **Fetch the issue**
   ```bash
   gh issue view <number> --json number,title,body,labels,assignees,milestone,url,state
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
   # Spec: <issue-title>

   ## Source
   - Issue: <url>

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
   - Write to `specs/<issue-number>-<slug>.md` or the project’s preferred path.

5. **Confirm**
   - Print the spec path and a short summary.

## Rules
- Do not change the issue’s meaning; rephrase for clarity only.
- Flag missing acceptance criteria explicitly.
- If the issue is too vague, note open questions and ask the user for input.
