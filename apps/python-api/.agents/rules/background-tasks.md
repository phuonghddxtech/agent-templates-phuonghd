# Celery & Background Tasks Best Practices

## 1. Idempotency is Mandatory
Every Celery task MUST be idempotent. If a task fails midway and is automatically retried, it should not corrupt the database or duplicate actions.
- Use atomic database operations (`select_for_update()`).
- Check state before modifying (e.g. `if order.status == 'new':`).

## 2. Pass IDs, NOT Model Instances
NEVER pass full ORM model instances as task arguments. They can become stale by the time the worker executes them. Pass primary keys (IDs) instead.

```python
# ❌ BAD:
send_email_task.delay(user_instance)

# ✅ GOOD:
send_email_task.delay(user_instance.id)
```
Inside the task, fetch the instance: `user = User.objects.get(id=user_id)`.

## 3. Retries & Error Handling
Handle external API failures gracefully using Celery's `autoretry_for`.

```python
@shared_task(bind=True, autoretry_for=(ConnectionError,), retry_kwargs={'max_retries': 3})
def sync_external_data(self, item_id):
    # logic
    pass
```

## 4. Only Delay Simple Types
Celery uses JSON by default. Only pass standard JSON-serializable types (strings, ints, floats, lists, dicts) as arguments. No custom objects.
