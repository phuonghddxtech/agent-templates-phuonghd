# Clean Code & Python Standards

## 1. Type Hinting
Always use Type Hints (Python 3.10+) for function parameters and return types.

```python
# ✅ DO:
def calculate_discount(price: float, percentage: float) -> float:
    return price * (1 - percentage)

# ❌ BAD:
def calculate_discount(price, percentage):
    return price * (1 - percentage)
```

## 2. Formatting (PEP-8)
- Maximum line length of 88 to 100 characters (compatible with Black).
- Use `snake_case` for variables/functions and `CamelCase` for classes.
- Sort imports logically: Standard Lib -> Third Party -> Local.

## 3. Docstrings
Use Google-style docstrings for complex classes and functions. Describe args and return values.

## 4. Services Layer
Django can get bloated. Avoid writing business logic in Views or Serializers.
Extract reusable business logic into separate `services.py` modules inside your apps.

```python
# users/services.py
def create_customer(email: str, password: str) -> User:
    user = User.objects.create_user(email=email, password=password)
    # emit signals or side effects
    return user
```
