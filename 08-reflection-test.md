# Reflection Test

- Problem
  - Legacy code
  - API of open source library
  - Bad design

## Example

Assume there is no getter for the private field “key” of the
Authentication class but we need to access it for our test

```java
class AuthPrivacyTest {
    @Test
    void testKey() throws Exception {
        Authentication auth = new Authentication("privateKey");
        Class<? extends Authentication> cl = auth.getClass();
        // get the reflected object
        Field field = cl.getDeclaredField("key");
        // set accessible true
        field.trySetAccessible();
        assertEquals(field.get(auth), privateKey);
    }
}
```
