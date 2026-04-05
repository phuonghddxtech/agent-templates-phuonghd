# Clean Code & Architecture (Laravel/PHP)

## 1. PSR Standards & Type Hinting
- Always follow **PSR-12** coding standard.
- Use **strict_types** at the top of every PHP file: `declare(strict_types=1);`
- Always define parameter types and return types. Use nullable types `?string` instead of omitting types.

```php
// ✅ DO:
declare(strict_types=1);

class UserService
{
    public function createUser(string $name, ?string $email): User
    {
        // ...
    }
}
```

## 2. Action Classes (Service Pattern)
Avoid fat controllers. Extract business logic into single-responsibility Action classes or Services.
- **Action Classes**: One class, one method (`handle()` or `execute()`). Good for complex mutations.
- **Services**: Group logical methods. Good for domain-specific wrappers (e.g. `StripeService`).

```php
// ✅ DO: Action Class
class CreateOrderAction
{
    public function execute(User $user, array $data): Order
    {
        return DB::transaction(function () use ($user, $data) {
            $order = $user->orders()->create($data);
            // ...
            return $order;
        });
    }
}
```

## 3. Don't use Facades for core logic (Optional but recommended)
Dependency injection is preferred for testability, except for standard Laravel features (Auth, DB, Log, Cache) where Facades are acceptable.

## 4. No Magic Numbers/Strings
Use Class Constants or Enums (PHP 8.1+) instead of raw strings/numbers.

```php
// ✅ DO:
enum OrderStatus: string {
    case PENDING = 'pending';
    case PAID = 'paid';
}
$order->status = OrderStatus::PAID;
```
