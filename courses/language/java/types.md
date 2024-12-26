# Java Primitives and Wrapper Classes

| Primitive Type | Wrapper Class     | Range                                   | Primitive Example         | Wrapper Example                                         |
|----------------|-------------------|-----------------------------------------|---------------------------|--------------------------------------------------------|
| `byte`         | `Byte`           | -128 to 127                             | `byte b = 100;`           | `Byte bObj = Byte.valueOf("100");`                    |
| `short`        | `Short`          | -32,768 to 32,767                       | `short s = 20000;`        | `Short sObj = Short.valueOf("20000");`                |
| `int`          | `Integer`        | -2^31 to 2^31-1                         | `int i = 12345;`          | `Integer iObj = Integer.valueOf("12345");`            |
| `long`         | `Long`           | -2^63 to 2^63-1                         | `long l = 123456789L;`    | `Long lObj = Long.valueOf("123456789");`              |
| `float`        | `Float`          | ±1.4E-45 to ±3.4E38                     | `float f = 3.14f;`        | `Float fObj = Float.valueOf("3.14");`                 |
| `double`       | `Double`         | ±4.9E-324 to ±1.7E308                   | `double d = 2.71828;`     | `Double dObj = Double.valueOf("2.71828");`            |
| `char`         | `Character`      | 0 to 65,535 (Unicode characters)        | `char c = 'A';`           | `Character cObj = Character.valueOf('A');`            |
| `boolean`      | `Boolean`        | `true` or `false`                       | `boolean b = true;`       | `Boolean bObj = Boolean.valueOf(true);`               |

## Notes
- **Wrapper classes** are used when primitives need to be treated as objects, e.g., in collections like `List<Integer>` or for null handling.
- **Ranges** for numeric types are inclusive and defined by the minimum and maximum values they can hold.
- **Character range** is based on Unicode, supporting a wide array of symbols and languages.
- **Boolean** has only two possible values: `true` and `false`.

# Other Types in Java

| Type            | Description                                | Example of Usage                                           |
|------------------|--------------------------------------------|------------------------------------------------------------|
| `Class`         | Represents a class definition in Java.     | `Class<?> clazz = String.class;`                           |
| `Method`        | Represents a method of a class.            | `Method method = String.class.getMethod("length");`        |
| `Field`         | Represents a field (variable) of a class.  | `Field field = String.class.getField("CASE_INSENSITIVE");` |
| `Constructor`   | Represents a class constructor.            | `Constructor<String> constructor = String.class.getConstructor();` |
| `Variable`      | A container for storing values.            | `int age = 25;`                                            |
| `String`        | Represents a sequence of characters.       | `String message = "Hello, World!";`                        |
| `Array`         | A collection of elements of the same type. | `int[] numbers = {1, 2, 3};`                               |
| `Enum`          | A special type for fixed sets of constants.| `enum Day { MONDAY, TUESDAY };`                            |
| `Interface`     | A contract for classes to implement.       | `interface Animal { void sound(); }`                       |
| `Annotation`    | Provides metadata about the code.          | `@Override public String toString() { return "Example"; }` |
| `Object`        | The root class of all classes in Java.     | `Object obj = new String("Hello");`                        |

## Notes
- **Reflection Classes** (`Class`, `Method`, `Field`, `Constructor`) are part of the `java.lang.reflect` package and are used for dynamic inspection and manipulation of classes.
- **String** is immutable and widely used for text manipulation.
- **Array** can hold multiple values of the same type but has a fixed size.
- **Enum** provides type safety and is useful for representing predefined constants.
- **Interface** and **Annotation** enhance code modularity and metadata handling.

