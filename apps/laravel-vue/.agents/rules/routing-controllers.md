# Routing & Controllers

## 1. `routes/web.php` for Interactions
Since this is a fullstack app, use `routes/web.php` for browser interactions instead of API routes.
NEVER write closure-based routes for business logic.

## 2. Controller Methods
Controllers should be THIN. They only do 3 things:
1. Receive request (via FormRequest).
2. Call Action/Service layer or Query DB.
3. Return `Inertia::render()` or Redirect.

## 3. Response Formatting (Inertia.js)
NEVER return JSON or API Resources directly if rendering a page.
ALWAYS use `Inertia::render('PageName', [...data])`.

```php
// ✅ DO:
public function show(User $user)
{
    return Inertia::render('Users/Show', [
        'user' => $user->only('id', 'name', 'email') // Only pass what's needed
    ]);
}

// ✅ DO: Post/PUT Redirects
public function store(StoreUserRequest $request)
{
    User::create($request->validated());
    return redirect()->route('users.index')->with('success', 'User created.');
}
```
