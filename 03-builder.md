# Builder Pattern

- Problem:
  ![problem](assets/builder-problem.png)
- Structure:
  - The client asks the director to construct
  - The client asks the builder to return the result
    ![builder](assets/builder.png)
- Focuses on constructing a complex object step by step. Every step returns a half-built object.
- Often builds a composite
- Design starts using Factory Method and evolves towards Builder/Abstract Factory

![builder-example](assets/builder-example.png)

```java
 public void buildSpecialBeefBurger(Builder<IngredientsList> builder) {
     builder.addBun(Bun.SESAME_BUN)
       .addPatty(Patty.BEEF_PATTY)
       .addPatty(Patty.BEEF_PATTY)
       .addSauce(Sauce.MAYO)
       .addSauce(Sauce.KETCHUP)
       .addSauce(Sauce.BBQ_SAUCE)
       .addCheese(Cheese.BRIE_CHEESE)
       .addCheese(Cheese.CHEDDAR_CHEESE)
       .addLettuce(Lettuce.ROMAINE_LETTUCE)
       .addPickle(Pickle.SPICY_SOUR_PICKLE)
       .addOnion(Onion.CARAMELIZED_ONION)
       .addTomato(Tomato.BEEFSTEAK_TOMATO);
 }
```
