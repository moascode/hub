# Java Package

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
