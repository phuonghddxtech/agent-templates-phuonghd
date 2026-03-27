Review code changes before commit.

1. Run `git diff` and `git diff --cached` to get all changes.
2. Check for bugs, security risks, N+1 queries, architecture violations (logic in Controller instead of Service).
3. Verify naming conventions from `.kiro/skills/coding-convention.md`.
4. Output:
   - Issues (CRITICAL / WARNING / INFO)
   - Suggestions
   - Risk level: LOW / MEDIUM / HIGH
