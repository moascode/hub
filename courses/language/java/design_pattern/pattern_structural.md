# Structural Patterns

## Adapter

## Adapter Pattern  

*What?*  

The Adapter Pattern allows incompatible interfaces to work together by providing a wrapper that translates requests from one interface to another.  

*Why?*  

- We want to integrate existing classes with incompatible interfaces without modifying their code.  
- We want to follow the Open/Closed Principle by extending functionality without altering existing classes.  
- We want to reuse legacy code while adapting it to fit a new system.  

*But?*  

- It introduces an extra layer of abstraction, which can add complexity.  
- It might impact performance due to additional method delegation.  

### Diagram  

| ![Adapter](../_img/adapter.png) |
|:-----------------------------------------------------------------------------------------:|
| *Figure 1: Adapter pattern UML diagram*  

### Implementation  

- Define a target interface that the client expects.  

```java
interface NewBurgerMachine {
    void makeBurger();
}
```

- Create an **adaptee** (existing class with an incompatible interface).  

```java
class OldBurgerMachine {
    void prepareBurger() {
        System.out.println("Burger is being prepared using the old machine.");
    }
}
```

- Implement an adapter class that bridges the adaptee and the target interface.  

```java
class BurgerMachineAdapter implements NewBurgerMachine {
    private OldBurgerMachine oldMachine;

    public BurgerMachineAdapter(OldBurgerMachine oldMachine) {
        this.oldMachine = oldMachine;
    }

    @Override
    public void makeBurger() {
        oldMachine.prepareBurger(); // Adapting the method call
    }
}
```

- Use the adapter to make the old class compatible with the new interface.  

```java
// Usage
public class AdapterDemo {
    public static void main(String[] args) {
        OldBurgerMachine oldMachine = new OldBurgerMachine();
        NewBurgerMachine adaptedMachine = new BurgerMachineAdapter(oldMachine);

        adaptedMachine.makeBurger(); // Works with the new interface
    }
}
```

### Usage in project

## Decorator

*What?*

## Decorator Pattern  

*What?*  

The Decorator Pattern dynamically adds new behavior to objects by wrapping them in a decorator class without modifying their original code.  

*Why?*  

- We want to extend an object’s functionality dynamically at runtime rather than through inheritance.  
- We want to follow the Open/Closed Principle by allowing modifications without changing existing code.  
- We want to avoid creating numerous subclasses to handle different feature combinations.  

*But?*  

- It can increase complexity due to multiple layers of wrapping.  
- Debugging might become difficult as behavior is distributed across multiple decorators.  

### Diagram  

| ![Decorator](../_img/decorator.png) |
|:-----------------------------------------------------------------------------------------:|
| *Figure 1: Decorator pattern UML diagram*  

### Implementation  

- Define a common interface for both the base component and decorators.  

```java
interface Burger {
    void prepare();
}
```

- Create a concrete component (the object to be decorated).  

```java
class BasicBurger implements Burger {
    @Override
    public void prepare() {
        System.out.println("Preparing a basic burger.");
    }
}
```

- Create an abstract decorator that wraps a `Burger` instance.  

```java
abstract class BurgerDecorator implements Burger {
    protected Burger decoratedBurger;

    public BurgerDecorator(Burger burger) {
        this.decoratedBurger = burger;
    }

    @Override
    public void prepare() {
        decoratedBurger.prepare();
    }
}
```

- Implement concrete decorators that extend functionality.  

```java
class CheeseDecorator extends BurgerDecorator {
    public CheeseDecorator(Burger burger) {
        super(burger);
    }

    @Override
    public void prepare() {
        super.prepare();
        System.out.println("Adding cheese.");
    }
}

class LettuceDecorator extends BurgerDecorator {
    public LettuceDecorator(Burger burger) {
        super(burger);
    }

    @Override
    public void prepare() {
        super.prepare();
        System.out.println("Adding lettuce.");
    }
}
```

- Use the decorator to add features dynamically.  

```java
// Usage
public class DecoratorDemo {
    public static void main(String[] args) {
        Burger burger = new BasicBurger();
        burger = new CheeseDecorator(burger);
        burger = new LettuceDecorator(burger);

        burger.prepare();
    }
}
```

### Usage in project

## Facade

## Facade Pattern  

*What?*  

The Facade Pattern provides a simplified, unified interface to a complex system of classes, making it easier to use.  

*Why?*  

- We want to hide the complexity of a subsystem and provide a clean, easy-to-use API.  
- We want to improve maintainability by centralizing access to multiple components.  
- We want to decouple clients from implementation details of a subsystem.  

*But?*  

- It might introduce a single point of failure if the facade becomes too complex.  
- It can limit flexibility if the facade does not expose all necessary functionality.  

### Diagram  

| ![Facade](../_img/facade.png) |
|:-----------------------------------------------------------------------------------------:|
| *Figure 1: Facade pattern UML diagram*  

### Implementation  

- Define complex subsystem components.  

```java
class BunMaker {
    void prepareBun() {
        System.out.println("Bun is prepared.");
    }
}

class PattyCooker {
    void cookPatty() {
        System.out.println("Patty is cooked.");
    }
}

class ToppingsAdder {
    void addToppings() {
        System.out.println("Toppings are added.");
    }
}
```

- Create a **facade** that simplifies interactions with the subsystem.  

```java
class BurgerFacade {
    private BunMaker bunMaker;
    private PattyCooker pattyCooker;
    private ToppingsAdder toppingsAdder;

    public BurgerFacade() {
        this.bunMaker = new BunMaker();
        this.pattyCooker = new PattyCooker();
        this.toppingsAdder = new ToppingsAdder();
    }

    public void makeBurger() {
        bunMaker.prepareBun();
        pattyCooker.cookPatty();
        toppingsAdder.addToppings();
        System.out.println("Burger is ready to serve.");
    }
}
```

- Use the facade to interact with the system in a simplified way.  

```java
// Usage
public class FacadeDemo {
    public static void main(String[] args) {
        BurgerFacade burgerFacade = new BurgerFacade();
        burgerFacade.makeBurger();
    }
}
```

### Usage in project
