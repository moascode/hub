# Design Pattern

## Design pattern questions

Below are some basic design pattern questions:

---

### **1. What is the Singleton Pattern? Can you explain its use cases and how it is implemented in Java?**

**Answer:**  
The **Singleton Pattern** ensures that a class has only one instance and provides a global point of access to that instance. It is commonly used for managing shared resources, like database connections or configuration settings.  
**Implementation in Java:**

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

---

### **2. What is the Factory Method Pattern? How does it differ from the Abstract Factory Pattern?**

**Answer:**  
The **Factory Method Pattern** defines an interface for creating objects, but lets subclasses decide which class to instantiate.  
**Difference with Abstract Factory**:

- **Factory Method**: Involves creating a single product.
- **Abstract Factory**: Used when there are multiple product families, and it provides an interface for creating related objects.

---

### **3. Explain the Builder Pattern and its application in Java.**

**Answer:**  
The **Builder Pattern** separates the construction of a complex object from its representation, allowing the same construction process to create different representations. It is useful for constructing objects with many parameters or optional fields.  
**Example:**

```java
public class Car {
    private String engine;
    private String wheels;
    
    // Private constructor to be used by the Builder
    private Car(CarBuilder builder) {
        this.engine = builder.engine;
        this.wheels = builder.wheels;
    }

    public static class CarBuilder {
        private String engine;
        private String wheels;

        public CarBuilder setEngine(String engine) {
            this.engine = engine;
            return this;
        }

        public CarBuilder setWheels(String wheels) {
            this.wheels = wheels;
            return this;
        }

        public Car build() {
            return new Car(this);
        }
    }
}
```

---

### **4. What is the Observer Pattern? How do you implement it in Java?**

**Answer:**  
The **Observer Pattern** allows an object (subject) to notify multiple observer objects when its state changes, without knowing who or what is observing it.  
**Implementation in Java:**

```java
interface Observer {
    void update(String message);
}

class ConcreteObserver implements Observer {
    private String name;
    
    public ConcreteObserver(String name) {
        this.name = name;
    }

    @Override
    public void update(String message) {
        System.out.println(name + " received: " + message);
    }
}

class Subject {
    private List<Observer> observers = new ArrayList<>();
    
    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}
```

---

### **5. What is the Strategy Pattern? Can you explain how it works in Java?**

**Answer:**  
The **Strategy Pattern** allows you to define a family of algorithms, encapsulate each one, and make them interchangeable. It helps in making the code more flexible and allows changing the algorithm without modifying the context class.  
**Example:**

```java
interface PaymentStrategy {
    void pay();
}

class CreditCardPayment implements PaymentStrategy {
    @Override
    public void pay() {
        System.out.println("Paying with credit card.");
    }
}

class PayPalPayment implements PaymentStrategy {
    @Override
    public void pay() {
        System.out.println("Paying with PayPal.");
    }
}

class ShoppingCart {
    private PaymentStrategy paymentStrategy;
    
    public ShoppingCart(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void checkout() {
        paymentStrategy.pay();
    }
}
```

---

### **6. What is the Decorator Pattern? How does it differ from the Proxy Pattern?**

**Answer:**  
The **Decorator Pattern** allows you to add behavior to an object dynamically, without modifying its structure.  
**Difference with Proxy Pattern**:

- **Decorator**: Adds additional functionality to an object at runtime.
- **Proxy**: Provides a surrogate or placeholder for another object, controlling access to it.

---

### **7. What is the Adapter Pattern? Provide an example of when it might be useful.**

**Answer:**  
The **Adapter Pattern** allows incompatible interfaces to work together by providing a wrapper around one of the interfaces. It’s useful when you have a third-party library with a different interface but you want to integrate it into your system.  
**Example:**

