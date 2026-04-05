# Eloquent ORM Best Practices

## 1. N+1 Problem Prevention
ALWAYS eager load relationships when fetching collections. Use `with()` or `$model->load()`.
NEVER query inside a loop.

```php
// ❌ BAD: Causes N+1 queries
$users = User::all();
foreach ($users as $user) {
    echo $user->profile->bio; // Query executed here
}

// ✅ GOOD:
$users = User::with('profile')->get();
foreach ($users as $user) {
    echo $user->profile->bio;
}
```

## 2. Query Scopes
Encapsulate complex WHERE clauses into Local Scopes in the Model.

```php
// User.php
public function scopeActive($query)
{
    return $query->where('status', 'active');
}

// Usage
User::active()->get();
```

## 3. Thin Controllers, Fat Models? No, Thin Both.
Don't put complex business logic in models. Models should only contain:
- Relationships (`hasMany`, `belongsTo`)
- Scopes
- Accessors / Mutators
- Casts

## 4. Mass Assignment & Strict Mode
Always define `$fillable` or use `Model::unguard()` safely in boot.
In Laravel 11+, consider using `$guarded = [];` but ensure input is strictly validated via FormRequests.
