# Object Oriented Programming

## inheritance

It is the process that enables one class to acquire the properties (methods and variables) of another. The class inheriting the properties of another is the subclass (also called derived class, or child class); the class whose properties are inherited is the superclass (base class, or parent class). To inherit from a class, use the extends keyword. A class can inherit from just one superclass, but can implement multiple interfaces!

    - inheriting members (fields and methods) from superclass
    - java supports only single inheritance to avoid diamond problem, but can implement multiple interfaces
    - all java classes inherit from java.lang.Object class, means Object is the only class without any parent
      - every class has access to methods defined in Object class (toString(), equals(), hashCode())

```java
public Class Animal {} //parent or superclass
public Class Mammal extends Animal {} //child or subclass
public Class Dog extends Mammal {} //transitive inheritance of Animal
```

## Encapsulation

To ensure that implementation details are not visible to users. The variables of one class will be hidden from the other classes, accessible only through the methods of the current class. This is called data hiding.

Getters && Setters: It is used to protect your data, particularly when creating classes. Getters and Setters must be made public and used only for manipulating PRIVATE variables. Getters and setters are fundamental building blocks for encapsulation

## Polymorphism

one method, with different implementations. There are two types of polymorphism in Java: compile-time polymorphism and runtime polymorphism. We can perform polymorphism in java by method overloading (compile time) and method overriding (runtime).

- Method overloading: Methods have the same name, but different parameters. Another name for method overloading is compile-time polymorphism.

- Method overriding: Implementation of same function from superclass to subclass.  Should have the same return type and arguments. The access level cannot be more restrictive than the overridden method.  A method declared final or static cannot be overridden.  If a method cannot be inherited, it cannot be overridden. Method overriding is also known as runtime polymorphism.

- method overloading: same method name, different parameters (number of parameters/ type)
  - If exact method not found, java will look for method with primitive type
  - If primitive method found, java will look for larger primitive type
  - If primitive method not found, java will do autoboxing to wrapper type
  - If exact wrapper type not found, java will look for immediate super type (ex: last resort is Object)
- method overriding: same method, different implementation in subclasses
  
## Abstraction

Data abstraction provides the outside world with only essential information without including implementation details. Abstraction is achieved using abstract classes and interfaces.

Abstract class: An abstract class is defined using the abstract keyword. If a class is declared abstract it cannot be instantiated (you cannot create objects of that type), but they can be subclassed. To use an abstract class, you have to inherit it from another class. Any class that contains an abstract method should be defined as abstract. An abstract class may or may not include abstract methods, if a method is not abstract, implementation can be done within the class. When an abstract class is subclassed, the subclass usually provides implementations for all of the abstract methods in its parent class.

abstract class can have constrcutor but can only called from subclass using super().
abstract method can not be private, final or static.

abstract classes are very useful, because in Java you can inherit just one super class, implementation of multiple abstract classes makes it easier to overcome the problem.

```java
abstract class Animal {
  int legs = 0;
  abstract void makeSound();
}
class Cat extends Animal {
  public void makeSound() {
    System.out.println("Meow");
  }
}
```

Abstract method: An abstract method is a method that is declared without an implementation (without braces, and followed by a semicolon): abstract void walk();

## interface

binding contract

An interface is a completely abstract class that contains only abstract methods. - Defined using the interface keyword.- May contain only static final variables.- Cannot contain a constructor because interfaces cannot be instantiated.- Interfaces can extend other interfaces.- A class can implement any number of interfaces. Use the implements keyword to use an interface with your class. When you implement an interface, you need to override all of its methods.

- An interface is implicitly abstract. You do not need to use the abstract keyword while declaring an interface.
- Each method in an interface is also implicitly abstract, so the abstract keyword is not needed.
- Methods in an interface are implicitly public.
- Interface can have static method but can not be overriden
- Interface can have private method and can only be used within the interface
- default and private non-static method can call abstract methods in the interface

```java
interface Animal {
  public void eat();
  public void makeSound();
}

class Cat implements Animal {
  public void makeSound() {
    System.out.println("Meow");
  }
  public void eat() {
    System.out.println("omnomnom");
  }
}
```

An interface with single abstract method is called functional interface. Lambda Expressions in Java 8: lambda expression to implement functional interface

```java
FuncInterface fobj = (int x)->System.out.println(2*x); 
```
