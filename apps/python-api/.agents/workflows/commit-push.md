---
description: Stage, run formatters, test, commit, and push Python code
---

## Steps

### 1. View Git Status
// turbo
```bash
git status
git diff --stat
```

### 2. Formatting & Testing
Format code using Black/Flake8. Then run PyTest.
// turbo
```bash
black .
flake8 .
pytest
```

Nếu test/flake8 fail → STOP. 

### 3. Đánh giá Unit Test (Mandatory Check)
Đặc biệt với các commit loại `feat` hoặc `fix`, bạn **PHẢI** viết Pytest:
- **Feature mới (`feat`)**: Đã có test case bao phủ API/Service chưa? Đã dùng APIClient và FactoryBoy chưa?
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
