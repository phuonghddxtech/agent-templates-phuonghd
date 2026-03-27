---
name: bug-fix-patterns
description: Common bug fix patterns for HRM-BPO. Use when diagnosing bugs, understanding where to look for issues, or deciding which files to modify.
---

## Diagnosis Checklist
1. Check Controller for input validation issues
2. Check Service for business logic errors
3. Check Repository for query/filter bugs
4. Check Model for relationship/scope issues
5. Check Vue component for frontend display bugs
6. Check routes for missing/wrong endpoints

## Common Bug Locations by Symptom

| Symptom | Look in |
|---|---|
| Wrong data returned | Repository query, Model scope |
| Validation error | FormRequest, Controller |
| Permission denied | Middleware, Policy |
| Calculation wrong | Service layer |
| UI not updating | Vue component, Vuex store |
| Email not sent | Job, Mail class, queue |
| Export broken | Exports/ class |

## Safe Fix Rules
- Minimal change only — do not refactor outside bug scope
- Never change DB migrations (create new one if schema change needed)
- Check if method is used elsewhere before modifying signature
- Tenant-scoped models must stay within tenant context

## Verify After Fix
```bash
docker-compose exec hrm_app php -l <changed_file>
docker-compose exec hrm_app php artisan test --filter <TestClass>
```
