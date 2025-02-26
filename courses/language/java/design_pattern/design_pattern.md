# Design Pattern

## Creational Patterns

### Singleton

What?
A singleton ensures that only one instance of a class exists at any given time in an application.

Why?
- We want to have a shared state across the application. Ex: Configuration
- We don’t need multiple instances, and a single instance saves memory. Ex: Logger

But?
- The Singleton pattern is sometimes considered an anti-pattern because it violates the Single Responsibility Principle (SRP). The class is responsible for both its primary function and managing its own instantiation.
- Unit testing is difficult because of the shared state. Changes in one test may lead to inconsistencies in others.

Diagram:



Implementation:

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

#### Usage in project

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

### Factory Method

The factory method pattern delegates the responsibility of object instantiation to its concrete subclasses.

#### Advantage and Limitation

Given the factory method, we achieve the following design principles:

1. Encapsulate what varies

We encapsulated the creation of the concrete objects within a single method. This way, the creator classes can evolve without affecting the rest of the application. The object creation process can also change without affecting the rest of the client code.

2. Dependency Inversion Principle

Dependency Inversion Principle promotes loose coupling and says that clients (high-level modules) should interact with abstractions (interfaces), rather than concrete implementations (low-level modules).

Traditionally, the client would be interacting directly with the concrete implementation of the Burger and BurgerStore. But now a client can be provided a variety of BurgerStores at runtime. If we introduce a new kind of BurgerStore we won't need to update the client to accommodate it.

3. Open/Closed Principle

The factory method pattern allows for new types of products to be added without modifying any existing code or the factory itself. If a new product needs to be added, we can simply extend the base factory and implement the factory method for the new product type. The existing client code does not need to change.

Limitations and Pitfalls
Just like any other pattern, there are always pitfalls:

1. Increased Complexity

Adding the factory method requires the creation of additional classes and interfaces, which increases overhead as well. The code might become very complicated since we need to introduce a lot of new subclasses to implement the pattern.

In the example above, we only had two different kind of burgers per factory, but let's say we were designing a factory that produces jets with different models. This could lead to an explosion of classes.

2. Might be hard to refactor

We saw how meticulous we had to be with the set up of the factory method. The factory pattern is deeply embedded into our system and it will require a lot of effort to replace it if in the future we decide to use some other implementation.

#### Implementation



### Builder

### Prototype

## Structural Patterns

### Adapter

### Decorator

### Facade

## Behavioural Patterns

### Strategy

### Observer

### State