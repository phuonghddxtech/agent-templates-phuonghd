---
description: Implement a Laravel backend task strictly following conventions
---

## Steps

### 1. Understand the Request
Analyze the task. Determine:
- Database schema changes (Migrations).
- Endpoint contracts (URL, Methods, JSON structures).
- Background processing requirements (Queues/Jobs).
- External integrations.

### 2. Implementation Execution
Create files in logical order. Prefer Artisan commands over manual creation.
Use the tools `/new-model` or `/new-endpoint` if applicable.

Standard Flow:
1. `Migration` + `Model` + `Factory`
2. `Action/Service` class for business logic
3. `FormRequest` for validation
4. `Controller` for orchestration (returning `Inertia::render` or redirect)
5. Vue Component (`resources/js/Pages/`)
6. `routes/web.php` registration

### 3. Verification & Testing
Write PHPUnit / Pest Feature tests for the new Web Route. Test both backend logic and Inertia props structure.
Run `php artisan test` to ensure it passes.

### 4. Stage and Commit
Run `/commit-push` to save changes.
