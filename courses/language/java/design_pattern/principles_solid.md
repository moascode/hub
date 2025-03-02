# SOLID Design Principles

Bad code slows down developers. Symptoms of bad code

- Introducing new features requires rewriting the code
- Changing the code breaks the application
- Fixing the code requires changes in many places

OO is about managing dependencies to prevent rigidity, fragility and non-reusability

## Summary

| **Principle**        | **Description** | **Key Idea** |
|----------------------|----------------|-------------|
| **Single Responsibility Principle (SRP)** | A class should have only one reason to change, meaning it should only have one job. | Keep each class focused on a single task to improve maintainability. |
| **Open/Closed Principle (OCP)** | Software entities (classes, modules, functions) should be open for extension but closed for modification. | Allow adding new functionality without altering existing code. |
| **Liskov Substitution Principle (LSP)** | Subtypes must be substitutable for their base types without altering the correctness of the program. | Derived classes should extend behavior without breaking parent class expectations. |
| **Interface Segregation Principle (ISP)** | Clients should not be forced to depend on interfaces they do not use. | Prefer small, specific interfaces over large, general ones. |
| **Dependency Inversion Principle (DIP)** | High-level modules should not depend on low-level modules. Both should depend on abstractions. | Depend on abstractions (interfaces) rather than concrete implementations. |


## Single Responsibility Principle (SRP)

"A class should have one, and only one, reason to change."

Payroll -> Employee
            + CalcPay
            + ReportHours
            + WriteEmployee
  
Employee has three responsibilities.

Payroll -> Employee
            + CalcPay
        -> ReportWriter
            + ReportHours
        -> EmployeeRepository
            + WriteEmployee

That's why a good code should have only a single reason to change.

## Open-Closed Principle (OCP)

"Modules should be open for extension, but closed for modification."

You should be able to change the behavior of the module without changing the module.
For new feature, extend the beahvior by writing new code instead of changing the existing code.

When developers tries to modify existing bad code, they may break the application. That's why a good code should be closed for modification but open for extension.

## Liskov Substitution Principle (LSP)

"Derived classes must be usable through the base class interface, without the need for the user to know the difference."

Client -> AbstractServer -> ConcreteServer

Square is not substitutable for rectangle..

Rectangle(Height, Width)
Square(Side)

Whenver LSP principle is violated, there is an 'If' statement checking the the instance of the object to prevent crashing the system.

Child class should always be substituted by it's base class.

## Interface Seggregation Principle (ISP)

Interface should not be too generic that many are forced to implement functionalities that are not required. It's best to have small, related and meaningful interfaces.

## Dependency Inversion Principle (DIP)

When developers try to fix a bug in one place, other breaks - leading to change in so many places. That's why code should not have concrete dependency on the implementation rather depend on abstractions.

High level module to call a low level module directly, it has a source code dependency. Change in dependent module forces to recompile all high level modules dependent on it. That's why high level modules should not depend on low level modules rather depend on interfaces.