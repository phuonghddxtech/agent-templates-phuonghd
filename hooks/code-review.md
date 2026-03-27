---
description: Review code changes before commit.
---

# Command: /code-review

## Purpose
Review code changes before commit against DXTech standards.

## Steps

1. Load conventions
Read `shared-workflow/.agents/workflows/code-review.md` and any `ai-rules/coding-convention.md` if it exists.

2. Get changes
// turbo
```bash
git diff          # unstaged changes
git diff --cached # staged changes
```

3. Analyze for issues
Check:
- Bugs or logic errors
- Security risks (SQL injection, unvalidated input, exposed secrets)
- Code duplication
- Architecture violations (e.g. business logic in Controller instead of Service)
- Missing error handling
- N+1 query problems

4. Verify conventions
- Controllers → thin, delegate to Services
- Services → business logic only
- Repositories → DB queries only
- Models → no business logic
- Follow naming conventions from `.kiro/steering/structure.md`

5. Output review report
Format:
```
## Issues
- [CRITICAL/WARNING/INFO] description

## Suggestions
- description

## Risk Level
LOW / MEDIUM / HIGH
```
