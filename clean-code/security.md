# Security review for added code

## What it does
Scans the current PR diff and flags newly added or modified code against common security vulnerability classes, including the OWASP Top 10.

## When to use it
Use this skill before merging a PR that touches input handling, authentication, authorization, secrets, data flows, or external integrations.

## Inputs
- The PR diff (`git diff base-branch...HEAD`, `gh pr diff <number>`, or a diff file)
- Project language/framework
- Risk appetite or compliance context (optional)

## Output
- A Markdown security report listing file, line, vulnerability class, severity, explanation, and proposed fix.

## Steps

1. **Load the diff**
   - Focus on added (`+`) and modified lines.
   - Ignore whitespace-only changes and generated files unless relevant.

2. **Scan for common vulnerability classes**

   | Class | What to look for | OWASP mapping |
   |-------|------------------|---------------|
   | Injection | Unparameterized queries, `eval`, `exec`, dynamic SQL, shell commands | A03:2021 – Injection |
   | Broken access control | Missing auth checks, insecure direct object references, hardcoded IDs | A01:2021 – Broken Access Control |
   | Cryptographic failures | Hardcoded secrets, weak hashing, missing TLS, plaintext storage | A02:2021 – Cryptographic Failures |
   | SSRF / unsafe redirects | User-controlled URLs passed to HTTP clients or redirects | A10:2021 – Server-Side Request Forgery |
   | XSS | Unescaped output, `innerHTML`, unsafe template interpolation | A03:2021 – Injection (XSS subset) |
   | Insecure deserialization | `pickle`, `yaml.load`, `ObjectInputStream` without validation | A08:2021 – Software and Data Integrity Failings |
   | Vulnerable dependencies | New packages with known CVEs (if lockfile diff is available) | A06:2021 – Vulnerable and Outdated Components |
   | Misconfiguration | Debug flags, default credentials, overly broad CORS | A05:2021 – Security Misconfiguration |
   | Logging exposure | Logging secrets, tokens, PII | A09:2021 – Security Logging and Monitoring Failures |
   | Path traversal | User-controlled file paths without sanitization | A01:2021 – Broken Access Control |

3. **Triage findings**
   - Mark severity: `critical`, `high`, `medium`, `low`, `info`.
   - Filter out false positives with a one-sentence rationale.

4. **Propose fixes**
   - Give concrete code-level mitigations, not generic advice.
   - Prefer safe APIs, validation, escaping, and moving secrets to configuration.

5. **Produce the report**
   - Group by severity.
   - Include file path, line number, issue, OWASP mapping, and proposed fix.

## Severity rules

- `critical`: Stop the PR. Fix before merge.
- `high`: Must be addressed or explicitly accepted by a security-aware reviewer.
- `medium`: Should be fixed; can be merged with a tracked follow-up.
- `low` / `info`: Document and consider in a follow-up.

## Output template

```markdown
## Security review summary

- **PR**: ...
- **Scanned files**: ...
- **Findings**: 1 critical, 1 medium, 0 low

## Critical

### `<file>` line `<line>`
- **Issue**: Hardcoded API key in source
- **OWASP**: A02:2021 – Cryptographic Failures
- **Fix**: Move the key to a secret manager or environment variable; inject it at runtime.

## Medium

### `<file>` line `<line>`
- **Issue**: User input concatenated into shell command
- **OWASP**: A03:2021 – Injection
- **Fix**: Use a parameterized command API or an allowlist before executing.
```

## Rules
- Do not suggest comments as fixes.
- Do not flag test fixtures or documentation unless they contain real secrets.
- Be specific: cite line numbers, functions, and exact patterns.
