Create a Pull Request description for the current branch.

1. Run `git log main..HEAD --oneline` and `git diff main...HEAD --stat`.
2. Generate PR title: `type(scope): description`
3. Generate PR description:
   - What changed
   - Why
   - Testing steps
   - Notes (migration, env vars, deployment)
