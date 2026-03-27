---
description: Chạy full test suite và báo cáo kết quả
---

## Steps

1. Check syntax of recently changed files
// turbo
```bash
git diff --name-only HEAD | grep '\.php$' | xargs -I{} docker-compose exec hrm_app php -l {}
```

2. Run PHPUnit tests
// turbo
```bash
docker-compose exec hrm_app ./vendor/bin/phpunit --stop-on-failure
```

3. Run frontend tests
// turbo
```bash
npx jest --runInBand
```

4. Output report
```
## Test Results

### Backend (PHPUnit)
- Status: PASS / FAIL
- Tests: X passed, Y failed
- Failed tests: (list if any)

### Frontend (Jest)
- Status: PASS / FAIL
- Tests: X passed, Y failed

### Overall: ✅ ALL PASS / ❌ FAILURES FOUND
```

If failures found → show exact error messages and file locations.
