# Package

Packages are used to avoid name conflicts and control access to classes. To import classes from other packages, use the `import` keyword.  

```java
import samples.Vehicle;
```

## Java API

The Java API is a collection of classes and interfaces provided by Java for common programming tasks. You need to import the relevant package to use them.  

```java
import java.awt.*;  // The wildcard (*) imports all classes in the package
```

### Common Java API

#### 1. `java.lang`

- Automatically imported by default.  
- **`System.out.println()`**:  
  - `System`: A final class in the `java.lang` package.  
  - `out`: A static member of the `System` class, of type `PrintStream`.  
  - `println()`: A method of the `PrintStream` class used for output.

- **`Math` Class**:
  - `Math.abs(x)`: Absolute value.  
  - `Math.max(a, b)`: Maximum of two values.  
  - `Math.pow(a, b)`: `a` raised to the power `b`.  
  - `Math.sqrt(x)`: Square root.

---

#### 2. `java.util`

##### 2.1 **Scanner Class**

Used for reading user input.  

```java
import java.util.Scanner;  // From the utility package
```

##### 2.2 Collections  

The `java.util.Collections` class provides utility methods for working with collections. All methods are static, so you don’t need to create a `Collections` object to use them.

- **Common Methods**:
  - `max(Collection c)`: Returns the maximum element based on natural ordering.
  - `min(Collection c)`: Returns the minimum element.
  - `reverse(List list)`: Reverses the elements in the list.
  - `shuffle(List list)`: Randomizes the order of elements.
  - `sort(List list)`: Sorts elements in natural order.

  ```java
  import java.util.Collections;
  import java.util.ArrayList;

  ArrayList<String> animals = new ArrayList<>();
  animals.add("tiger");
  // Sort in ascending order
  Collections.sort(animals);
  // Sort in descending order
  Collections.sort(animals, Collections.reverseOrder());
  ```

##### 2.3 Iterators  

The `Iterator` interface provides methods to traverse collections.  

- `hasNext()`: Returns `true` if there are more elements.
- `next()`: Returns the next element.  
- `remove()`: Removes the last returned element.


```java
import java.util.Iterator;
import java.util.LinkedList;

LinkedList<String> animals = new LinkedList<>();
animals.add("fox");

Iterator<String> it = animals.iterator();    
while (it.hasNext()) {      
    String value = it.next();     
    System.out.println(value);       
}
```

---

#### 3. `java.time`

The `java.time` package provides classes for date and time manipulation.

- `LocalDate`: Represents a date.
- `LocalTime`: Represents a time.
- `LocalDateTime`: Combines date and time.
- `ZonedDateTime`: Date and time with timezone information.

Common Methods

- **Current Date/Time**:  

  ```java
  LocalDate.now();
  LocalTime.now();
  ```

- **Custom Date/Time**:  

  ```java
  LocalDateTime.of(2024, 12, 26, 14, 30);
  ```

- **Date/Time Manipulation**:  
  - `plusDays()`, `minusWeeks()`.  
  - Compare with `isBefore()`, `isAfter()`, `isEqual()`.

- **Periods**:  

  ```java
  Period.between(startDate, endDate);
  ```

- **Durations**:  

  ```java
  Duration.between(startTime, endTime);
  ```

- **`ChronoUnit`**:  

  ```java
  ChronoUnit.HOURS.between(time1, time2);
  ```

- **Timestamps with `Instant`**:  

  ```java
  Instant before = Instant.now();
  Duration timeTaken = Duration.between(before, Instant.now());
  System.out.println(timeTaken.toMillis());
  ```

- **Converting to GMT** (example conversion):  
  `2022-11-02T13:50+05:30` → GMT: `2022-11-02T07:20`.  

---

#### 3. `java.io`

Files: The java.io package includes a File class that allows you to work with files. exists() method determines whether a file exists. getName() method returns the name of the file. double backslashes is used in the path

```java
import java.io.File;
//...
 File x = new File("C:\\sololearn\\test.txt");    
if(x.exists()) {     
System.out.println(x.getName() +  "exists!");    
}    else {     
 System.out.println("The file does not exist");   
}
```

Reading a file: Scanner class from the java.util.Scanner package is used to read the files. We can use the Scanner object's next() method to read the file's contents.

```java
import java.util.Scanner;
//..
try {  
  File x = new File("C:\\sololearn\\test.txt");  
  Scanner sc = new Scanner(x);  
  while(sc.hasNext()) {    
    System.out.println(sc.next());  
  }  
  sc.close();
} 
catch (FileNotFoundException e) {  
  System.out.println("Error");
}
```

Creating a file: Formatter, another useful class in the java.util.Formatter package, is used to create content and write it to files. If the file already exists, this will overwrite it.

```java
import java.util.Formatter;

public class MyClass {
   public static void main(String[ ] args) {
  try {
    Formatter f = new Formatter("C:\\sololearn\\test.txt");
  } catch (Exception e) {
      System.out.println("Error");
  }
  }
}
```

Writing to a file: format() method of Formatter class is used to write content to files. \r\n is the newline symbol in Windows. \r = return, moves all the way to the left, but doesn't move down, \n = newline, moves down but not horizontally. %s mean a string and get's replaced by the first parameter

```java
import java.util.Formatter;
//... 
try {
    Formatter f = new Formatter("C:\\sololearn\\test.txt");
    f.format("%s %s %s", "1","John", "Smith \r\n");
    f.format("%s %s %s", "2","Amy", "Brown");
    f.close();    
  } catch (Exception e) {
    System.out.println("Error");
  }
  ```

---

#### 3. `java.Math`

```java
int a = Math.max(3, 11); //11
in b = Math.min(-2, 0); //-2

//aware of autocasting
int x = 5; long y = 3;
long z = Math.max(x, y); //5; x will be autocasted to long and the result will be long

double d = 2.56;
Math.round(d) // 3; decimal to integral; param float - return int, param double - return long

//always return double
Math.ceil(2.45) //3.0
Math.floor(2.45); //2.0
Math.pow(2, 5); //32.0
math.random(); //random number between 0 and 1.0 (not included)
```

---
