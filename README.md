# 🧰 ai-skills-kit

A collection of reusable AI skill files designed to plug into any project.
Stop rewriting the same prompts and workflows — clone once, use everywhere.

---

## What's inside

| Category              | Description                                                   |
|-----------------------|---------------------------------------------------------------|
| `clean-code/`         | Skills for readable, maintainable, production-quality code   |
| `github/`             | PR reviews, unresolved comment fixes, issue and CI workflows  |
| `jira/`               | Ticket creation, intake, estimation, sprint planning          |
| `figma/`              | Implement UI components and pages from Figma designs         |
| `specs/`              | Feature specs, implementation plans, API and component specs |
| `implementation/`     | Execute a committed spec or scoped change safely             |
| `testing/`            | Unit tests, E2E triage, coverage maps, test strategy           |
| `observability/`      | Sentry triage, alarm review, incident investigation             |
| `product/`            | Epic analysis, story breakdown, product context, acceptance criteria |

Each folder is a domain. Each file is one focused, portable skill.

---

## Skill format

A skill is a single Markdown file with one clear responsibility. Keep it tool-agnostic when possible — the same skill should be useful in OpenCode, Cursor, Copilot, or Claude Code.

Top of every skill file:

- **What it does** — one sentence
- **When to use it** — trigger condition
- **Inputs** — what the agent needs from the user or context
- **Output** — what the agent should produce
- **Steps** — concise, numbered workflow

## Getting started

### 1. Clone the repo into your project

```bash
git clone https://github.com/your-org/ai-skills-kit.git .ai-skills
```

### 2. Point your AI tool to the skills
Depending on your setup (OpenCode, Cursor, Copilot, etc.), reference the skill files you need directly in your config or as context files.

### 3. Pick only what you need
Skills are fully modular — use one, use all. No dependencies between folders.

## Contributing
- Have a skill that saved you time? Add it.
- Create a folder under the right category (or add a new one)
- Keep the skill file focused on one clear responsibility
- Add a short comment at the top explaining what it does and when to use it
- Open a PR
