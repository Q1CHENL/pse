# Modern Testing Principles

## AssertJ

A powerful and mature assertion library with a type safe API, a variety of
assertions and descriptive failure messages

- `assertThat(obj).xxx(yyy)` with wide range of xxx methods

## General

- Given, When, Then

```java
@Test
void findProduct() {
    // Given(Inpute): preparation
    insertIntoDatabase(new Product(100, "Smartphone"));
    // When(Action): Method call
    Product product = dao.findProduct(100);
    // Then(Output): assertion
    assertThat(product.getName()).isEqualTo("Smartphone");
}
```

- Use prefixes actual and expected
- Use fixed data instead of randomized data (flaky tests, e.g `Instant.now()`, `new Date()`)
- Don’t extend existing tests to "just test one more tiny thing": find failure quick
- Don't hide the relevant parameters (in helper functions)
- Favor composition over inheritance (hard to understand)
- Don’t rewrite production code in tests
- Focus on testing a complete functional requirement (integration test) rather than unit tests with mocks
- Use constructor injection instead of field injection (poor testability)
- Avoid assertTrue() and assertFalse()

```java
// Don't
assertTrue(actualProductList.contains(expectedProduct));
// Do
assertThat(actualProductList).contains(expectedProduct);
```
