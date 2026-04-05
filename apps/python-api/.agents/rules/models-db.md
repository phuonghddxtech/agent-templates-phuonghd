# Django Models & ORM Best Practices

## 1. N+1 Problem Prevention
ALWAYS optimize querysets in your Views/Services to prevent N+1 queries.
- Use `select_related()` for `ForeignKey` and `OneToOneField`.
- Use `prefetch_related()` for `ManyToManyField` and reverse `ForeignKey`.

```python
# ❌ BAD:
users = User.objects.all()
for user in users:
    print(user.profile.bio) # Hits DB in every loop

# ✅ GOOD:
users = User.objects.select_related('profile').all()
for user in users:
    print(user.profile.bio)
```

## 2. Fat Models - Thin Views
Methods that operate exclusively on a single instance's data should belong to the Model.
Use Custom Managers (`models.Manager`) or QuerySets (`models.QuerySet`) for complex table-wide filtering.

```python
class ActiveUserManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(is_active=True)

class User(AbstractUser):
    # ...
    active_objects = ActiveUserManager()
```

## 3. Indexes & Constraints
Always add `db_index=True` for fields that are frequently filtered or ordered by.
Ensure `unique_together` or `UniqueConstraint` is used when needed for data integrity.

## 4. Updates & Deletes
Use `.update()` on querysets when modifying multiple records instead of iterating and saving one by one.
```python
# ✅ FAST
User.objects.filter(status='pending').update(status='active')
```
