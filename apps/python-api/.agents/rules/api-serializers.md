# Django REST Framework (DRF) Best Practices

## 1. Class-Based Views (ViewSets)
Prefer `ModelViewSet` or `GenericViewSet` over function-based `@api_view` for CRUD operations. It enforces structure and helps with automated documentation.

## 2. Serializers = Validation
Use serializers to validate data. Define strict `validate()`, `validate_<field_name>()` methods.
NEVER perform request dictionary manipulation in the View before passing it to the serializer.

```python
# ✅ GOOD:
class OrderSerializer(serializers.ModelSerializer):
    class Meta:
        model = Order
        fields = ['id', 'amount', 'status']
    
    def validate_amount(self, value):
        if value < 0:
            raise serializers.ValidationError("Amount cannot be negative")
        return value
```

## 3. Separation of Concerns
Keep Views thin:
```python
class OrderViewSet(viewsets.ModelViewSet):
    serializer_class = OrderSerializer
    queryset = Order.objects.select_related('customer')

    def perform_create(self, serializer):
        # Good: Call service/action here if complex
        order = serializer.save()
        create_order_action(order)
```

## 4. Nested Serializers
Be careful with nested serializers for Writes (creation).
Use `PrimaryKeyRelatedField` allowing ID inputs for creation, and nested serializers for Read operations via `.to_representation()`.

```python
def to_representation(self, instance):
    rep = super().to_representation(instance)
    rep['customer'] = CustomerSerializer(instance.customer).data
    return rep
```
