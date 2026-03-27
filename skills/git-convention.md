---
name: git-convention
description: Git commit and branch conventions for HRM-BPO. Use when generating commit messages, creating branches, or writing PR descriptions.
---

## Commit Format
```
type(scope): short description
```
- Lowercase, imperative tense, no period at end
- Max 72 characters total

## Commit Types
| Type | When to use |
|---|---|
| `feat` | New feature |
| `fix` | Bug fix |
| `refactor` | Code restructure, no behavior change |
| `docs` | Documentation only |
| `test` | Tests only |
| `chore` | Maintenance, deps, config, build |

## Scope
Use the HRM module name:
`attendance`, `leave`, `ot`, `payroll`, `employee`, `contract`, `salary`, `auth`, `role`, `shift`, `holiday`, `asset`

## Examples
```
feat(leave): add approval notification email
fix(attendance): correct overtime calculation on night shift
refactor(payroll): extract tax logic into TaxService
chore: update maatwebsite/excel to 3.1.48
```

## Branch Naming
```
feature/short-description
fix/short-description
chore/short-description
```

## PR Title
Same format as commit: `type(scope): description`
