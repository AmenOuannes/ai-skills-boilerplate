# Analyze E2E test failures

## What it does
Reads an E2E test report and categorizes failures to suggest fixes or follow-up actions.

## When to use it
Use this skill after a nightly or CI E2E run to triage failures quickly.

## Inputs
- E2E report path, URL, or raw output
- Test framework (Playwright, Cypress, Selenium, etc.)
- Optional CI logs

## Output
- Categorized failure summary with proposed fixes

## Steps

1. **Load the report**
   - Parse failures, errors, screenshots, traces, and logs.

2. **Categorize failures**

   | Category | Signal | Likely action |
   |----------|--------|-------------|
   | Flaky test | Intermittent timeout, previous runs passed | Quarantine or retry logic |
   | Real bug | Consistent assertion or crash | Open a bug ticket |
   | Test data issue | Setup/teardown failure | Fix fixtures or seed data |
   | Environment issue | Network, service unavailable | Alert infra or rerun |
   | UI change | Selector not found, text mismatch | Update test selectors |

3. **Group by root cause**
   - Combine failures that share the same error, file, or environment signal.

4. **Propose fixes**
   - For real bugs: point to the likely source code area.
   - For flaky tests: suggest retry, wait, or quarantine.
   - For UI changes: list selectors or text that need updating.

5. **Produce the report**

## Output template

```markdown
## E2E failure summary

- **Total failures**: ...
- **Flaky**: ...
- **Real bugs**: ...
- **Environment / data**: ...
- **Test maintenance**: ...

## Critical failures

### `<test-file>` — `<test-name>`
- **Category**: Real bug
- **Failure**: ...
- **Suggested fix**: ...

## Follow-up actions

- [ ] ...
```

## Rules
- Do not blame flakiness without evidence.
- Link to screenshots, traces, or CI logs when available.
- Separate test fixes from source-code fixes.
