---
argument-hint: []
description: Generate a PR description following the Scout/Forra template with title,
  optional ticket number, problem, solution, and notes
---

Generate a pull request description for the current changes. Ask the user for a ticket number if one is not obvious from the branch name or context. Always output the result inside a Markdown code block.

## Output format

```markdown
# [TICKET-123] <Title in imperative mood>

## 📖 Description

- <one-line summary>
- <second concise bullet if needed>

## ⚠️ Problem

- <problem we are solving>
- <second bullet if needed>

## 🤓 Solution

- <what changed>
- <why this is the best solution>
- <additional change>

## 🗒 Note

- <anything else worth mentioning>
```

## Rules

1. **Title**: Include the ticket number if available. If not provided or obvious, ask the user: "What is the ticket number for this PR?" before generating.
2. **Description**: Short, concise bullet points. Skip the section only if truly empty.
3. **Problem**: Skip the section if there is no real problem to describe (e.g., pure feature addition without a bug).
4. **Solution**: Mandatory. Explain what changed and why. Use bullet points.
5. **Note**: Optional. Use for follow-ups, risks, nice-to-haves, or things that need reviewer attention. Keep it short.
6. Always produce the final output inside a Markdown code block so the user can copy it directly.

## Context gathering

Before writing, inspect the current branch and recent changes to understand what the PR does. Use `git diff --stat` and key file reads as needed.
