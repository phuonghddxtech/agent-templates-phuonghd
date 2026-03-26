---
name: laravel-structure
description: HRM-BPO Laravel project structure, file locations, and naming conventions. Use when searching for files, understanding module layout, or navigating the codebase.
---

## Source Layout
All backend code is under `src/`. Pattern: Controller → Service → Repository → Model.

| Layer | Path |
|---|---|
| Controllers | `src/app/Http/Controllers/{Api,Tenant,Core,Common}/` |
| Services | `src/app/Services/` |
| Repositories | `src/app/Repositories/` |
| Models | `src/app/Models/{Core,Tenant}/` |
| Routes | `src/routes/{api,tenant,core}/` |
| Vue Components | `src/resources/js/{core,tenant,common}/` |
| Migrations | `src/database/migrations/` |

## Modules
Attendance, Leave, OT, Payroll, Employee, Contract, Salary, Assets, Shifts, Holidays

## Naming
- Controllers: `AttendanceController.php` (singular PascalCase)
- Models: `AttendanceDetails.php`
- Tables: `attendance_details` (plural snake_case)
- Vue: `ContractSettings.vue`
- Routes: `/api/attendance-logs` (kebab-case)

## Multi-tenancy
- `Core/` = system-level (admin, settings)
- `Tenant/` = tenant-scoped (all business modules)
