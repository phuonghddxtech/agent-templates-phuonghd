---
description: Create a new Laravel controller, web route, and an Inertia Vue page
---

## Steps

### 1. Planning
- Web route endpoint (e.g., `GET /orders`, `POST /orders`)
- Required Controller methods.
- Vue component file path (e.g., `resources/js/Pages/Orders/Index.vue`).
- FormRequest needed for submitted data?

### 2. Scaffold Backend
// turbo
```bash
php artisan make:controller Web/OrderController
```

If accepting user input:
// turbo
```bash
php artisan make:request StoreOrderRequest
```

### 3. Implement Controller
- Accept `Request` or `FormRequest`.
- Query DB or call Action class.
- Return `Inertia::render('Orders/Index', ['data' => ...])`.

### 4. Scaffold Vue Page
Create the `.vue` file in `resources/js/Pages/`.
Use `<script setup lang="ts">` and define props using `defineProps`.

### 5. Register Web Route
Open `routes/web.php` and add the route:
```php
Route::get('/orders', [OrderController::class, 'index'])->name('orders.index');
```

### 6. Verify and Test
- Verify Typescript compiles.
- Run `php artisan test` if tests were created.
