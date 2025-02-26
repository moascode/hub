# Creational Patterns

## Singleton

### What?

A singleton ensures that only one instance of a class exists at any given time in an application.

### Why?
- We want to have a shared state across the application. Ex: Configuration
- We don’t need multiple instances, and a single instance saves memory. Ex: Logger

### But?
- The Singleton pattern is sometimes considered an anti-pattern because it violates the Single Responsibility Principle (SRP). The class is responsible for both its primary function and managing its own instantiation.
- Unit testing is difficult because of the shared state. Changes in one test may lead to inconsistencies in others.

### Diagram:

| ![Singleton](../_img/singleton.png) |
|:-----------------------------------------------------------------------------------------:|
| *Figure 1: Singleton pattern UML diagram*

### Implementation:

- Make constructor private to prevent any instantiation of the class with 'new' keyword
- Create a static variable to hold the single instance and create a method to provide the instance of the class. Static so that this method is accessible without any instance
```java
public class EagerSingleton {
    private static final EagerSingleton INSTANCE = new EagerSingleton();
    private EagerSingleton() { }
    public static EagerSingleton getInstance() {
        return INSTANCE;
    }
}
```
- This will create the instance at the application startup (Eager initilization). There is a possibility that this instance is not immediately needed. We can create the instance when it's necessary to improve application startup (Lazy initialization).
```java
public class LazySingleton {
    private static LazySingleton instance;
    private LazySingleton() { }
    public static LazySingleton getInstance() {
        if (instance == null) {
            instance = new LazySingleton();
        }
        return instance;
    }
}
```
- Above implementation is not thread safe. Multiple threads can access the method at the same time and create more than one instance which violats the pattern. We need to make it thread safe.
```java
public class LazySingleton {
    private static LazySingleton instance;
    private LazySingleton() { }
    public static synchronized LazySingleton getInstance() {
        if (instance == null) {
            instance = new LazySingleton();
        }
        return instance;
    }
}
```
- This introduces performace overhead as synchronization slows down access to the instance and reduces efficiency in high-concurrency applications. We can leverages Java's class loading mechanism to maintain thread-safety and efficiency.
```java
public class HolderSingleton {
    private HolderSingleton() { }
    private static class SingletonHolder {
        private static final HolderSingleton INSTANCE = new HolderSingleton();
    }
    public static HolderSingleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

### Usage in project

Created a single instance for DateAndTimeProvider class that provides a specific implementation of the date and time.

```java
static DateAndTimeProvider getInstance() {
    return ServiceProvider.INSTANCE;
}

final class ServiceProvider {
    private static final DateAndTimeProvider INSTANCE = Lookup.getDefault().lookup(DateAndTimeProvider.class);

    private ServiceProvider() {}
}
```

Created a single instance for OptimizerProperties, but also made sure that the instance can be updated dynamically by using AtomicReference. Ex: default optimizer properties if no properties file provided.

```java
private static final AtomicReference<OptimizerProperties> INSTANCE = new AtomicReference<>();

public static OptimizerProperties getInstance() {
    return INSTANCE.updateAndGet(instance -> instance != null ? instance : newInstance());
}

public static OptimizerProperties newInstance() {
    try {
        final ResourceBundle rb = ResourceBundle.getBundle("optimizer");
        return new OptimizerProperties(rb);
    } catch (MissingResourceException e) {
        log.warn("optimizer properties not found: " + e.getMessage());
        return new OptimizerProperties();
    }
}
```

## Factory Method

### What?

A Factory Method abstracts away the details of object creation by delegating it to subclasses.

### Why?
- We want to encapsulate object creation that allows new types to be added without modifying existing code, promoting the Open/Closed Principle.
- We want to enables loose coupling, making it easier to swap implementations and use dependency injection.

### But?
- It introduces additional complexity by requiring extra classes and interfaces.
- It might be hard to refactor  if switching to a different pattern later.

### Diagram

| ![Singleton](../_img/factory.png) |
|:-----------------------------------------------------------------------------------------:|
| *Figure 1: Factory pattern UML diagram*

### Implementation
- A concrete interface and class define the objects to be instantiated using the factory pattern.
```java
//Concrete interface
interface Burger {
  void prepare() {}
  void cook() {}
  void serve() {}
}
//Concrete classes
class CheeseBurger implements Burger {
  CheeseBurger(Ingredients ingredient){}
  // ...
}
class VeganBurger implements Burger {
  VeganBurger(Ingredients ingredient){}
  // ...
}
```
- A Creator Interface or Abstract Class declares the factory method.
```java
interface BurgerFactory {
  Burger createBurger();
}
```
- Factory classes implement the factory method to create instances of specific types while returning the interface for loose coupling.
```java
class CheeseBurgerFactory implements BurgerFactory {
  Burger createBurger() {
    Ingredient ingredient = new CheeseBurgerIngredient();
    return new CheeseBurger(ingredient);
  }
}
class VeganBurgerFactory implements BurgerFactory {
  Burger createBurger() {
    Ingredient ingredient = new VeganBurgerIngredient();
    return new VeganBurger(ingredient);
  }
}
//Usage
BurgerFactory burgerFactory = new CheeseBurgerFactory();
Burger burger = burgerFactory.createBurger();
```
### Usage in project


## Builder
### What?

### Why?

### But?

### Diagram

### Implementation

### Usage in project

## Prototype
### What?

### Why?

### But?

### Diagram

### Implementation

### Usage in project