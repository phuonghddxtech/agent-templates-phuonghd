---
description: Verify if a branch is safe to merge into main.
---

# Command: /merge-check

## Purpose
Verify if the current branch is safe to merge.

## Steps

1. Check for conflicts with main
// turbo
```bash
git fetch origin
git diff main...HEAD --stat
git merge-base --is-ancestor HEAD origin/main || echo "Branch has diverged"
```

2. Check uncommitted changes
// turbo
Run `git status` — there should be no uncommitted changes.

3. Review commit history
// turbo
Run `git log main..HEAD --oneline` — summarize what will be merged.

4. Output merge readiness
Based on the above, output one of:

```
✅ READY TO MERGE
- No conflicts detected
- X commits to be merged
- Summary: ...
```

or

```
🚫 BLOCKED
- Reason: (conflicts / uncommitted changes / missing review)
- Action needed: ...
```
