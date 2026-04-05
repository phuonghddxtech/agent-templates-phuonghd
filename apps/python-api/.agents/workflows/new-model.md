---
description: Create a new Django Model with its Admin class and migrations
---

## Steps

### 1. Requirements Processing
Analyze the model required:
- Table name
- Fields and types
- Relationships (`ForeignKey`, `ManyToManyField`)
- Meta classes (indexes, ordering)

### 2. Implement Model
Create or edit the models.py file in the relevant app folder.
- Add fields.
- Add `__str__` method.
- Add custom Manager if required.

### 3. Implement Admin
Register the model in `admin.py`.
- Define an `admin.ModelAdmin` class.
- Set `list_display`, `search_fields`, `list_filter`.

### 4. Implement Factory
Create `ModelFactory` using `factory_boy` in a `tests/factories.py` file.

### 5. Generate Migrations
// turbo
```bash
python manage.py makemigrations
```

### 6. Run Migrations
// turbo
```bash
python manage.py migrate
```
