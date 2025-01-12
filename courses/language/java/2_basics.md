# Basics

## Data Types

Java supports two categories of data types:

### Primitive Types

Store simple values directly in memory. Primitive types are faster and memory efficient. (Ex: int, long, float, double, char, boolean..)

### Non-Primitive/ Reference Types

Objects contains addresses of locations in memory (Arrays, Strings, Object). It is useful for generics or allowing null values.

- **Wrapper Classes**: Provide object equivalents of primitives. (Ex: Byte, Short, Integer..)

Primitive and Wrapper Classes summary

| Primitive Type | Wrapper Class | Range                                   | Primitive Example         | Wrapper Example                  |
|----------------|---------------|-----------------------------------------|---------------------------|-----------------------------------|
| `byte`         | `Byte`        | -128 to 127                             | `byte b = 100;`           | `Byte bObj = Byte.valueOf("100");` |
| `short`        | `Short`       | -32,768 to 32,767                       | `short s = 20000;`        | `Short sObj = Short.valueOf("20000");` |
| `int`          | `Integer`     | -2^31 to 2^31-1                         | `int i = 12345;`          | `Integer iObj = Integer.valueOf("12345");` |
| `long`         | `Long`        | -2^63 to 2^63-1                         | `long l = 123456789L;`    | `Long lObj = Long.valueOf("123456789");` |
| `float`        | `Float`       | ±1.4E-45 to ±3.4E38                     | `float f = 3.14f;`        | `Float fObj = Float.valueOf("3.14");` |
| `double`       | `Double`      | ±4.9E-324 to ±1.7E308                   | `double d = 2.71828;`     | `Double dObj = Double.valueOf("2.71828");` |
| `char`         | `Character`   | 0 to 65,535 (Unicode characters)        | `char c = 'A';`           | `Character cObj = Character.valueOf('A');` |
| `boolean`      | `Boolean`     | `true` or `false`                       | `boolean b = true;`       | `Boolean bObj = Boolean.valueOf(true);` |

#### String

- Strings in Java are immutable, meaning once created, their values cannot be changed. Any modification (e.g., concatenation or replacement) creates a new `String` object.
- The **String Pool** is a special memory region in the heap where **string literals** are stored. The pool is created at **runtime**, but its content is determined by **compile-time literals** and runtime additions via `intern()`. When a string literal is created (e.g., `String str = "Hello";`), Java checks the pool:
  - **If the string already exists in the pool**, its reference is reused.
  - **If not**, a new string is added to the pool.
- Strings created with the `new` keyword are stored in the heap, not the pool. However, these can be added to the pool manually using the `intern()` method.

```java
String str = "first" //create string "first" and point str to it
str.concat(" second")//create string "first second " and nothing points at it, so no change to str!!
str = str.concat(" second") //create string "first second" and point str to it
String str2 = "  first  ".trim().intern(); //points to "first" from string pool which was created with "str" 
```

#### Comparison: `String` vs. `StringBuilder` vs. `StringBuffer`

| Feature            | `String`                  | `StringBuilder`          | `StringBuffer`          |
|---------------------|---------------------------|---------------------------|--------------------------|
| **Mutability**      | Immutable                 | Mutable                   | Mutable                  |
| **Thread Safety**   | Thread-safe (immutability)| Not thread-safe           | Thread-safe              |
| **Performance**     | Slower (due to immutability)| Faster (no synchronization)| Slower (synchronization overhead) |
| **Use Case**        | Read-only strings or fewer modifications | Frequent string operations in a single thread | String operations in multi-threaded environments |
| **Memory Usage**    | Creates new objects for modifications | Modifies in place, reducing memory overhead | Modifies in place with synchronization |

### Type Casting

- **Auto Casting/ Upcasting (Numeric Promotion):** Numeric promotion automatically converts smaller data types into larger ones during operations. `byte`, `short`, and `char` are first promoted to `int` before any operation, and the result is `int`.
- **Explicit Casting/ Downcasting:** Explicit casting is required when assigning a value of a larger data type to a smaller data type. Use explicit casting to avoid type mismatch errors. Possible loss of precision or overflow/underflow may occur.

```java
int x = 5;
double y = 3.2;
double result = x + y; // x is promoted to double

double largeNumber = 123.45;
int smallerNumber = (int) largeNumber; // Explicit cast
System.out.println(smallerNumber); // Output: 123 (truncated)
```

### Boxing and Unboxing

- **Boxing** is converting primitive into wrapper class
- **Unboxing** is converting wrapper class into primitive
- **Autoboxing** is when boxing is done autometically
- **Java can not do autocast and autobox at the same time**

