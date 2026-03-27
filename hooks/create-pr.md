---
description: Create a Pull Request description based on branch commits.
---

# Command: /create-pr

## Purpose
Create a Pull Request title and description based on commits in the current branch.

## Steps

1. Get current branch commits
// turbo
```bash
git log main..HEAD --oneline
```
This gets all commits specific to this branch (not just last 5).

2. Get changed files summary
// turbo
```bash
git diff main...HEAD --stat
```

3. Generate PR title
Follow conventional commit format: `type(scope): description`

4. Generate PR description
Use this structure:

```
## What changed
- bullet points of key changes

## Why
Brief reason for the change.

## Testing
- How to test this PR
- Any manual steps needed

## Notes
Any migration, env variable, or deployment notes.
```

5. Output the full PR title + description ready to paste into GitHub.
