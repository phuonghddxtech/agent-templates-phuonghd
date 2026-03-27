Check if current branch is safe to merge into main.

1. Run `git fetch origin`, `git diff main...HEAD --stat`, `git log main..HEAD --oneline`.
2. Check for uncommitted changes with `git status`.
3. Output READY TO MERGE or BLOCKED with reason.
