---
description: Stage, commit, push Laravel code and create PR
---

## Steps

### 1. View Git Status
// turbo
```bash
git status
git diff --stat
```

### 2. Type Checking & Testing
Run tests before committing. If PHPStan/Pint are configured, run them.
// turbo
```bash
php artisan test
```

Nếu test fail → STOP. 

### 3. Đánh giá Unit Test (Mandatory Check)
Đặc biệt với các commit loại `feat` hoặc `fix`, bạn **PHẢI** viết Feature test cho Controller/Action:
- **Feature mới (`feat`)**: Đã có test case bao phủ logic mới chưa?
- **Lỗi (`fix`)**: Bạn đã tạo regression test case tái hiện lỗi chưa?
- 🔴 Nếu chưa có test, KHÔNG ĐƯỢC COMMIT. Khuyên user tạo test file và viết test trước.

### 4. Stage & Commit
```bash
git add .
git commit -m "feat(module): short description under 60 chars

- Detailed body explaining why and what changed.
"
```

### 5. Push
```bash
git push origin HEAD
```
