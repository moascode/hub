# Class

A **class** is a blueprint for creating objects. It defines behavior (methods) and attributes (fields or variables).  

## Class Members

### Fields (Variables)

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

### Methods

A method performs actions defined by its body. **Method Signature** includes the method's name, the number and types of parameters, and the return type.  

#### Mehtod Overriding

Subclass can override method from super class. The overridden method needs to be at least as acceesible as the original method. The return type can be subtype for overriden method. 
The exception thrown can also be subtype of the original exception.
Private and static method can not be overrriden but can be hidden. That means you can have the same mthod name in the subclass which will belong to the class.
Final method can not be overriden.

---

## Constructor

A **constructor** is a special method used to initialize an object when it is created. It has the same name as the class and no return type.  

- A class can have multiple constructors (overloading).  
- If no constructor is defined, a **default constructor** is automatically provided.  
- Constructors are not inherited.  
- Access modifiers (`private`, `protected`, `public`) can be used.
  - **Private constructors** prevent direct object creation and are often used with static factory methods.  
- **`this`**: Refers to the current object. It is used to access instance variable.
  - `this()` calls another constructor in the same class and must be the first statement.  
- **`super`**: Refers to the superclass. It is used to access super class variable.
  - `super()` calls the superclass constructor.  
  - If not explicitly used, a no-arg `super()` is added automatically. Compilation fails if no matching constructor exists.  

### Initialization Order

1. Superclass constructor.  
2. Static variables and initializers.  
3. Instance variables and initializers.  
4. Constructor body.  

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

### Anonymous Classes

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

### Inner Classes

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

### Sealed and Non-Sealed Classes

- **Sealed Classes**: Restrict which other classes can extend them. It must be declared in the same package as it's subclasses.  
- **Non-Sealed Classes**: Allow unrestricted inheritance.

```java
public sealed class Car permits Ford, Renault, Fiat {}
//each of the permitted class must extend Car
//subclasses have to be either final, sealed or non-sealed

public final class Ford extends Car {}
//can not be further extended

public non-sealed class Renault extends Car {}
//can be extended by any other class

public sealed class Fiat permits Uno, Punto {}
//cn only be extended by Uno and Punto
```

### Reflection Classes

Java's reflection API allows inspecting classes, methods, and fields at runtime.  

| Type          | Description                               | Example Usage                                         |
|---------------|-------------------------------------------|-------------------------------------------------------|
| `Class`       | Represents a class definition.            | `Class<?> clazz = String.class;`                      |
| `Method`      | Represents a method of a class.           | `Method method = String.class.getMethod("length");`   |
| `Field`       | Represents a class variable.              | `Field field = String.class.getField("CASE_INSENSITIVE");` |
| `Constructor` | Represents a constructor.                 | `Constructor<String> constructor = String.class.getConstructor();` |

---

## Special "Class"

### Enum

An Enum is a special type used to define collections of constants. values are comma-separated. Enums define variables that represent members of a fixed set. Enum values can be used for switch statement. an enum is a type of class that mainly contains static members. You should always use Enums when a variable (especially a method parameter) can only take one out of a small set of possible values.

```java
enum Rank {  SOLDIER,  SERGEANT,  CAPTAIN}
Rank a = Rank.SOLDIER;
for(var rank : Rank.values()) {
  System.out.println(rank.ordinal() + ":" + rank.name()) //1 : SOLDIER
}
```

Enum can have contructor and instance methods.
Enums can implement anstract methods inside enum.

```java
enum Compass {
  NORTH("america"), SOUTH("africa"), WEST("europe"), EAST("asia");
  private final String continent;
  private Compass(String continent) { //always private
    this.continent = coontinent;
  }
  public getContinent() {
    return this.continent;
  }
}
//main method
Compass.NORTH.getContinent(); //constrcutor is called for each enum once
```

Enums can implement interface.

```java
public interface Planet{
  String getPlanetName();
}
enum Compass implements Planet {
  //implement for specific enum
  NORTH {
    public String getPlanetName(){return "Earth in the North";}
  },
  SOUTH {
    public String getPlanetName(){return "Earth in the South";}
  }
  //or can also implement as a generic one
  public String getPlanetName(){return "Earth";}
}
//main method
Compass.SOUTH.getPlanetName();
```

### Records

Encapsulated classes but without boilerplate code. Encapsulation is secured. Constructor, getters, toStirng(), equals(), hashCode() are auto generated. Records can not have fields other than in constrcutor. Record can have static fields and methods.

```java
```
