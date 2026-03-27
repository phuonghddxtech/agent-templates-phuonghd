---
description: Push current branch to remote repository.
---

# Command: /push

## Purpose
Push current branch to remote repository safely.

## Steps

1. Check for uncommitted changes
// turbo
Run `git status` — if there are uncommitted changes, warn the user and stop.

2. Verify current branch
// turbo
Run `git branch --show-current` — confirm it's not `main` or `master` to avoid accidental pushes.

3. Push branch
// turbo
Run `git push origin HEAD`
