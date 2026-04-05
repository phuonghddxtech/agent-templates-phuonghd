---
description: Create a new eloquent model with its migration, factory, and seeder
---

## Steps

### 1. Requirements Processing
Analyze the model required:
- Table name
- Columns and types
- Relationships (`hasMany`, `belongsTo`, etc.)
- Factory states needed

### 2. Run Artisan Command
// turbo
```bash
php artisan make:model {ModelName} -mfs
```
This generates the Model, Migration, Factory, and Seeder.

### 3. Edit Migration
Define schema in `database/migrations/xxxx_xx_xx_create_xxx_table.php`:
- Add `foreignIdFor()`
- Add necessary index or unique constraints
- Apply soft deletes if required.

### 4. Edit Factory
Define dummy data matching the schema in `database/factories/{Model}Factory.php`.

### 5. Edit Model
- Define `$fillable` or `$guarded = []`.
- Add `casts`.
- Define relationship methods.
- Add local query scopes.

### 6. Edit Seeder (Optional)
If needed, call the factory in `database/seeders/{Model}Seeder.php` and register it in `DatabaseSeeder.php`.

### 7. Run Migration
// turbo
```bash
php artisan migrate
```
