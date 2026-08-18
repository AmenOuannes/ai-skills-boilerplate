# Provide product context

## What it does
Loads and summarizes product knowledge so the AI has the right context before working on a feature, ticket, or spec.

## When to use it
Use this skill at the start of a task when the AI needs to understand the product, its users, key flows, terminology, or recent decisions.

## Inputs
- Product documentation location (folder, Notion link, wiki URL, or files)
- Optional topic or feature area to focus on
- Optional questions to answer

## Output
- A concise product context summary for the current task

## Steps

1. **Identify the product knowledge source**
   - Product README, wiki, Notion, PRDs, user research docs, decision logs, or a `product/` folder in the repo.

2. **Load relevant sections**
   - Product vision and goals
   - Target users and personas
   - Key user journeys
   - Domain terminology and definitions
   - Recent product decisions or constraints

3. **Filter by task relevance**
   - Focus on the topic or feature area at hand.
   - Skip unrelated history.

4. **Summarize the context**
   - Keep it short enough to fit in the agent context window.
   - Include only what changes how the task should be approached.

5. **Surface open questions**
   - Note anything ambiguous or missing.

## Output template

```markdown
## Product context

- **Product goal**: ...
- **Target users**: ...
- **Key journey**: ...
- **Relevant terminology**: ...
- **Constraints/decisions**: ...
- **Open questions**: ...
```

## Rules
- Do not hallucinate product facts.
- If sources are missing, ask the user for them.
- Keep summaries actionable, not historical essays.
- Update the knowledge source if the task reveals outdated information.