```java
int a = 5;
Integer b = Interger.valueOf(a) //boxing
int c = b.intValue() //unboxing
Integer d = c //autoboxing

int x = 7;
long y = x //autocasting - ok
Long z = x //autocasting and autoboxing can not be done together - nok
Long z = Long.valueOf(x) // explicit boxing - ok
Long z = (long) x //explicit casting - ok
```

### Notes

- **What is the problem with double precision in Java, and what are the alternatives to handle it efficiently in terms of memory and performance?**

  - **Problem:** `double` has precision limitations due to floating-point representation in binary. Not all decimal numbers can be exactly represented in binary, leading to rounding errors in calculations.
  
  - **Solution:**
  
    - Alternative - BigDecimal: `BigDecimal` provides arbitrary precision but is slower and more memory-intensive than `double`.
    - Efficient Alternative - Fixed-Point Arithmetic: Fixed-point arithmetic scales decimals to integers (e.g., multiplying by 100) to avoid floating-point errors while maintaining performance and memory efficiency, similar to `double`.

---

## Variables

Variables are containers for storing values during program execution. Their behavior and lifecycle are determined by their type and scope.

- **Local Variables**: Must be initialized explicitly. Declared inside methods or blocks and destroyed after block execution.
- **Instance Variables**: Exist as long as the object is alive.
- **Class Variables**: Declared with the `static` keyword and exist throughout the program lifecycle.
- **Final Variables**: Cannot reassign a reference, but the object contents can change.

---

## Operators

- Operator Types
  
  - **Unary**: Requires a single operand (e.g., `!`, `++`, `--`).
  - **Binary**: Operates on two operands (e.g., `+`, `-`, `*`, `/`).
  - **Ternary**: Simplifies conditional expressions (e.g., `x = (a > b) ? a : b;`).
  
- Special Operators
  
  - **`instanceof` operator**: Determines if an object is an instance of a class or subclass.
  - **`==` operator**: Determines if values are equal in primitive and if references are equal in object.

---

## Flow Control

### Conditional Constructs

- **`if-else`**: Basic decision-making structure.
- **`switch`**:
  
  - Supports `byte`, `short`, `char`, `int`, `String`, and enums.
  - Uses `yield` for returning values from a switch block.
  - Example:

    ```java
    String dayType = switch(day) {
        case MONDAY, TUESDAY, WEDNESDAY -> "Weekday";
        case SATURDAY, SUNDAY -> "Weekend";
        default -> "Unknown";
    };
    ```

### Loops

- **For Loops**:

  - Infinite loop: `for(;;)`
  - Multiple indices: `for (int i = 0, j = 5; i < j; i++, j--)`
  
- **While Loop**: Repeats as long as the condition is `true`.
- **Break and Continue**:

  - Labeled breaks to exit nested loops.

## Special Keywords

### Optional specifier

| **Keyword** | **Field** | **Method** | **Class** |
|--------------|-----------|------------|-----------|
| `volatile` | Used to indicate that a variable's value may be changed by multiple threads. Guarantees visibility of changes to variables across threads. | N/A | N/A |
| `transient` | Fields marked as `transient` are not serialized when an object is converted to a byte stream. | N/A | N/A |
| `static` | A static field belongs to the class, not instances. Changing its value affects all instances of the class. | A static method belongs to the class and can be called without creating an instance. It can only access static fields or methods. The main method must always be static. | A static class can only be a nested class (non-top-level), allowing organization of code. |
| `final` | A final field can only be assigned once. For reference types, the reference is constant, but the content can be modified.  | A final method cannot be overridden by subclasses. | A final class cannot be subclassed (inherited from). |

- `static final field` must be initialized before use.
- `static block` is used to initialize static variables. It runs once when the class is loaded.
- `static method` can only call static field/method
  
  - fix1: make all field and method static
  - fix2: create instance every time to access non-statis field and method
  - fix3: create a static instance and use it everywhere
- `static import` is used to import static members of another class, enabling direct access without class reference (e.g., `import static java.lang.Math.pow`).
- `void` indicates that a method does not need to return any value

### Access Modifier

| **Access Modifier** | **Field** | **Method** | **Class** |
|---------------------|-----------|------------|-----------|
| `private` | Field can only be accessed within the same class. | Method can only be accessed within the same class. | Only inner/nested class can be declared `private` and it can only be accessed within the outer class |
| `default` (no modifier) | Field can be accessed within the same package. | Method can be accessed within the same package. | Class can be accessed within the same package. |
| `protected` | Field can be accessed within the same package and by subclasses outside the package. | Method can be accessed within the same package and by subclasses outside the package. | N/A |
| `public` | Field can be accessed from anywhere in the program. | Method can be accessed from anywhere in the program. | Class can be accessed from anywhere in the program. |
