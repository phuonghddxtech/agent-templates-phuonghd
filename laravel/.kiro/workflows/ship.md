---
description: Review, commit và push code trong một lệnh duy nhất
---

## Steps

1. Check for uncommitted changes
// turbo
```bash
git status
git diff
git diff --cached
```
If branch is `main` or `master` → stop and warn user.

2. Review code quality
Check for:
- Architecture violations (business logic in Controller instead of Service)
- N+1 queries
- Missing error handling
- Security risks (unvalidated input, exposed secrets)

If CRITICAL issues found → stop and report before continuing.

3. Generate commit message
Follow `.kiro/skills/git-convention.md`: `type(scope): description`

4. Commit and push
// turbo
```bash
git add <each changed file explicitly — never use git add . or git add -A>
git commit -m "type(scope): description"
git push origin HEAD
```

5. Output summary
Show: branch name, commit hash, commit message, files changed.
