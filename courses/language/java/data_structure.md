# Data Structure

## Collection

A set of interfaces commonly referred as Collection.

List, Set, Queue implement Collection
ArrayList implment List
HashSet and TreeSet implement Set
interface Deque implements Queue
LinkedList implements Queue and List
interface Map does not implement collection
HashMap and TreeMap implement Map

Methods in collection
Collection.equals() - compares the type and contents of collection, implementations vary
ArrayList checks order, Hashmap checks if contains same elements

All collection interfaces are generic, therefore support all object types

## ArrayList

List is an ordered collection that can have duplicates. There are two implementation of the List interface - ArrayList and LinkedList.
ArrayList is better for accessing data while LinkedList for inserting data.

a resizable array. ArrayList class is in the java.util.ArrayList package. ArrayLists store objects. Thus, the type specified must be a class type. You cannot pass, for example, int as the objects' type. Instead, use the special class types that correspond to the desired value type, such as Integer for int, Double for double, and so on. The add() method adds new objects to the ArrayList. Conversely, the remove() methods remove objects from the ArrayList. Useful methods: get(int index), size(), clear(), contains().

```java
import java.util.ArrayList;

String[] names = new String[]{"John", "George", "Luke"};
//Factory methods for creating List, size is fixed so you can not add/remove elements
List<String> namesList = Arrays.asList(names) // elements can be modified
List<String> namesOf = List.of(varargs) //immutable list
List<String> namesCopyOf = List.copyOf(namesList) //immutable list with copy of original values


ArrayList<String> colors = new ArrayList<String>(10); //initial size
List<String> colors2 = new ArrayList<>();//can specify the interface List on the left, can ommit the type on the right side
List<String> colors3 = new ArrayList<>(colors2) //creates copy of colors2
var names = new ArrayList<String>(); //must specify the type on the right side for using var
names.add("Spartan") //return true
names.remove("Spartan") // return true, return false if not exist
names.isEmpty() //returns true
names.size() // returns size 0
names.clear() // clear collection
names.add("Spartan2")
names.add("Spartan3")
names.add("Spartan4")
names.contains("Spartan2") //returns true
names.removeIf(s -> s.length() > 4) //remove element Spartan2 since it's length is 8 : takes predicate as argument
names.foreach(name -> System.out.print(name + ", ")) //prints Spartan3, Spartan4 : takes consumer as argumenr
names.equals() //comparing the type and contents of collection
```

## Linkedlist

Linkedlist stores data and address of the next node which link each node with another. You cannot specify an initial capacity for the LinkedList.

```java
import java.util.LinkedList;
//....
LinkedList<String> c = new LinkedList<String>();
```

## Queue

Queue interface is implemnted by LinkedList class. It adds element at the back and reads from the front. The Queue interface has it's own method. The difference between the proper method and collection methods is that collection will throw exception while proper method will return false for unsuccessfull operation.

```java
Queue<string> colors = new LinkedList<>();
colors.offer("blue"); //add element to the queue
colors.offer("red");
String first = colors.peek() //returns the first element in the queue
colors.poll() //remove the first element in the queue
```

### Deque

Deque interface is used to access element from both side of the queue, also called double ended queue. It can be also used as stack. It is implemnted by LinkedList and ArrayQueue.

Stack: adds element from the back and reads from the back. Mthods - peek(), push(E e), pop()
Double ended queue: methods - peekFirst(), pollFirst(), offerFirst(E e), peekLast(), pollLast(), offerLast(E e)

```java
Deque<String> colors = new ArrayQueue<>(); //used as stack
Deque<Integer> nums = new LinkedList<>(); //used as double ended queue
```

## Map

Map is used for storing data collections as key and value pairs. The put, remove, and get methods are used to add, delete, and access values in the HashMap. Use size() method to get the number of elements. There are two implementations of the map interface - HashMap and TreeMap. Hashmap does not maintain order while TreeMap maintains order but takes more time to add element.

