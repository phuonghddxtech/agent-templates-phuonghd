# PHPUnit / Pest Testing Standards

## 1. RefreshDatabase trait
Always use `RefreshDatabase` in your Feature tests to ensure a clean state before each test runs. 

## 2. Arrange, Act, Assert (AAA)
Structure tests logically:
- **Arrange**: Set up models, factories, auth.
- **Act**: Make the HTTP request or call the service.
- **Assert**: Verify database state and JSON response.

## 3. Use Model Factories
NEVER use DB::insert or raw arrays to seed test data. Always use Eloquent Factories.

```php
// ✅ DO:
$user = User::factory()->create(['role' => 'admin']);
```

## 4. Feature Testing vs Unit Testing
- **Unit Tests**: For isolated math, formatters, and utilities (no database hit).
- **Feature Tests**: For API endpoints (Controllers, Actions). This is where you should spend 90% of your testing effort.

```php
public function test_user_can_create_order()
{
    // Arrange
    $user = User::factory()->create();
    $payload = ['item_id' => 1, 'qty' => 2];

    // Act
    $response = $this->actingAs($user, 'sanctum')->postJson('/api/orders', $payload);

    // Assert
    $response->assertStatus(201)
             ->assertJsonStructure(['data' => ['id', 'status', 'total']]);
    
    $this->assertDatabaseHas('orders', [
        'user_id' => $user->id,
        'item_id' => 1
    ]);
}
```
