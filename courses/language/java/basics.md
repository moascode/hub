# Java Basics

This document serves as a reference for understanding the fundamentals of Java.

---

## Data Fundamentals

### Data Types

Java supports three categories of data types:

1. **Primitive Types**: Store simple values directly in memory.
2. **Wrapper Classes**: Provide object equivalents of primitives for use in collections, null handling, and utility methods.
3. **Other Special Types**: Classes like `String`, `Class`, `Method`, `Enum`, etc., offer advanced capabilities.

#### Primitive and Wrapper Classes
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

#### Notes
- **Wrapper Classes**: Useful in scenarios where primitives need to behave as objects, such as working with generics (`List<Integer>`) or allowing `null` values.
- **Range**: Defines the minimum and maximum values a primitive type can hold.
- **Boolean**: Has only two states: `true` and `false`.

---

### Data Operands

#### Variables
Variables act as containers for storing values during program execution. Their behavior and lifecycle are determined by their type and scope.

- **Local Variables**: Must be initialized explicitly. Declared inside methods or blocks and destroyed after block execution.
- **Instance Variables**: Exist as long as the object is alive.
- **Class Variables**: Declared with the `static` keyword and exist throughout the program lifecycle.
- **Final Variables**: Cannot reassign a reference, but the object contents can change.

---

## Data Operators

#### Operator Types
- **Unary**: Requires a single operand (e.g., `!`, `++`, `--`).
- **Binary**: Operates on two operands (e.g., `+`, `-`, `*`, `/`).
- **Ternary**: Simplifies conditional expressions (e.g., `x = (a > b) ? a : b;`).

#### Special Operators
- **`instanceof` operator**: Determines if an object is an instance of a class or subclass.
- **`==` operator**: Determines if values are equal in primitive and if references are equal in object.

---

### Type Casting

#### Numeric Promotion (Auto Casting)
Numeric promotion automatically converts smaller data types into larger ones during operations.

- If operands have different data types, Java promotes the smaller type to the larger type.
  - If one operand is an integer and the other is a decimal, the integer is promoted to a decimal.
- `byte`, `short`, and `char` are first promoted to `int` before any operation, and the result is `int`.

Example:
```java
int x = 5;
double y = 3.2;
double result = x + y; // x is promoted to double
```

#### Explicit Casting
Explicit casting is required when assigning a value of a larger data type to a smaller data type.

- Use explicit casting to avoid type mismatch errors.
- Possible loss of precision or overflow/underflow may occur.

Example:
```java
double largeNumber = 123.45;
int smallerNumber = (int) largeNumber; // Explicit cast
System.out.println(smallerNumber); // Output: 123 (truncated)
```

---

## Other Special Types

Here's the improved and expanded version of the **String** section based on your notes, with detailed explanations and comparisons.

---

### String

#### String Features

1. **Immutability**:
   - Strings in Java are immutable, meaning once created, their values cannot be changed.
   - Any modification (e.g., concatenation or replacement) creates a new `String` object.

2. **String Pool**:  
   - The **String Pool** is a special memory region in the heap where **string literals** are stored.
   - When a string literal is created (e.g., `String str = "Hello";`), Java checks the pool:
     - **If the string already exists in the pool**, its reference is reused.
     - **If not**, a new string is added to the pool.
   - Strings created with the `new` keyword are stored in the heap, not the pool. However, these can be added to the pool manually using the `intern()` method.
   - The pool is created at **runtime**, but its content is determined by **compile-time literals** and runtime additions via `intern()`.

   Example:  
   ```java
   String string1 = "hello";
   String string2 = "  hello  ".trim().intern();
   System.out.println(string1 == string2); // true
   ```

   - **`intern()` Method**:
     - Adds a string to the pool if it doesn't already exist and returns the reference from the pool.
     - This can help reduce memory usage by avoiding duplicate string objects in the heap.

---

#### Comparison: `String` vs. `StringBuilder` vs. `StringBuffer`