```java
interface MediaPlayer {
    void play(String fileName);
}

class AudioPlayer implements MediaPlayer {
    @Override
    public void play(String fileName) {
        System.out.println("Playing audio file: " + fileName);
    }
}

interface AdvancedMediaPlayer {
    void playAdvanced(String fileName);
}

class VideoPlayer implements AdvancedMediaPlayer {
    @Override
    public void playAdvanced(String fileName) {
        System.out.println("Playing video file: " + fileName);
    }
}

class MediaAdapter implements MediaPlayer {
    private AdvancedMediaPlayer advancedMediaPlayer;

    public MediaAdapter(AdvancedMediaPlayer advancedMediaPlayer) {
        this.advancedMediaPlayer = advancedMediaPlayer;
    }

    @Override
    public void play(String fileName) {
        advancedMediaPlayer.playAdvanced(fileName);
    }
}
```

---

### **8. Explain the Proxy Pattern with an example.**

**Answer:**  
The **Proxy Pattern** involves providing a surrogate or placeholder for another object to control access to it. This can be useful for lazy loading, access control, or logging.  
**Example:**

```java
interface RealSubject {
    void request();
}

class RealSubjectImpl implements RealSubject {
    @Override
    public void request() {
        System.out.println("Request made to the real subject.");
    }
}

class Proxy implements RealSubject {
    private RealSubjectImpl realSubject;

    @Override
    public void request() {
        if (realSubject == null) {
            realSubject = new RealSubjectImpl();
        }
        realSubject.request();
    }
}
```

---

### **9. What is the Command Pattern, and how is it implemented in Java?**

**Answer:**  
The **Command Pattern** encapsulates a request as an object, thereby allowing parameterization of clients with queues, requests, and operations. It decouples the sender of a request from the object that handles the request.  
**Example:**

```java
interface Command {
    void execute();
}

class Light {
    void turnOn() {
        System.out.println("Light is ON");
    }

    void turnOff() {
        System.out.println("Light is OFF");
    }
}

class TurnOnCommand implements Command {
    private Light light;

    public TurnOnCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOn();
    }
}
```

---

### **10. What is the State Pattern? How is it useful in object-oriented design?**

**Answer:**  
The **State Pattern** allows an object to change its behavior when its internal state changes, making the object appear to change its class. It’s useful for managing state-dependent behavior without creating large conditional statements.  
**Example:**  
A simple example could be a **Traffic Light** system where the light changes its behavior (color) based on its state (green, yellow, red).

---

### **11. Can you explain the Chain of Responsibility Pattern and its Java implementation?**

**Answer:**  
The **Chain of Responsibility Pattern** allows a request to be passed along a chain of handlers, where each handler either processes the request or passes it on to the next handler. It decouples senders and receivers of requests.  
**Example:**

```java
abstract class Handler {
    protected Handler next;

    public void setNext(Handler next) {
        this.next = next;
    }

    public abstract void handleRequest(String request);
}

class ConcreteHandlerA extends Handler {
    @Override
    public void handleRequest(String request) {
        if (request.equals("A")) {
            System.out.println("Handled by A");
        } else if (next != null) {
            next.handleRequest(request);
        }
    }
}
```

---

### **12. What is the Composite Pattern? When would you use it?**

**Answer:**  
The **Composite Pattern** allows you to treat individual objects and compositions of objects uniformly. It’s particularly useful when working with tree-like structures.  
For example, it can be used in graphical systems where both individual shapes and groups of shapes need to be treated the same way.

---

### **13. What is the Memento Pattern? How does it help in undo functionality?**

**Answer:**  
The **Memento Pattern** allows you to capture and externalize an object's internal state without violating encapsulation, and allows restoring it later. It's useful in scenarios where undo functionality is needed.  
**Example:**  
An application that allows users to undo changes to a document could store the state of the document in a **memento** object.

---

### **14. What is the Interpreter Pattern? Provide a real-world example.**

**Answer:**  
The **Interpreter Pattern** defines a representation for a language's grammar and uses an interpreter to interpret sentences in the language. It’s useful for designing systems that involve parsing and interpreting expressions.  
**Example:**  
A simple **calculator** that interprets mathematical expressions like "3 + 4" using the Interpreter Pattern.

---

### **15. How do Design Patterns improve code flexibility and maintainability?**

**Answer:**  
Design Patterns provide reusable solutions to common problems, enabling developers to use proven strategies to solve issues. By following design patterns, code becomes more flexible, easier to extend, and easier to maintain. Additionally, it promotes consistency across the codebase, making it easier for other developers to understand and work with.

