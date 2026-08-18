# Write an implementation spec

## What it does
Takes a ticket, feature request, or brief description and writes a focused Markdown implementation spec.

## When to use it
Use this skill before implementation begins, when the work needs clarity, acceptance criteria, and a technical plan.

## Inputs
- Source: ticket key/URL, issue description, or user prompt
- Project context: language, frameworks, existing patterns
- Optional constraints: scope, timeline, dependencies

## Output
- A Markdown spec file ready for review and implementation.

## Steps

1. **Capture the source**
   - Record the issue/ticket link and the original request.

2. **Define the goal**
   - Write one paragraph explaining what success looks like.

3. **Set the scope**
   - In scope
   - Out of scope
   - Assumptions

4. **List acceptance criteria**
   - Use checkboxes.
   - Make each criterion testable or observable.

5. **Describe the technical approach**
   - High-level design decisions
   - Components or files likely to change
   - Data model or API surface if relevant

6. **Identify risks and dependencies**
   - What could block this?
   - What needs to happen before or after?

7. **Link architecture if needed**
   - If the spec needs a modular architecture, use [`clean-code/design.md`](../clean-code/design.md) to produce a separate architecture doc and reference it here.
   - Do not mix deep architecture into the spec itself.

8. **Draft the spec file**

## Output template

```markdown
# Spec: <title>

## Source
- <ticket/issue URL or user request>

## Goal
<one-paragraph summary>

## Scope

### In scope
- ...

### Out of scope
- ...

### Assumptions
- ...

## Acceptance criteria
- [ ] ...
- [ ] ...

## Technical approach
- ...

## Risks and dependencies
- ...
```

## Rules
- Keep the spec focused enough to fit in one PR when possible.
- Do not include implementation code.
- If the source is vague, note open questions rather than invent scope.
