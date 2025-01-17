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

## Hashmap

HashMap is used for storing data collections as key and value pairs. The put, remove, and get methods are used to add, delete, and access values in the HashMap. Use  size() method to get the number of elements.

```java
import java.util.HashMap;
//...
 HashMap<String, Integer> points = new HashMap<String, Integer>();   
points.put("Amy", 154);
```

## Sets

A Set is a collection that cannot contain duplicate elements. One of the implementations of the Set is the HashSet class.

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

## Enum

An Enum is a special type used to define collections of constants. values are comma-separated. Enums define variables that represent members of a fixed set. Enum values can be used for switch statement. an enum is a type of class that mainly contains static members. You should always use Enums when a variable (especially a method parameter) can only take one out of a small set of possible values.

```java
enum Rank {  SOLDIER,  SERGEANT,  CAPTAIN}
Rank a = Rank.SOLDIER;
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
