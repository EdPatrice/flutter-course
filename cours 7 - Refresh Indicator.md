# Indicateur de Rafraîchissement

```dart
Future<void> fetchProducts() async {
    // code ...
}

body: RefreshIndicator(
    child: ListView(), 
    onRefresh: fetchProducts,
)
```
