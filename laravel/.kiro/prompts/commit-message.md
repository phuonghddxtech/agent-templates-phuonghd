Generate a conventional commit message based on current git changes.

1. Run `git status`, `git diff`, `git diff --cached`.
2. Follow format in `.kiro/skills/git-convention.md`: `type(scope): description`
3. QUAN TRỌNG: Chỉ `git add <từng_file_đã_được_chỉnh_sửa>`. Nghiêm cấm sử dụng `git add .` hoặc `git add -A`.
4. Execute: `git commit -m "type(scope): description"`
