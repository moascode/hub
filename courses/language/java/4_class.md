# Class

A **class** is a blueprint for creating objects. It defines behavior (methods) and attributes (fields or variables).  

---

## Class Members

### 1. Fields (Variables)

Fields represent data or state within a class. Setter methods can be used to set field values.

#### Types of Fields  

- **Local Variable**
  
  - Must be initialized before use.  
  - Can only be marked as `final`.  
  - Can be **effectively final** if its value is not modified after initialization.  

- **Instance Variable**
  
  - Automatically assigned default values if not initialized.  
  - Can have all access modifiers: `private`, `protected`, `public`.  
  - Can be marked as `final`, `volatile`, or `transient`.  
  - A `final` variable must be intialized inline or using constructor

- **Varargs (Variable Arguments)**
  
  - Accepts any number of parameters of the same type.  
  - Only one varargs parameter is allowed, and it must be the last parameter.  
  - Arrays can be passed to varargs.  

### 2. Methods

A method performs actions defined by its body. **Method Signature** includes the method's name, the number and types of parameters, and the return type.  

---

## Constructor

Constructors are special methods invoked when an object is created and are used to initialize object attributes. It must be same with class name and no return type. The constructor is called when you create an object using the new keyword. A single class can have multiple constructors with different numbers of parameters. The setter methods inside the class can be used to set the attribute values. Java automatically provides a default constructor, so all classes have a constructor. Constructors are not inherited by subclasses. All the constructor of the superclass/superclasses is called when the subclass is instantiated.

**Super**:  if you want to pass arguments to superclass' constructor then you must use Super(var). To access a variable of super class - Supar.var

```java
public class Animal {
    Animal(String name) {
        System.out.println("Animal name is: " + name);
    }
}

public class Dog extends Animal {
    Dog() {
        super("Dog");
    }
}
```

---

## Objects

An object is an instance of a class. Variables hold **references** to objects, not the actual object itself.

### Object Comparison

- `==`: Compares object references (not values).  
- `.equals()`: Compares object values for equality.  
- The automatically generated hashCode() method is used to determine where to store the object internally.
- Whenever you implement equals, you MUST also implement hashCode.

Example of overriding `equals()`:

```java
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    Person person = (Person) o;
    return Objects.equals(firstName, person.firstName) && Objects.equals(lastName, person.lastName);
}
```

### Type Casting

Java supports automatic type casting of integers to floating points, since there is no loss of precision. On the other hand, type casting is mandatory when assigning floating point values to integer variables.

- **Upcasting**: Casting an object of a subclass to its superclass is called Upcasting. Animal a = new Cat();
- **Downcasting**: Casting an object of a superclass to its subclass is called downcasting.

---

## Class Types

### JDK-Defined Classes

- **`Math` Class**:  
  - `Math.abs(x)`: Absolute value.  
  - `Math.max(a, b)`: Maximum of two values.  
  - `Math.pow(a, b)`: `a` raised to the power `b`.  
  - `Math.sqrt(x)`: Square root.

---

### Special Classes

#### Anonymous Classes

Allows creating subclasses on the fly with overridden methods. The modification on the overriden method is applicable only to the current object, and not the class itself.

```java
Machine m = new Machine() {
    @Override
    public void start() {
        System.out.println("Wooooo");
    }
};
m.start();  // Outputs "Wooooo"
```

#### Inner Classes

A class within another class. It Can be private, providing encapsulation. Once you declare an inner class private, it cannot be accessed from an object outside the class.

```java
class Robot {
    int id;
    Robot(int i) {
        id = i;
        Brain b = new Brain();
        b.think();
    }
    private class Brain {
        public void think() {
            System.out.println(id + " is thinking");
        }
    }
}
```

#### Sealed and Non-Sealed Classes

- **Sealed Classes**: Restrict which other classes can extend them.  
- **Non-Sealed Classes**: Allow unrestricted inheritance.

---

### Reflection Classes

Java's reflection API allows inspecting classes, methods, and fields at runtime.  

| Type          | Description                               | Example Usage                                         |
|---------------|-------------------------------------------|-------------------------------------------------------|
| `Class`       | Represents a class definition.            | `Class<?> clazz = String.class;`                      |
| `Method`      | Represents a method of a class.           | `Method method = String.class.getMethod("length");`   |
| `Field`       | Represents a class variable.              | `Field field = String.class.getField("CASE_INSENSITIVE");` |
| `Constructor` | Represents a constructor.                 | `Constructor<String> constructor = String.class.getConstructor();` |

---