---

These questions cover some of the most widely used design patterns in Java and give insight into how each pattern can be applied effectively in software development.

## Design principle questions

Below are are some basic questions that focus on **Clean Code** concepts, as described by Robert C. Martin, including the **SOLID design principles**, **code simplicity**, **code readability**, and **software design principles**.

---

### **1. What are the SOLID design principles, and why are they important in Clean Code?**

**Answer:**  
SOLID is an acronym for five design principles that aim to make software more understandable, flexible, and maintainable:

- **S**ingle Responsibility Principle (SRP): A class should have only one reason to change.
- **O**pen/Closed Principle (OCP): Software entities (classes, modules, functions) should be open for extension, but closed for modification.
- **L**iskov Substitution Principle (LSP): Subtypes must be substitutable for their base types without altering the correctness of the program.
- **I**nterface Segregation Principle (ISP): Clients should not be forced to depend on interfaces they don't use.
- **D**ependency Inversion Principle (DIP): High-level modules should not depend on low-level modules. Both should depend on abstractions.

These principles help in building systems that are easier to maintain and extend over time.

---

### **2. How does the Single Responsibility Principle (SRP) contribute to Clean Code?**

**Answer:**  
SRP ensures that a class has only one reason to change. This makes code **more modular**, **easier to understand**, and **less prone to bugs**. For example, if a class handles both data persistence and UI logic, changes in the UI logic could inadvertently affect data persistence, leading to a tightly coupled design. Refactoring such classes into separate classes for each responsibility improves maintainability.

---

### **3. What is the Open/Closed Principle (OCP), and how does it help in software design?**

**Answer:**  
The **Open/Closed Principle** states that a class should be open for extension but closed for modification. This allows new functionality to be added to the system without modifying the existing code. For example, you can extend the functionality of a `Shape` class by adding subclasses (like `Circle`, `Rectangle`), without modifying the `Shape` class itself.

---

### **4. What is the Liskov Substitution Principle (LSP), and why is it important?**

**Answer:**  
The **Liskov Substitution Principle** ensures that derived classes can be used interchangeably with their base classes without affecting the correctness of the program. If derived classes violate LSP, the program might behave unexpectedly. For example, overriding a method in a subclass should not change the expected behavior of the base class method.

---

### **5. How do you apply the Interface Segregation Principle (ISP) in Clean Code?**

**Answer:**  
The **Interface Segregation Principle** states that no client should be forced to depend on methods it does not use. To apply this, avoid creating large, monolithic interfaces. Instead, break them down into smaller, more specialized interfaces. For example, instead of having a `Vehicle` interface with methods like `start()`, `stop()`, `fly()`, create separate interfaces like `Drivable` and `Flyable`.

---

### **6. What is the Dependency Inversion Principle (DIP), and how does it improve flexibility?**

**Answer:**  
The **Dependency Inversion Principle** dictates that high-level modules should not depend on low-level modules, but both should depend on abstractions. This improves flexibility by decoupling components and makes the system easier to extend and maintain. For instance, instead of directly using `new` to create objects, you can inject dependencies via constructors or setters (Dependency Injection).

---

### **7. How does the use of meaningful variable and function names contribute to code readability?**

**Answer:**  
Meaningful variable and function names help readers understand the purpose of the code at a glance. For example, using `calculateTotalPrice()` is far clearer than `doStuff()`. It reduces the need for comments, making the code self-documenting and easier to maintain.

---

### **8. What are magic numbers, and why should they be avoided in Clean Code?**

**Answer:**  
**Magic numbers** are hardcoded numeric values that appear without explanation, making the code hard to understand and maintain. Instead, use named constants or enums. For example:

```java
// Bad: Magic Number
if (age >= 18) { ... }

// Good: Named Constant
if (age >= ADULT_AGE) { ... }
```

This makes the code more readable and maintainable.

---

### **9. What does it mean to keep functions small, and why is it important?**

