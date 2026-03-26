# Project Structure

## Root Layout

```
root/
├── src/                  # Main Laravel application
├── css/                  # Compiled CSS output
├── js/                   # Compiled JS output
├── docker/               # Docker configs (Nginx, PHP, Supervisor, cron)
├── docker-compose.yml    # Docker Compose setup
├── webpack.mix.js        # Laravel Mix (asset build config)
├── package.json          # Node dependencies
└── documentation/        # HTML documentation
```

## Laravel App (`src/`)

```
src/
├── app/
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── Api/          # RESTful API controllers
│   │   │   ├── Tenant/       # Tenant-scoped controllers
│   │   │   ├── Core/         # Core system controllers
│   │   │   └── Common/       # Shared controllers
│   │   ├── Requests/         # Form request validation
│   │   ├── Resources/        # API response transformers
│   │   └── Middleware/       # HTTP middleware
│   ├── Models/
│   │   ├── Core/             # Core system models
│   │   └── Tenant/           # Tenant-scoped models
│   │       ├── Attendance/
│   │       ├── Contract/
│   │       ├── Employee/
│   │       ├── Leave/
│   │       ├── OT/
│   │       ├── Payroll/
│   │       └── Salary/
│   ├── Services/             # Business logic layer
│   ├── Repositories/         # Data access layer
│   ├── Jobs/                 # Queued background jobs
│   ├── Mail/                 # Mailable classes
│   ├── Notifications/        # Notification classes
│   ├── Exports/              # Excel export classes
│   ├── Imports/              # Excel import classes
│   ├── Filters/              # Query filter builders
│   ├── Rules/                # Custom validation rules
│   ├── Observers/            # Model event observers
│   ├── Helpers/              # Helper utilities
│   └── Console/              # Artisan commands
├── routes/
│   ├── api.php               # Main API router
│   ├── web.php               # Main web router
│   ├── api/                  # API route groups by module
│   ├── tenant/               # Tenant-specific routes
│   └── core/                 # Core system routes
├── resources/
│   ├── js/
│   │   ├── core/             # Core Vue components
│   │   ├── tenant/           # Tenant Vue components
│   │   ├── common/           # Shared Vue components
│   │   ├── store/            # Vuex store modules
│   │   └── mainApp.js        # Vue app entry point
│   ├── sass/                 # SCSS source files
│   ├── views/                # Blade templates
│   └── lang/                 # Translation files (en, vi, ja)
├── database/
│   ├── migrations/
│   ├── seeders/
│   └── factories/
└── config/                   # Laravel config files
```

## Architecture Patterns

- **MVC + Service + Repository**: Controllers → Services → Repositories → Models
- **Multi-Tenancy**: Tenant-scoped models and routes; core vs. tenant separation throughout
- **Observer Pattern**: Model observers in `app/Observers/` for automatic side effects
- **Job Queue**: Async processing via `app/Jobs/` with Supervisor workers
- **Filter Pattern**: `app/Filters/` for reusable query builder filters

## Naming Conventions

| Artifact | Convention | Example |
|---|---|---|
| Controllers | Singular PascalCase | `AttendanceController` |
| Models | Singular PascalCase | `AttendanceDetails` |
| DB Tables | Plural snake_case | `attendance_details` |
| Vue Components | PascalCase | `ContractSettings.vue` |
| Routes | RESTful, kebab-case | `/api/attendance-logs` |
| Migrations | snake_case with timestamp | `2023_01_01_create_attendances_table` |

## Frontend Organization

Vue components are split by domain under `src/resources/js/`:
- `core/` — system-level UI (auth, settings, admin)
- `tenant/` — tenant-facing features (attendance, leave, OT, etc.)
- `common/` — reusable components shared across both

Compiled output goes to `js/` and `css/` at the root (not inside `src/`).
