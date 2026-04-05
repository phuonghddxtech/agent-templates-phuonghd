# Pytest & Django Testing Standards

## 1. Pytest Configuration
Always use `pytest` with `pytest-django`. Do not use the default `unittest` standard Django `TestCase`.

## 2. API Testing using APIClient
For testing endpoints, use DRF's `APIClient`.
```python
import pytest
from rest_framework.test import APIClient

@pytest.fixture
def api_client():
    return APIClient()

@pytest.mark.django_db
def test_create_order(api_client, user_factory):
    api_client.force_authenticate(user=user_factory())
    response = api_client.post('/api/orders/', {'amount': 100})
    assert response.status_code == 201
    assert response.data['amount'] == 100
```

## 3. Database Markers
Always decorate tests that hit the database with `@pytest.mark.django_db`.

## 4. Factory Boy
Use `factory_boy` to generate mock data. NEVER hardcode IDs or use `User.objects.create()` repeatedly in tests without factories.

```python
import factory
from myapp.models import Order

class OrderFactory(factory.django.DjangoModelFactory):
    class Meta:
        model = Order
        
    amount = 100
    status = 'pending'
```
