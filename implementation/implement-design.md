# Implement a design

## What it does
Takes a design document, Figma link, or design spec and implements it end to end as code.

## When to use it
Use this skill when the design phase is done and the implementation phase begins. This includes UI components, pages, API contracts, or system designs.

## Inputs
- Design source: Figma URL, Markdown design doc, architecture diagram, or spec
- Target tech stack and project conventions
- Optional scope boundaries

## Output
- Implemented code matching the design
- Tests or stories/examples where appropriate
- A summary of deviations or open questions

## Steps

1. **Read the design**
   - Parse the design source.
   - Identify visual structure, interactions, data flow, states, and edge cases.

2. **Confirm scope**
   - List what will be built, what is out of scope, and what needs clarification.

3. **Explore the codebase**
   - Find the right location for the new code.
   - Read similar existing implementations to follow conventions.

4. **Plan the implementation**
   - Break the design into files and components.
   - Note dependencies on existing systems, APIs, or components.

5. **Build incrementally**
   - Implement one logical piece at a time.
   - Run lint, type checks, and relevant tests after each step.

6. **Validate against the design**
   - Compare the output with the source design.
   - Flag any deviations and the reason for them.

7. **Summarize**
   - What was implemented, what changed, what remains.

## Rules
- Do not change the design intent without explicit approval.
- Keep the implementation reviewable; avoid oversized changes.
- Reuse existing components, hooks, or utilities when available.
- Run the project’s checks before considering the work done.
