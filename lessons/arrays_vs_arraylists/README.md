- title: Arrays vs ArrayLists
- tags: android, arrays, arraylists, big O

# Objectives
- Recognize the difference between arrays and arraylists
- Introduction to Big O notation

# Resources
- [Introduction to Data Structures - mycodeschool via Youtube](https://www.youtube.com/watch?v=92S4zgXN17o&list=PL2_aWCzGMAwI3W_JlcBbtYTwiQSsOTa6P)
- [Data Structures: List as Abstract Data Type - mycodeschool via Youtube](https://www.youtube.com/watch?v=HdFG8L1sajw&list=PL2_aWCzGMAwI3W_JlcBbtYTwiQSsOTa6P&index=2)
- [Data Structures: Arrays v. Linked Lists - mycodeschool via Youtube](https://www.youtube.com/watch?v=lC-yYCOnN8Q&list=PL2_aWCzGMAwI3W_JlcBbtYTwiQSsOTa6P&index=4)

# Arrays

## Properties

An **array** is a special kind of collection in Java. An array has the following properties:

- **ordered**: The items in an array have a definite order, as with a `List`.

- **one-dimensional**: The items are arranged in a one-dimensional sequence.

- **indexed**: The items in an array are indexed from 0 through one less than the length, and each can be accessed by index.

- **fixed length**: The length of an array must be specified when the array is created, and cannot be changed afterward.

- **mutable**: The items in an array (but not the length of the array) may individually be changed at any time.

- **homogeneous**: The type of an array must be specified when the array is created. All items in in the array must be of this type. The type may be a primitive type, a class, or even an array type.  (But see below regarding subclasses and class arrays.)

> :star: **Note:** The length of an array is represented by a `int` (which may not be negative), as are indexes.  This means the size of a Java array is limited to (1 << 31) - 1, about 2.1 billion.

## Types

An array _type_ is written by the base type followed by square brackets.  For example, an array of `boolean` is written `boolean[]`, and an array of `String` is written `String[]`.

## Creating

An array variable is a reference variable, like a class variable.  As with a class variable, an array variable may have the value `null`, indicating that it does not refer to an array at all.

```java
int[] arr;          // Initialized to null.
int[] arr = null;
int arr[];          // Alternate syntax.
```

Arrays themselves are allocated on the Java heap, like objects, using the `new` keyword, and specifying the array length in the square brackets.

```java
int[] arr = new int[4];
```

Like static variables, the items of an array are initially set to safe default values: 0 for numeric types, false for booleans, `null` for object types. You can also initialize the array to given values, using either equivalent syntax:

```java
int[] arr = new int[4] { 4, 8, 0, 10 };
int[] arr = { 4, 8, 0, 10 };
```

Like objects, arrays are cleaned up by the garbage collector once they are no longer referenced.

## Accessing

Square brackets are used to access an element in an array, given its index.  The index value must be at least zero, and must be less than the array length; this is checked at run time.

```java
arr[0]  // First element; evaluates to 4.
arr[2]  // Third element; evaluates to 0.

arr[4]  // Raises ArrayIndexOutOfBoundsException
```

On the left side of an assignment (`=`), this sets the item rather than getting it.

```java
arr[3] = 42;
```

An array variable may be assigned (unless it is `final`) a different array by assigning it without square brackets.

> :star: **Note:** If you assign an array variable without specifying an index in square brackets, you are changing the array variable to point to a different array.  This does not change the values in either the old or the new array!
>
> ```java
int[] arr0 = { 1, 3, 5, 7 };
int[] arr1 = { 2, 4, 6, 8 };
> ```
>
> Initially, `arr0` and `arr1` refer to different arrays.  This line
> changes one element in the array `arr0` refers to.
>
> ```java
arr0[1] = 100;
> ```
>
> `arr0` now contains { 1, 100, 5, 7 }.
>
> This assignment now changes the array _variable_ `arr0` to refer to the _same array_ as `arr1`.
>
> ```java
arr0 = arr1;
> ```
>
> The array that `arr0` previously referred to is now a candidate for garbage collection.  Since `arr0` and `arr1` both refer to the same array, changes to one will be visible through the other.
>
> ```java
System.out.println(arr0[1]);
arr1[1] = 200;
System.out.println(arr0[1]);
> ```
> This prints out "4" followed by "200".

An array also has a `length` field, which contains its length.

To iterate over the contents of an array, you may either iterate over indexes explicitly,

```java
for (int i = 0; i < arr.length; ++i)
    System.out.println(arr[i]);
```

or using an iterator 'for' loop.

```java
for (int item : arr)
    System.out.println(item);
```

Remember, an array may not be resized; its length is set by `new`.  It may be reassigned to a different array object, though; it's up to you to make sure the new array has the same contents.

## Copying

`System.arraycopy()` copies a range of elements of an array either to another location in the same array or to another array.  It even handles correctly a copy from one range to another overlapping range in the same array.

Its arguments are,

1. The source array.
2. The start index in the source array.
3. The target array (which may be the same as the source array).
4. The start index in the target array.
5. The number of items to copy.

For example, `System.arraycopy(arr0, 2, arr1, 0, 3)` will copy 3 items starting from the third position (index 2) of `arr0`, to the beginning (index 0) of `arr1`.

> :star: **Hint:**  Using `arraycopy()`, we can write a simple method that "expands" an array by creating a larger array and copying elements from the old array into it.
>
> ```
static int[] expandArray(int[] array, int newSize) {
    int[] newArray = new int[newSize];
    System.arraycopy(array, 0, newArray, 0, array.length);
    return newArray;
}
```

## Other operations

The [`java.util.Arrays`](http://docs.oracle.com/javase/7/docs/api/java/util/Arrays.html) class contains a numer of static methods that operate on arrays.  Since Java generics cannot be used with primitive types, this class provides overloads for each primitive array type for most of its methods.

## Arrays and inheritance

> :star: **Note:** This is an advanced topic!

Java allows you to cast a class array to an array of the class's base. For example, with this class hierarchy,

```java
public class C {}
public class D extends C {}
```

Java allows you to cast a `D[]` array to `C[]`.  This leads to a dangerous situation: Java allows you to insert a `C` instance into a `C[]` array, but also promises you that you receive a `D` instance when you index a `D[]` array.  If both types can refer to the same array, there's a contradiction.  Can you see it?

Consider this code:

```java
D[] dArr = new D[4];   // Create a D array.
dArr[0] = new D();     // Add a D instance to it.
C[] cArr = dArr;       // Cast the array to the base class array.
cArr[1] = new C();     // Add a C instance to the same array.
D d = dArr[1];         // Extract the C instance as a D.  Yikes!
```

To avoid this situation, a Java array carries with it the type of objects it can hold, which is specified when the array is created with `new`.  Any insertion of an item to the array is checked against this (dynamic) type, even if the insertion is via an array variable with a base class array type. So, in the code above, the fourth line will raise an `ArrayStoreException`.

# Performance

An array is stored as a contiguous block of memory, which determines its performance for specific actions:

1. Accessing an Element: O(1)
  - Since we know know where the block of memory is and the size of the array is fixed, getting the element at an index is a matter of multiplying the size of the type of the element by the index, and adding that to the memory address of the array (as demonstrated with our hex math above). Computers can do this kind of look up very quickly as it involves just a single, simple calculation.
2. Inserting an Element at beginning: O(n)
  - This requires shifting all other elements, hence O(n)
3. Inserting an Element at end
  - If array is full: O(n) : array needs to be copied in its entirety to a new block of memory
  - If array is not full: O(1) : if there's still room allocated (let's say there's one more 24 byte block free for an array), then we can mutate the contents of memory at that byte block's address without having to copy the array into another (more spacious) location.

## Multidimentional arrays

Java does _not_ support two- or higher-dimensional arrays!  However, you can emulate them by one of two methods:

1. **Arrays of arrays**: Since Java allows you to create an array of arrays, you can use nested arrays for higher dimensions.

  Note that _each_ inner array must separately be allocated: Java does not create them for you!  This code demonstrates how to do this for an array of `numRows` rows and `numCols` columns.

  ```java
  int[][] arr = new int[numRows][];     // Note syntax!
  for (int i = 0; i < arr.length; ++i)
      arr[i] = new int[numCols];
  ```

  Because each inner array is allocated separately, you are at liberty to make them different lengths.  This is called a **ragged array**.

  The element in row `r` and column `c` is `arr[r][c]`.

1. **Index arithmetic**: A two- or higher-dimensional array may be "flattened" into a one-dimensional array by performing index manipulations.  For example, a two-dimensional array of `numRows` and `numCols` can be stored in a one-dimensional array of length `numRows * numCols`.

  The element with row `r` and column `c` is stored at index `r * numCols + c` in the one-dimensional array, _i.e._ `arr[r * numCols + c]`.

# Exercises

> :dart: **Exercise:** Reversing an array:
>
> 1. Write a method that accepts an `int[]` and returns a new, reversed array.
> 1. Write a method that accepts an `int[]` and reverses the elements _in place_, i.e. it rearranges elements in the array passed to the method.
> 1. Write equivalent _generic_ methods, _e.g._ `reverse<T>(T[] arr)` and `reverseInPlace<T>(T[] arr)`.
>
> Collect your methods (which should be static) into a single class.

<div></div>

> :dart: **Exercise:** A **bit vector** behaves like a list of booleans; however, the booleans are encoded as individual bits in a larger integer type such as `int` or `long`.  This is eight times as efficient as an array of `boolean`, each of which occupies one byte.
>
> Write a `BitVector` class.  It should accept a length, in bits, at construction, and provide `set(index, bit)` and `get(index)` methods, where the individual bits are represented by booleans.  Your class should use about `length / 32` integer values or `length / 64` long values to store the bits.

<div></div>

> :dart: **Exercise:** A **sparse array** is an array that has only a few elements set relative to its length; most elements are 0 (for numeric arrays) or `null` (for object arrays).  A sparse array is represented more efficiently by a sequence of (index, value) pairs.
>
> For example, the array `{ 0, 0, 3, 0, 8, 0, 0 }` could be represented by the pairs (2, 3) and (4, 8), where the first entry in each pair is an index and the second entry is a value.  All other items are assumed to be zero.
>
> Write a method that converts a `double[]` array into a `List<Entry>`, where `Entry` is a class you create that contains an integer index and a double value.  This method should add an entry to the list only for items in the array that are nonzero.
>
> Then write a corresponding method that converts the list of entries back into an explicit array.
>
> Verify that a round trip through your methods returns the original array, for a variety of test cases.

<div></div>

> :dart: **Exercise:** Write a `Matrix` class that stores a two-dimensional mathematical matrix of `double` values.  Accept the number of rows and columns in the constructor.  Provide a `get(row, col)` accessor and a corresponding `set(row, col, value)`.  Provide a `toString()` that prints matrix out in the traditional format, with "(" and ")" characters on the left and right, respectively.

<div></div>

> :dart: **Exercise:** Implement your own `ArrayList` from scratch.  It should be functionally identical to the original.
>
> 1. Write unit tests for `ArrayList<Double>`.
>   - Make sure you test each method.
>   - Make sure you test cases with empty and non-empty lists.
>   - Make sure you test error conditions as well as correct usage.
> 1. Verify that your tests work as expected on the standard `ArrayList` class.
> 1. Create your own `ArrayList<T>` that implements `List<T>`.  Use IntelliJ to fill in all the methods you need.
> 1. Implement the methods, running tests as you go.

<div></div>

> :dart: **Exercise:** A **native collection** is a collection class specific to a single native type.  Java developers often use a native collection instead of a generic collection to avoid boxing/unboxing operations, reduce memory use, and improve performance.
>
> Write a `DoubleArrayList` class that accepts and returns `double` values instead of `Double` objects.
>
> Write some simple benchmarks for the basic operations, and compare performance of your class versus `ArrayList<Double>`.

## Linked List

A linked list is a way of storing information.  A linked list consists of a series of nodes.  Each node contains data, as well as a pointer to the next node in the series.

![Linked list picture](https://upload.wikimedia.org/wikipedia/commons/6/6d/Singly-linked-list.svg)

|Linked List| Array |
|---|---|
|Ordered|Ordered|
|One Dimensional|One Dimensional|
|Indexed|Indexed|
|Variable Size|Fixed Size|
|Mutable|Mutable|

##Common Operations

### Access an element

![Linked List Access](https://upload.wikimedia.org/wikipedia/commons/6/6d/Singly-linked-list.svg)

- Runtime: O(n)
- Explanation: In order to access the node at index 4, we need to 	visit every node before it.

### Insert an element

![Linked List Insertion](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4b/CPT-LinkedLists-addingnode.svg/474px-CPT-LinkedLists-addingnode.svg.png)


- Runtime: O(1)
- Explanation: We can insert a node in constant time by changing the 	pointer of the previous node to point to the new 	node.


### Find an element

![Linked List Find](https://upload.wikimedia.org/wikipedia/commons/6/6d/Singly-linked-list.svg)

- Runtime: O(n)
- Explanation: In order to find an element, we have to look at each 	node in the linked list.

### Delete an element

![Linked List Delete](https://modernpathshala.com/Images/singly-linked-list/Article/276195620161604035916Delete-Node-In-Linked-List.JPG)


- Runtime: O(1)
- Explanation: We need to change the pointer of a node to the node 	after the node we want to delete.

### Node Implementation

We can make a functional linked list of Ints with only a Node class.

```java
class Node {
    private Integer value;
    private Node next;
}
```

But what if we want to be able to make our Linked List Node not limited just to Ints?

### Generics

Generics are a powerful tool in Java that lets us extend code to multiple different types.  The symbol: 'T' indicates a generic.  Let's rewrite the code from above:

```java
class Node<T> {
	private T value;
	private Node<T> next;
}
```

The 'T' in angle brackets indicates that the class will use generics.
