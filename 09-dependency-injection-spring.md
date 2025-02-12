# Dependency Injection with Spring

## Inversion of Control

Control of objects or portions of a program is transferred to a container or framework, which makes calls to the program’s custom code

## Spring

- 3 possibilities to use dependency injection
  - Constructor injection
  - Method injection (setter)
  - Field injection (attribute)
- BeanFactory: An object that the Spring container instantiates, assembles, and manages
  - `@Bean`: Used on methods within a `@Configuration` class to define and configure beans.
  - `@Component`: A generic stereotype annotation for a Spring-managed component.
  - `@Service`: A specialization of `@Component` intended for the service layer, improving readability and semantic clarity.
- ApplicationContext: a sub interface of BeanFactory and provides more
  enterprise specific functionalities

### Constructor Injection (preferred: more robust, prevents errors)

No annotation needed in Spring

### Method Injection

```java
// With this annotation, the container will call setter methods of our Bean class, after instantiating
// the object (possibly) with the default constructor with no arguments)
@Autowired
public void setStore(Store store) {
    this.store = store;
}
```

### Field Injection

```java
public class Store {
    // This annotation tells Spring to inject a bean object
    @Autowired
    private Item item;
}
```

### Autowiring dependencies

4 modes:

1. no: default value → no autowiring is used for the bean and we have to explicitly
   name the dependencies
2. byName: autowiring based on the name of the property → Spring will look for a bean
   with the same name as the property that needs to be set

   ```java
   public class Store {
       @Autowired
       // Spring will look for the one with name "item1"
       // if there are multiple ones
       @Qualifier("item1")
       private Item item;
   }
   ```

3. byType: similar to the byName autowiring, but based on the type of the property
   → Spring will look for a bean with the same type of the property to set
   (if there's more than one bean of that type, the framework throws an exception)

   ```java
   // Store will be autowired by type
   @Bean(autowire = Autowire.BY_TYPE)
   public class Store {
       private Item item;
       public setItem(Item item){
        this.item = item;
        }
   }
   ```

4. constructor: autowiring based on constructor arguments → Spring will look for
   beans with the same type as the constructor arguments
