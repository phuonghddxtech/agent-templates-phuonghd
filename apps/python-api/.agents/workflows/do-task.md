---
description: Implement a Python backend task strictly following conventions
---

## Steps

### 1. Understand the Request
Analyze the task. Determine:
- Database schema changes (Migrations).
- Endpoint contracts (URL, Methods, JSON structures).
- Background processing requirements (Celery).
- External integrations.

### 2. Implementation Execution
Create files in logical order. 
Use `/new-model` or `/new-api` if applicable.

Standard Flow:
1. `models.py` + `admin.py` + `makemigrations`
2. `services.py` for business logic (if complex)
3. `serializers.py` for validation
4. `views.py` (ViewSets)
5. `urls.py`

### 3. Verification & Testing
Write Pytest tests for every new Endpoint or highly complex Service.
Run `pytest` to ensure it passes.

### 4. Stage and Commit
Run `/commit-push` to save changes.
