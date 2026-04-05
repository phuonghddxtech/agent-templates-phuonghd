# Validation & Request Handling

## 1. Always Use Form Requests
NEVER validate data inside the controller using `$request->validate()`.
Extract all validation logic into a dedicated FormRequest class.

```php
// ❌ BAD:
public function store(Request $request) {
    $request->validate(['name' => 'required', 'email' => 'required|email']);
    // ...
}

// ✅ GOOD:
public function store(StoreUserRequest $request) {
    // $request is already validated
    $validatedData = $request->validated();
    app(CreateUserAction::class)->execute($validatedData);
}
```

## 2. Authorization in Form Requests
Use the `authorize()` method in Form Requests to determine if the user has permission to perform this action.

```php
public function authorize(): bool
{
    return $this->user()->can('create', User::class);
}
```

## 3. Strict Validation Rules
- ALWAYS validate what you expect. Don't trust input.
- Use array dot notation for nested JSON payloads.
- Use explicit Enums validation `Rule::enum(UserRole::class)` in Laravel 9+.