**Answer:**  
**Small functions** are easier to read, test, and maintain. Each function should do **one thing** and do it well. This adheres to the **Single Responsibility Principle (SRP)** and avoids large, complex methods that can be difficult to debug and understand. Functions should generally be kept to around **20-30 lines**.

---

### **10. How does the use of comments impact Clean Code?**

**Answer:**  
While comments can be helpful, Clean Code emphasizes **writing code that is self-explanatory**. Comments should be used to explain why something is done (e.g., business logic), but **not to explain what the code is doing** (which should be clear from the code itself). Avoid redundant or obvious comments like `// increment i by 1`.

---

### **11. What is the "Don't Repeat Yourself" (DRY) principle?**

**Answer:**  
The **DRY** principle emphasizes that each piece of knowledge or logic should have a single representation in the system. Avoid duplicating code, as it increases the chances of bugs and makes the system harder to maintain. Reusable code can be created using functions, classes, or modules to abstract repeated logic.

---

### **12. How can you use abstraction to simplify complex systems?**

**Answer:**  
Abstraction hides unnecessary details and exposes only the essential parts of the system. This helps simplify complex systems by breaking them into smaller, more manageable pieces. For example, a **service layer** can abstract business logic from data access, making the code easier to test and modify.

---

### **13. How do you apply the Law of Demeter (Principle of Least Knowledge) in your design?**

**Answer:**  
The **Law of Demeter** suggests that an object should only communicate with its **direct dependencies** and avoid reaching out to objects of its dependencies. This minimizes the coupling between components and makes the code easier to understand and modify. For example:

```java
// Bad: Chain of method calls
customer.getAddress().getStreet().getZipCode();

// Good: Direct communication with necessary methods
customer.getZipCode();
```

---

### **14. What are the benefits of using Dependency Injection (DI) in Clean Code?**

**Answer:**  
**Dependency Injection** (DI) decouples the creation of dependencies from the classes that use them. This makes the code more flexible, easier to test, and easier to maintain. DI helps adhere to the **Dependency Inversion Principle (DIP)** and makes components more reusable.

---

### **15. How can you refactor large classes or functions to adhere to Clean Code principles?**

**Answer:**  
Refactor large classes or functions by:

- **Extracting smaller methods** or **classes** that handle specific responsibilities.
- Following the **Single Responsibility Principle (SRP)** and making sure each class or method has one clear purpose.
- Using **composition** over inheritance when appropriate to keep the code modular and flexible.

---

### **16. What is the purpose of using interfaces in object-oriented design?**

**Answer:**  
**Interfaces** provide a way to define common behavior without specifying the details of implementation. They allow **decoupling** between components, enabling flexibility and making the system easier to extend. They also promote the **Dependency Inversion Principle (DIP)** by allowing classes to depend on abstractions rather than concrete implementations.

---

### **17. Why is it important to handle exceptions properly in Clean Code?**

**Answer:**  
Proper exception handling improves the robustness and maintainability of the code. Avoid **catching general exceptions** and provide meaningful error messages. It's important to follow the principle of **failing fast**, so exceptions should be thrown early and caught at the appropriate levels in the code.

---

### **18. How does test-driven development (TDD) contribute to Clean Code?**

**Answer:**  
**TDD** encourages writing tests before writing the code, ensuring that the code is written to be **testable** and **modular**. It helps in **refactoring safely** and ensures that the system is always working as expected. TDD also leads to smaller, more focused functions, promoting **Single Responsibility** and **Code Readability**.

---

### **19. How do you balance between adhering to design principles and keeping code simple?**

**Answer:**  
While it's important to follow design principles, simplicity should always be the goal. If adhering to a principle makes the code more complicated than necessary, it’s better to refactor and find a simpler solution. The goal is **elegant simplicity**, which makes the system maintainable without sacrificing important design principles.

---

### **20. What is "Code Smell," and how do you detect it?**

**Answer:**  
**Code Smell** refers to any indication that something might be wrong with the code. Common examples include:

- Long methods or classes.
- Duplicated code.
- Overuse of comments.
- Poorly named variables/functions.
Detecting code smells helps identify areas that might need refactoring or improvement.
