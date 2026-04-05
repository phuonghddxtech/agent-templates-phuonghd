---
description: Create a new API endpoint using DRF ViewSets and Serializers
---

## Steps

### 1. Planning
- Endpoint URL
- HTTP Methods needed
- Serializer validation requirements
- Select/Prefetch related optimizations

### 2. Implement Serializer
Create or edit `serializers.py`.
- Define `ModelSerializer` or `Serializer`.
- Add custom validation methods `validate_fieldname()`.

### 3. Implement Service (Optional)
If complex logic is needed, create it in `services.py`.

### 4. Implement ViewSet
Create or edit `views.py`.
- Define `ViewSet` or `GenericViewSet` or `APIView`.
- Optimize `.queryset` with `select_related`/`prefetch_related`.
- Call Service in `perform_create` or action methods if applicable.

### 5. Register URL
Add to `urls.py` via `DefaultRouter` or `path()`.

### 6. Write Tests
Use `tests.py` or create a generic test folder.
- Write Pytest functions using `APIClient` fixture.
- Test 201/200 OK.
- Test 400 Bad Request.

// turbo
```bash
pytest tests/
```
