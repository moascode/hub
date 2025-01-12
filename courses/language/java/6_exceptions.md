# Java Exceptions

Exceptions are caused by user error, programmer error, or physical resource issues. A try/catch block is placed around the code that might generate an exception.  The Exception type can be used to catch all possible exceptions. If an exception is created using thorws, this exception must be managed in the caller program using try/catch block. A single try block can contain multiple catch blocks that handle different exceptions separately. 'finally' is added after 'try' and 'catch' to execute some code whether the exception happened or not.

```java
public class MyClass {
    public static void main(String[ ] args) {
        try {
            int a[ ] = new int[2];
            System.out.println(a[5]);
        } catch (Exception e) {
            System.out.println("An error occurred");
        }
        finally {
            System.out.println ("I can run no matter what");
        }
    }
}
```
