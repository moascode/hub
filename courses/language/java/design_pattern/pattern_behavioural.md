# Behavioural Patterns

##

## Strategy Pattern  

*What?*  

The Strategy Pattern defines a family of algorithms, encapsulates them in separate classes, and makes them interchangeable at runtime.  

*Why?*  

- We want to select an algorithm dynamically without modifying the client code.  
- We want to follow the Open/Closed Principle by allowing new strategies to be added without modifying existing logic.  
- We want to avoid using multiple conditional statements (`if-else` or `switch`) for different behaviors.  

*But?*  

- It introduces additional classes, increasing complexity.  
- The client must be aware of different strategies and decide which one to use.  

### Diagram  

| ![Strategy](../_img/strategy.png) |
|:-----------------------------------------------------------------------------------------:|
| *Figure 1: Strategy pattern UML diagram*  

### Implementation  

- Define a common strategy interface.  

```java
interface CookingStrategy {
    void cook();
}
```

- Implement concrete strategies.  

```java
class GrilledCooking implements CookingStrategy {
    @Override
    public void cook() {
        System.out.println("Cooking burger on a grill.");
    }
}

class FriedCooking implements CookingStrategy {
    @Override
    public void cook() {
        System.out.println("Cooking burger in a frying pan.");
    }
}
```

- Create a context class that uses a strategy.  

```java
class Burger {
    private CookingStrategy cookingStrategy;

    public Burger(CookingStrategy cookingStrategy) {
        this.cookingStrategy = cookingStrategy;
    }

    public void setCookingStrategy(CookingStrategy cookingStrategy) {
        this.cookingStrategy = cookingStrategy;
    }

    public void cook() {
        cookingStrategy.cook();
    }
}
```

- Use the strategy pattern to change behavior dynamically.  

```java
// Usage
public class StrategyDemo {
    public static void main(String[] args) {
        Burger burger = new Burger(new GrilledCooking());
        burger.cook();

        // Change cooking strategy dynamically
        burger.setCookingStrategy(new FriedCooking());
        burger.cook();
    }
}
```

This approach enables dynamic selection of cooking strategies without modifying the `Burger` class.

### Usage in project

## Observer

## Observer Pattern  

*What?*  

The Observer Pattern establishes a one-to-many dependency between objects, where changes in one object (the **subject**) trigger updates in its dependent objects (the **observers**) automatically.  

*Why?*  

- We want to implement event-driven programming where multiple objects react to state changes in another object.  
- We want to decouple the subject and observers to allow independent evolution.  
- We want to enable multiple observers to dynamically subscribe and unsubscribe.  

*But?*  

- It can lead to memory leaks if observers are not properly removed.  
- Frequent updates might impact performance if there are too many observers.  

### Diagram  

| ![Observer](../_img/observer.png) |
|:-----------------------------------------------------------------------------------------:|
| *Figure 1: Observer pattern UML diagram*  

### Implementation  

- Define an **Observer** interface.  

```java
interface Observer {
    void update(String message);
}
```

- Define a **Subject** interface to manage observers.  

```java
interface Subject {
    void addObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers(String message);
}
```

- Implement a **Concrete Subject** (publisher).  

```java
import java.util.ArrayList;
import java.util.List;

class BurgerOrderSystem implements Subject {
    private List<Observer> observers = new ArrayList<>();

    @Override
    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }

    public void newOrder(String orderDetails) {
        System.out.println("New Order: " + orderDetails);
        notifyObservers("Order received: " + orderDetails);
    }
}
```

- Implement **Concrete Observers** (subscribers).  

```java
class Chef implements Observer {
    private String name;

    public Chef(String name) {
        this.name = name;
    }

    @Override
    public void update(String message) {
        System.out.println(name + " received order update: " + message);
    }
}

class Waiter implements Observer {
    @Override
    public void update(String message) {
        System.out.println("Waiter received order update: " + message);
    }
}
```

- Use the observer pattern to notify subscribers.  

```java
// Usage
public class ObserverDemo {
    public static void main(String[] args) {
        BurgerOrderSystem orderSystem = new BurgerOrderSystem();

        Observer chef1 = new Chef("Chef John");
        Observer chef2 = new Chef("Chef Lisa");
        Observer waiter = new Waiter();

        orderSystem.addObserver(chef1);
        orderSystem.addObserver(chef2);
        orderSystem.addObserver(waiter);

        orderSystem.newOrder("Cheeseburger with fries");

        orderSystem.removeObserver(chef2);

        orderSystem.newOrder("Vegan burger with salad");
    }
}
```

This approach ensures that all subscribed observers are notified when a new order is placed.

### Usage in project

##

## State Pattern  

*What?*  

The State Pattern allows an object to change its behavior dynamically based on its internal state, encapsulating state-specific behavior into separate classes.  

*Why?*  

- We want to avoid using multiple conditional statements (`if-else` or `switch`) to handle different states.  
- We want to make the system more maintainable by encapsulating state-specific logic in separate classes.  
- We want to follow the Single Responsibility Principle by delegating behavior to state classes.  

*But?*  

- It introduces additional classes, increasing complexity.  
- The transitions between states must be well-defined to avoid inconsistent behavior.  

### Diagram  

| ![State](../_img/state.png) |
|:-----------------------------------------------------------------------------------------:|
| *Figure 1: State pattern UML diagram*  

### Implementation  

- Define a common **State** interface.  

```java
interface BurgerState {
    void handleState(Burger burger);
}
```

- Implement concrete **State** classes.  

```java
class RawState implements BurgerState {
    @Override
    public void handleState(Burger burger) {
        System.out.println("Burger is raw. Cooking started...");
        burger.setState(new CookingState());
    }
}

class CookingState implements BurgerState {
    @Override
    public void handleState(Burger burger) {
        System.out.println("Burger is being cooked...");
        burger.setState(new ReadyState());
    }
}

class ReadyState implements BurgerState {
    @Override
    public void handleState(Burger burger) {
        System.out.println("Burger is ready to serve!");
    }
}
```

- Create a **Context** class that manages the state.  

```java
class Burger {
    private BurgerState state;

    public Burger() {
        this.state = new RawState(); // Initial state
    }

    public void setState(BurgerState state) {
        this.state = state;
    }

    public void nextState() {
        state.handleState(this);
    }
}
```

- Use the state pattern to transition between states.  

```java
// Usage
public class StateDemo {
    public static void main(String[] args) {
        Burger burger = new Burger();

        burger.nextState(); // Transition from Raw to Cooking
        burger.nextState(); // Transition from Cooking to Ready
        burger.nextState(); // Burger is Ready
    }
}
```

This approach ensures that `Burger` changes behavior dynamically based on its state without relying on conditional statements.

### Usage in project
