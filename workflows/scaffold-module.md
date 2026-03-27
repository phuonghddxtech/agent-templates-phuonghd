---
description: Tạo migration, model, controller, service, repository cho một module mới
---

## Input required
User must provide: module name (e.g. `asset`, `shift`)

## Steps

1. Confirm module name and layer
Ask user:
- Module name?
- Cần tạo những layer nào? (migration / model / controller / service / repository / vue component)

2. Generate migration
Create file: `src/database/migrations/<timestamp>_create_<module>s_table.php`
Follow existing migration patterns in the project.

3. Generate model
Create file: `src/app/Models/Tenant/<Module>.php`
- Add `$fillable`, relationships, scopes as needed
- Tenant-scoped model

4. Generate controller
Create file: `src/app/Http/Controllers/Api/<Module>Controller.php`
- Thin controller: only handle request/response
- Delegate all logic to Service

5. Generate service
Create file: `src/app/Services/<Module>Service.php`
- Business logic only
- Call Repository for DB operations

6. Generate repository
Create file: `src/app/Repositories/<Module>Repository.php`
- DB queries only
- No business logic

7. Register routes
Add to appropriate route file in `src/routes/api/`
Follow kebab-case: `/api/<module-name>`

8. Output summary
List all files created with their paths.
