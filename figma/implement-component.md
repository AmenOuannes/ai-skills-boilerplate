# Implement a UI component from Figma

## What it does
Takes a Figma link and implements the corresponding UI component in the project’s component library.

## When to use it
Use this skill when a Figma design exists for a component that needs to be built or updated.

## Inputs
- Figma component or frame URL
- Project scope or target library path
- Tech stack (React, Vue, styling system, variants convention)

## Output
- Component source file
- Component story, spec, or usage example
- Optional Figma code-connect mapping file
- A short summary of what was implemented

## Steps

1. **Read the Figma design**
   - Use the Figma API or MCP to fetch the node.
   - Extract: component name, visual structure, states, variants, spacing, typography, colors.

2. **Present a summary to the user**
   - Proposed component name (PascalCase)
   - Variants (e.g., `intent: primary | secondary`, `size: sm | md | lg`)
   - Props (required vs optional)
   - Interactive states (hover, disabled, loading, focus)

3. **Confirm before proceeding**
   - Wait for user approval on name, variants, and props.

4. **Explore existing components**
   - Read 2–3 nearby components to follow naming, file structure, and export patterns.
   - Check for barrel files and story conventions.

5. **Plan the files**
   - Propose the component file, story/example file, and barrel export update.

6. **Implement the component**
   - Use the project’s styling system and variant convention.
   - Export variant types where applicable.
   - Use `forwardRef` for focusable/interactive elements.

7. **Add stories or examples**
   - Include one story per meaningful variant combination.

8. **Add Figma code-connect mapping (optional)**
   - If the project uses Figma Code Connect, create the mapping file next to the component.

9. **Validate**
   - Run lint, type checks, and format.
   - Open the story/example and compare against the Figma design if possible.

10. **Commit**
    - Stage the new files and commit with a conventional commit message.

## Rules
- Match the project’s existing component patterns.
- Do not hardcode design tokens if the project has a token system.
- Keep the component self-contained and reusable.
- Confirm each phase with the user before writing files.
