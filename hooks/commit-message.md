---
description: Generate a Conventional Commit message based on Git changes.
---

# Command: /commit-message

## Purpose
Generate a Conventional Commit message based on Git changes.

## Steps

1. Load conventions
Read `.kiro/skills/git-convention.md` for commit format and scope rules.

2. Check current status
// turbo
Run `git status` to identify changed files.

3. Analyze changes
// turbo
Run `git diff` for unstaged and `git diff --cached` for staged changes.

4. Generate commit message
Follow the format in `.kiro/skills/git-convention.md`:
- Pick the correct type and scope
- Write a short, imperative description

5. Execute commit
// turbo
```bash
git add .
git commit -m "type(scope): description"
```
