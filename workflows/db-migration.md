---
description: Tạo migration để thay đổi schema database an toàn
---

## Input required
User must provide: table name, changes needed (add column / drop column / modify column / add index)

## Steps

1. Check existing migration and model
// turbo
```bash
ls src/database/migrations/ | grep <table_name>
```
Read the latest migration for this table to understand current schema.

2. Validate change request
- NEVER modify existing migration files
- Always create a new migration
- If dropping a column → warn user about data loss

3. Generate migration file
Create: `src/database/migrations/<timestamp>_<action>_<column>_to_<table>_table.php`

Follow pattern:
```php
public function up(): void
{
    Schema::table('<table>', function (Blueprint $table) {
        // change here
    });
}

public function down(): void
{
    Schema::table('<table>', function (Blueprint $table) {
        // revert here
    });
}
```
Always implement `down()` method.

4. Update model $fillable if new column added
Update: `src/app/Models/Tenant/<Model>.php`

5. Output instructions
```
## Migration created
File: src/database/migrations/<filename>

## Run migration
docker-compose exec hrm_app php artisan migrate

## Rollback if needed
docker-compose exec hrm_app php artisan migrate:rollback
```
