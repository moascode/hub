# Design Pattern

## Summary

| **Category**       | **Pattern**      | **Description** |
|--------------------|----------------|----------------|
| **Creational** <br> (*Deals with object creation mechanisms, increasing flexibility and reuse of code.*) | **Singleton**   | Ensures only one instance of a class exists, providing a global access point. |
|                    | **Factory Method** | Defines an interface for creating objects but lets subclasses decide which to instantiate. |
|                    | **Builder**     | Constructs complex objects step-by-step, separating object creation from its representation. |
|                    | **Prototype**   | Creates new objects by cloning existing instances, useful for expensive object creation. |
| **Structural** <br> (*Focuses on composing classes and objects to form larger structures while keeping the system flexible and efficient.*) | **Adapter**     | Bridges two incompatible interfaces, allowing them to work together without modification. |
|                    | **Decorator**   | Dynamically adds behavior to objects at runtime without modifying their structure. |
|                    | **Facade**      | Simplifies interactions with a complex system by providing a unified, high-level interface. |
| **Behavioural** <br> (*Concerns communication between objects, defining how they interact and distribute responsibilities.*) | **Strategy**    | Encapsulates interchangeable algorithms in separate classes, allowing dynamic selection. |
|                    | **Observer**    | Establishes a one-to-many dependency where observers react to subject state changes. |
|                    | **State**       | Allows an object to change behavior dynamically by transitioning between different states. |

### **Difference Between Design Patterns and Design Principles**  

| **Aspect**        | **Design Principles** | **Design Patterns** |
|------------------|--------------------|----------------|
| **What it is**   | General guidelines for writing clean, maintainable, and scalable code. | Reusable solutions to common software design problems. |
| **Purpose**      | Helps in designing flexible and loosely coupled systems. | Provides predefined templates for solving specific software problems. |
| **Scope**        | High-level concepts applicable across various designs and architectures. | Concrete implementations that can be directly used in coding. |
| **Flexibility**  | More abstract and broad, influencing the overall structure of a system. | More specific and structured, with well-defined implementations. |
| **Examples**     | SOLID Principles, DRY (Don't Repeat Yourself), KISS (Keep It Simple, Stupid). | Singleton, Factory Method, Observer, Strategy, Adapter, etc. |
| **Usage**        | Used as a foundation for designing robust and maintainable software. | Applied to solve recurring software design problems effectively. |

**Analogy:**  

- **Design principles** are like **rules of good writing** (e.g., "use proper grammar, avoid redundancy").  
- **Design patterns** are like **common writing structures** (e.g., "use the five-paragraph essay format").  

Both are essential for designing high-quality software, but principles guide how to think, while patterns provide ready-made solutions.