```java
import java.util.HashMap;

Map<Integer, String> names = Map.of(1, "John", 2, "George");
HashMap<Integer, String> names = new HashMap<>();   
names.put(1, "Amy");
names.put(5, "John");
names.putIfAbsent(7, "Hero"); //put only if the key is absent

String myName = names.get(1);
String myName2 = names.getOrDefault(2, "NA");
String myName3 = names.replace(5, "Gorge")//repalces with new value but returns old value "John"

//merge() -- insert only if the name is longer than original name or key is absent
BinFunction<string, String, String> longerName = (name1, name2) -> name1.length() > name2.length() ? name1 : name2;
names.merge(7, "Heroine", longerName);
names.merge(8, "Steve", longerName);



//loop over all keys
for(Integer key: names.keySet()){
    System.out.println("Key: " + key + " Value: " + names.get(key))
}
//foreach
names.forEach((k,v) -> System.out.println("Key: " + k + " Value: " + v));
//entryset
names.entrySet().forEach(e -> System.out.println("Key: " + e.getKey() + " Value: " + e.getValue()))
```

## Sets

A Set is a collection that cannot contain duplicate elements. There are two implementation of the Set interface.

- HashSet: stores hashcode as key and object as value. can not contain duplicate and does not maintain order
- TreeSet: stores element in sorted order, default order is insertion order. insertion time is more than HashSet

```java
import java.util.HashSet;
//...
HashSet<String> set = new HashSet<String>();   
set.add("A"); //return true, return false if it's duplicate 
```

### LinkedHashSet

LinkedHashSet maintains a linked list of the set's elements in the order in which they were inserted. A hash table stores information through a mechanism called hashing, in which a key's informational content is used to determine a unique value called a hash code. So, basically, each element in the HashSet is associated with its unique hash code to directly access the memory address.

```java
import java.util.LinkedHashSet;
//....
LinkedHashSet<String> set = new LinkedHashSet<String>();
set.add("A");
```

## Sorting data in Collection

Data is sorted using sort() method. 

- For primitive, elements are sorted by natural order.
- For String, numbers > uppercase lesster > lowercase letter
- For Object, define criterie for sorting

There are two ways to define sorting criteria for object
    - use a class which implemetns Comparable<T> interface. It has one abstract method - int comapreTo(T o). It retuens an int based on following rules.
      - if both objects are same, return 0
      - if current object is smaller, return negative number
      - if current object is larger, return positive number
    - pass the implementation of Comparator<T> interface in sort() method. It has one mthod - compare(T o1, T o2). This is mainly used when ther are multiple sorting criteria

```java
public class Person implements Comparable<Person> {
    private String name;
    private String age;
    public Person(String name, String age) {
        this.name = name;
        this.age = age;
    }
    public String getName(){return name;}
    public String getAge(){return age;}
    @Override
    public int comapreTo(Person other) {
        return this.age - other.age; //same? return 0; larger? return positive; smaller? return negative
    }
}
//main method - using Comparator<T> interface
List<Person> personList = Arrays.asList(new Person("John", 25), new Person("Amy", 20));
Collections.sort(personList, (p1, p2) -> p1.getAge() - p2.getAge()); // sort by age
Collections.sort(personList, (p1, p2) -> p1.getName().compareTo(p2.getName())) //sort by name
//Comparator is in java.util package
Collections.sort(personList, Comparator.comparing(Person::getName)); //sort using method reference
Collections.sort(personList, Comparator.comparing(Person::getName).reversed()); //reverse sorting
Collections.sort(personList, Comparator.comparing(Person::getName).thenComparingInt(Person::getAge)); //multiple comparison
```

## Summary

Array size can be changed in Arraylist during runtime and each element is stored in sequence memory location. Search (get method) operations are fast in Arraylist

Linked list is a data structure where size cannot be initialized and each node is linked to other node. Node consists of data and address of next node. These are stored at random memory locations.  Insert and remove operations give good performance (O(1)) in LinkedList

The ArrayList is better for storing and accessing data, as it is very similar to a normal array.The LinkedList is better for manipulating data, such as making numerous inserts and deletes.

Arrays and Lists store elements as ordered collections

A HashMap cannot contain duplicate keys. Adding a new item with a key that already exists overwrites the old element. The HashMap class provides containsKey and containsValue methods that determine the presence of a specified key or value.

HashSet class cannot have duplicate elements but does not automatically retain the order.

LinkedHashSet maintains a linked list of the set's elements in the order in which they were inserted.

HASHMAP, HASHTABLE, HASHCODE, VECTOR, STRINGBUILDER, STRINGBUFFER
