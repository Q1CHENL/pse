# Dependency Injection with Guice

> From state testing to behavior testing: reduced coupling

## Guice Modules

- AbstractModule (an provided abstract class with a protected method
  `configure()`)
- ProductionModule (Defined user)
- TestModule (Defined by user)

ProductionModule

```java
public class ProductionModule extends AbstractModule {
    // Example: a ProductionModule binds WarehouseImpl to Warehouse
    // Warehouse is the interface
    public void configure() {
        bind(Warehouse.class).to(WarehouseImpl.class);
    }
}
```

```java
public class InventorySystem {
    private static String TALISKER = "Talisker";
    private int totalStock;
    // No new anymore
    @Inject private Warehouse warehouse;
    public void addToWarehouse(String item, int amount) {
        warehouse.add(item, amount); totalStock += amount;
    }
    public int getTotalStock() {
        return totalStock;
    }
    public boolean processOrder(Order order) {
        order.fill(warehouse);
        return order.isFilled();
    }
    public static void main(String[] args) {
        // An injector is created: it allows to specify bindings of implementations
        // to interfaces → In this case it injects a ProductionModule
        Injector injector = Guice.createInjector(new ProductionModule());
        // Create an instance of InventorySystem needing the injection
        InventorySystem inventorySystem = injector.getInstance(InventorySystem.class);
        inventorySystem.addToWarehouse(TALISKER, 50);
        boolean order1success = inventorySystem.processOrder(new OrderImpl(TALISKER, 50));
        boolean order2success = inventorySystem.processOrder(new OrderImpl(TALISKER, 51));
        System.out.println("Order1 succeeded? " + order1success + " - Order2 succeeded?" + order2success);
    }
}
```

TestModule (for Unit Test)

```java
// Unit test that binds warehouse to a mock object
public class TestModule extends AbstractModule {
@Override
protected void configure() {
        Warehouse warehouseMock = EasyMock.createMock(Warehouse.class);
        bind(Warehouse.class).toInstance(warehouseMock);
    }
}

```

```java

class InventorySystemTest {
    private static String TALISKER = "Talisker";
    private InventorySystem inventorySystem;
    private Injector injector;
    @BeforeEach
    void setUp() throws Exception {
        // Tell Guice to create an injector using TestModule that binds Warehouse
        // to a WarehouseMock
        injector = Guice.createInjector(new TestModule());
        // Let Guice instantiate the InventorySystem and the Warehouse in it
        inventorySystem = injector.getInstance(InventorySystem.class);
    }
    @Test
    void addToWarehouse() {
        // Retrieve the WarehouseMock from the injector to use it during the test
        Warehouse warehouseMock = injector.getInstance(Warehouse.class);
        warehouseMock.add(TALISKER, 50);
        expectLastCall().andVoid();
        replay(warehouseMock);
        // Specified behavior in the test case
        inventorySystem.addToWarehouse(TALISKER, 50);
        assertEquals(inventorySystem.getTotalStock(), 50);
        // EasyMock validation
        verify(warehouseMock);
    }
}
```
