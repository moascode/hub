# Java Threads

Java is a multi-threaded programming language. There are two ways to create a thread. 

- One is to Extend the Thread class. Every Java thread is prioritized to help the operating system determine the order in which to schedule threads. The priorities range from 1 to 10, with each thread defaulting to priority 5. You can set the thread priority with the setPriority() method.

```java
class Loader extends Thread {  
    public void run() {    
        System.out.println("Hello");  
    }
}
    
class MyClass {  
    public static void main(String[ ] args) {    
        Loader obj = new Loader();    
        obj.start();  
    }
}
```

- Other way is to  implementing the Runnable interface. The Thread.sleep() method pauses a Thread for a specified period of time. For example, calling Thread.sleep(1000); Thread.sleep() throws an InterruptedException, so be sure to surround it with a try/catch block. implementing the Runnable interface is the preferred way to start a Thread, because it enables you to extend from another class, as well.
  
```java
class Loader implements Runnable {  
    public void run() {    
        System.out.println("Hello");  
}   }

class MyClass {  
    public static void main(String[ ] args) {    
        Thread t = new Thread(new Loader());    
        t.start();  
}   }
```