| Feature            | `String`                  | `StringBuilder`          | `StringBuffer`          |
|---------------------|---------------------------|---------------------------|--------------------------|
| **Mutability**      | Immutable                 | Mutable                   | Mutable                  |
| **Thread Safety**   | Thread-safe (immutability)| Not thread-safe           | Thread-safe              |
| **Performance**     | Slower (due to immutability)| Faster (no synchronization)| Slower (synchronization overhead) |
| **Use Case**        | Read-only strings or fewer modifications | Frequent string operations in a single thread | String operations in multi-threaded environments |
| **Memory Usage**    | Creates new objects for modifications | Modifies in place, reducing memory overhead | Modifies in place with synchronization |

---

### Common String Operations

1. **Method Chaining**:
   - Strings allow method chaining to combine multiple operations.  
     Example:
     ```java
     String name = "  John Wayne  ";
     name = name.trim().toUpperCase().replace('Y', 'R');
     System.out.println(name); // Outputs: JOHN WARNE
     ```

2. **Substring Operations**:
   - Use `substring(int beginIndex, int endIndex)` to extract parts of a string.  
     Example:
     ```java
     String str = "Hello, World!";
     String sub = str.substring(7, 12); // "World"
     ```

3. **Split and Join**:
   - Split strings into arrays using `split()`.
   - Join arrays or collections using `String.join()`.  
     Example:
     ```java
     String sentence = "Java is fun";
     String[] words = sentence.split(" "); // ["Java", "is", "fun"]
     String joined = String.join("-", words); // "Java-is-fun"
     ```

4. **Formatting Strings**
   - Use `String.format()` for constructing dynamic strings.  
     Example:
     ```java
     String name = "John";
     int age = 30;
     String formatted = String.format("%s is %d years old.", name, age);
     System.out.println(formatted); // "John is 30 years old."
     ```

---

### Reflection and Metadata

#### Reflection Classes
| Type            | Description                                | Example of Usage                                           |
|------------------|--------------------------------------------|------------------------------------------------------------|
| `Class`         | Represents a class definition in Java.     | `Class<?> clazz = String.class;`                           |
| `Method`        | Represents a method of a class.            | `Method method = String.class.getMethod("length");`        |
| `Field`         | Represents a field (variable) of a class.  | `Field field = String.class.getField("CASE_INSENSITIVE");` |
| `Constructor`   | Represents a class constructor.            | `Constructor<String> constructor = String.class.getConstructor();` |

---

## Date and Time (java.time)

### Key Classes
- **`LocalDate`**: Represents a date.
- **`LocalTime`**: Represents a time.
- **`LocalDateTime`**: Combines date and time.
- **`ZonedDateTime`**: Date and time with timezone information.

#### Common Methods
- **Current Date/Time**: `LocalDate.now()`, `LocalTime.now()`.
- **Custom Date/Time**: `LocalDateTime.of(2024, 12, 26, 14, 30)`.
- **Manipulation**:
  - Add/subtract: `plusDays()`, `minusWeeks()`.
  - Compare: `isBefore()`, `isAfter()`, `isEqual()`.

#### Period and Duration
- **Period**: Works with dates (e.g., `Period.between(startDate, endDate)`).
- **Duration**: Works with times (e.g., `Duration.between(startTime, endTime)`).

---

### Notes

- **`ChronoUnit`**: Use `ChronoUnit` from `java.time.temporal` to calculate time differences, e.g.,  
  `ChronoUnit.HOURS.between(time1, time2);`.

- **`Instant` for Timestamps**: `Instant` records timestamps, commonly for measuring process durations, e.g.,  
  ```java
  Instant before = Instant.now();
  Duration timeTaken = Duration.between(before, Instant.now());
  System.out.println(timeTaken.toMillis());
  ```

- **Convert to GMT**: Adjust offset time to convert to GMT, e.g.,  
  `2022-11-02T13:50+05:30` → GMT: `2022-11-02T07:20`.

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

---

## Interview notes

- **What is the problem with double precision in Java, and what are the alternatives to handle it efficiently in terms of memory and performance?**
  - `double` has precision limitations due to floating-point representation in binary. Not all decimal numbers can be exactly represented in binary, leading to rounding errors in calculations.
  - Alternative - BigDecimal: `BigDecimal` provides arbitrary precision but is slower and more memory-intensive than `double`.
  - Efficient Alternative - Fixed-Point Arithmetic: Fixed-point arithmetic scales decimals to integers (e.g., multiplying by 100) to avoid floating-point errors while maintaining performance and memory efficiency, similar to `double`.
