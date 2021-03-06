# Welcome to willyOS !
  
[![Build Status](https://travis-ci.org/ZenMaster91/uniovi.tpp.svg?branch=master)](https://travis-ci.org/ZenMaster91/uniovi.tpp)
![Test Status](https://img.shields.io/badge/tests-passing-brightgreen.svg)
[![GitHub issues](https://img.shields.io/github/issues/ZenMaster91/uniovi.tpp.svg)](https://github.com/ZenMaster91/uniovi.tpp/issues)
[![GitHub forks](https://img.shields.io/github/forks/ZenMaster91/uniovi.tpp.svg)](https://github.com/ZenMaster91/uniovi.tpp/network)
[![GitHub stars](https://img.shields.io/github/stars/ZenMaster91/uniovi.tpp.svg)](https://github.com/ZenMaster91/uniovi.tpp/stargazers)
[![GitHub license](https://img.shields.io/badge/license-AGPL-blue.svg)](https://raw.githubusercontent.com/ZenMaster91/uniovi.tpp/master/LICENSE)   

This repository includes all code performed during the subject of TPP from prof. Jose Manuel Redondo at the University of Oviedo. Anyway, to give some structure it's presented as an API called willyOS. The structure of this API might be different from the structure followed during the labs because it refers more to the big picture of the subject than to the individual labs. Because of this reason the structure is the following:

```php
 - willyOS
   - SDK
     - CoreServices
       - ...
     - Foundation
       - ...
     - RandomKit
       - ...
     - RealWorldKit
       - ...
     - ...
     
 - willyOSTests
   - SDKTest
     - ... Same structure
```

> ### Note
> 
> The tests that come with willyOS are written using the framework NUnit. You can find more information at: https://www.nunit.org. After the installation remember that you have to import the `NUnit.framework` at the beginning of your test class.
> ```C#
> using NUnit.Framework;
> ```

### Quickly Access
* [CoreServices](#coreservices)
  *  [CSFunctions](#csfunctions)
* [Foundation](#foundation)
  * [INSDictionary](#insdictionary)
  * [INSList](#inslist)
  * [INSStack](#insstack)
  * [NSDictionary](#nsdictionary)
  * [NSLinkedListNode](#nslinkedlistnode)
  * [NSList](#nslist)
  * [NSStack](#nsstack)

# CoreServices - `Deprecated`
The Core Services provide functions and resources that build the core of the API.

## CSFunctions
###  Overview
This class provide the three basic core functions that are Find, Filter and Reduce. This functions are declared as static so there's no need of creating an instance of this class to call any of its functions. In willyOS this functions are implemented with generics so they accept any kind of data.  

#### Find Function
Find function return the first appearance of the element that matches a given predicate in a given collection.   
**Predicate <T> f:** The predicate that is going to be applied over the elements of the enumerable.   
**IEnumerable<T> e:** The enumerable to apply the predicate.   
```C#
    T Find<T>(Predicate<T> f, IEnumerable<T> e)
```
  
To use the `Find` function:
  
```C#
    // An NSList of 'int' elements
    var oddNumbers = new NSList<int>() { 1, 3, 5, 7, 9, 11, 13, 15 };

    // An NSList of 'String' elements
    var streets = new NSList<string>() { "Albemarle", "Brandywine", "Chesapeake" };

    var number = CSFunctions.Find(n => n == 7, oddNumbers);
    Console.WriteLine(number);
    // Prints 7

    var street = CSFunctions.Find(n => n.Equals("WallStreet"), streets);
    Console.WriteLine(street);
    // Nothing will be printed as street = null. That is the default(string);
```
   
#### Filter Function
Returns the first element in a collection that fulfills a specific predicate. If no suitable element exists, the default value is returned.  
**Predicate <T> f:** The predicate that is going to be applied over the elements of the enumerable.   
**IEnumerable<T> e:** The enumerable to apply the predicate.   
```C#
    IEnumerable<T> Find<T>(Predicate<T> f, IEnumerable<T> e)
```
  
To use the `Filter` function:
  
```C#
    // An NSList of 'int' elements
    var oddNumbers = new NSList<int>() { 1, 3, 5, 7, 9, 11, 13, 15 };

    var number = CSFunctions.Filter(n => n < 7, oddNumbers);
    Console.WriteLine(number);
    // Prints: List -> [1] -> [3] -> [5] ->
```
  
#### Reduce Function
Returns the application of a function to all the elements of a collection, so a single value is returned storing the computation done with all the collection elements.   
**Func<TResult, TInput, TResult> f:** The to perform over the enumerable collection.   
**IEnumerable<T> en:** The enumerable to apply the function.   
**TResult seed:** The type of the result. 
```C#
    TResult Reduce<TInput, TResult>(Func<TResult, TInput, TResult> f, IEnumerable<TInput> en, TResult seed = default(TResult))
```
   
To use the `Reduce` function:
  

```C#
    // An NSList of 'int' elements
    var oddNumbers = new NSList<int>() { 1, 3, 5 };

    var number = CSFunctions.Reduce((e1, e2) => e1 + e2, oddNumbers, new int());
    Console.WriteLine(number);
    // Prints 9
```
  

# Foundation
Access the essential classes that define basic object behavior, data types, collections, and operating-system services. Incorporate design patterns and mechanisms that make your apps more efficient and robust.

## INSDictionary
### Overview
The INSDictionary class declares the programmatic interface to objects that manage immutable associations of keys and values.
    
> ### Inherits From
>    [IDictionary](https://msdn.microsoft.com/es-es/library/s4ys34ea(v=vs.110).aspx)
  
## INSList
### Overview
Next Step List interface. A list type that is also enumerable has to implement this interface.
    
### Interface Methods
```C#
    void SafeCopyTo(ref T[] array, int arrayIndex);
```
  
> ### Inherits From
>    [IList](https://msdn.microsoft.com/es-es/library/5y536ey6(v=vs.110).aspx),
>    [IEnumerable](https://msdn.microsoft.com/es-es/library/9eekhta0(v=vs.110).aspx)
   
## INSStack
### Overview
Declares the programatic interface to objects that behaves like an stack.

### Interface Methods
```C#
    void Push(object element);
    void Pop()
```
   
## NSDictionary
### Overview
The NSDictionary class declares the programmatic interface to objects that manage immutable associations of keys and values. 
A key-value pair within a dictionary is called an entry. Each entry consists of one object that represents the key and a second object that is that key’s value. Within a dictionary, the keys are unique.

> ### Inherits From
>    [Dictionary](https://msdn.microsoft.com/es-es/library/xfhwa508(v=vs.110).aspx)
  
## NSLinkedListNode
### Overview
The NSLinkedListNode represents a node of a linked list. A node is a container that has its own value and a pointer to the next node.
  
### Creating new NSLinkedListNodes
With this API the nodes creation is really easy. For example:
   
```C#
     // secondOddNumber is a NSLisnkedListNode that can store integer values.
    var secondOddNumber = new NSLinkedListNode<int>() {
        Value = 3
    };

    // firstOddNumber is a NSLisnkedListNode that can store integer values. And has secondOddNumber as Next value;
    var firstOddNumber = new NSLinkedListNode<int>() {
        Value = 1, Next = secondOddNumber
    };

    // Now, personNode will be a node that can store people.
    var personNode = new NSLinkedListNode<Person>() {
        Value = new Person(name: "John", surname: "Appleseed", age: 50)
    };
```
   
### Accesing NSLinkedListNode properties
From a NSLinkedListNode pointer you can access to its properties: **Value** That represents the content of the node. And **Next** that is a pointer to the next node. For example:
    
```C#
    // We're getting the value of the second odd number from the first one, first accessing to its next property and the to the value if posibble.
    var secondOddNumberFromFirst = firstOddNumber.Next?.Value;
    Console.WriteLine(firstOddNumber);
    // Prints 3
    
```
    
### Traveling from NSLinkedListNode to the Next NSLinkedListNode
Sometimes you will need to travel from one node to the following one, for example in a linked list. With the willyOS implementation cannot be easy.
    
```C#
    // We create some nodes. We create them in inverse order to link them in a natural order.

    var three = new NSLinkedListNode<string>() {
        Value = "three"
    };

    var two = new NSLinkedListNode<string>() {
        Value = "two", Next = three
    };

    var one = new NSLinkedListNode<string>() {
        Value = "one", Next = two
    };

    // Lets travel from one to two.
    val pointer = one.Next;
    Console.WriteLine(pointer);
    // Prints [NSNode: Value=two, Next=[NSNode: Value=three, Next=]]
```
    
> ### Conforms To
>    [IEquatable](https://msdn.microsoft.com/es-es/library/ms131187(v=vs.110).aspx)
  
## NSList
###  Overview
Lists are one of the most commonly used data types in an app. You use lists to store your app’s data. Specifically, you use the NSList<T> type to hold elements of a single type, the list’s Element type (T). A list can store any kind of elements—from integers to strings to classes.
willyOS makes it easy to create lists in your code using literals: simply surround a comma separated list of values with curly brackets. Without any other information, willyOS creates a list that includes the specified values, automatically inferring the array’s Element type.  
For example:

```C#
    // An NSList of 'int' elements
    var oddNumbers = new NSList<int>() {1, 3, 5, 7, 9, 11, 13, 15};

    // An NSList of 'String' elements
    var streets = new NSList<string>() {"Albemarle", "Brandywine", "Chesapeake"};

    // An empty NSList
    var emptyList = new NSList<string>();
```

> ### Note
> 
> Remember to use the corresponding import at the beginning of your class to use NSList. As NSList is allocated at Foundation:
> ```C#
> using Foundation;
> ```



###  Accessing NSList Values
When you need to perform an operation on all of an list's elements, use a foreach loop to iterate through the list’s contents.

```C#
    foreach(string street in streets) {
        Console.WriteLine("I don't live on {0}.", street);
    }
    // Prints "I don't live on Albemarle."
    // Prints "I don't live on Brandywine."
    // Prints "I don't live on Chesapeake."
```

Use the IsEmpty property to check quickly whether a NSList has any elements, or use the Count property to find the number of elements in the list.

```C#
    if oddNumbers.IsEmpty {
        Console.WriteLine("I don't know any odd numbers.");
    } else {
        Console.WriteLine("I know {0} odd numbers.", oddNumbers.Count);
    }
    // Prints "I know 8 odd numbers."
```

You can access individual list elements through a subscript. The first element of a nonempty list is always at index zero. You can subscript a lis with any integer from zero up to, but not including, the count of the list. Using a negative number or an index equal to or greater than count triggers a runtime error. For example:

```C#
    Console.WriteLine(oddNumbers[0].ToString(), oddNumbers[3].ToString());
    // Prints 1 - 7

   Console.WriteLine(emptyDoubles[0]);
    // Triggers runtime error: Index out of range
```

### Adding and Removing Elements
Suppose you need to store a list of the names of students that are signed up for a class you’re teaching. During the registration period, you need to add and remove names as students add and drop the class.

```C#
    var students = new NSList<string>() {"Ben", "Ivy", "Jordell"};
```

To add single elements to the list, use the Add(T item) method.

```C#
    students.Add("Maxime");
    // ["Ben", "Ivy", "Jordell", "Maxime"]
```

You can add new elements in the middle of a list by using the Insert(int index, T item) method for single elements. The elements at that index and later indices are shifted back to make room.

```C#
    students.Insert("Liam", 3);
    // ["Ben", "Ivy", "Jordell", "Liam", "Maxime"]
```

To remove elements from a list, use the Remove(T item) or RemoveAt(int index) methods.

```C#
    // Ben's family is moving to another state
    students.RemoveAt(0);
    // ["Ivy", "Jordell", "Liam", "Maxime"]

    // Liam is signing up for a different class
    students.Remove("Liam");
    // ["Ivy", "Jordell", "Maxime"]
```

You can replace an existing element with a new value by assigning the new value to the subscript.

```C#
    var MaxIndex = students.IndexOf("Maxime");
    if(MaxIndex =! -1) {
        students[MaxIndex] = "Max";
    }
    // ["Ivy", "Jordell", "Max"]
```

> ### Conforms To
>    [INSList](#inslist)
  
## NSStack
### Overview
A stack is an abstract data type that serves as a collection of elements. Here we use LIFO (Last In First Out). With a NSStack you can perform Push(object item) and Pop(). The decision of implementing the NSStack as a non generic was made on that a stack is there to store any kind of object during some time and than poping it. So we don't want to make compulsory to instanciate one stack per type you need to store. To create an NSStack for example:
   
```C#
    // By default the stacks are initialised with 10 positions.
    var stack = new NSSTack();

    // But you can also set the number of maximum elements in the stack by passing it to the constructor. For example 100 positions.
    var bigStack = new NSSTack(100);
```
 
### Adding and Getting elements from the NSStack
As described in the overview the NSStack has a LIFO policy so that:
   
```C#
    // To add elements to any NSStack use the Push(object element)
    stack.Push(1);
    stack.Push(3);
    stack.Push(5);
    stack.Push(7);
    // stack staus: [7, 5, 3, 1]

    // To get the elements from the stack use Pop() that returns an object.
    var number = stak.Pop();
    Console.WritteLine(number);
    // Prints 7;
    // stack staus: [5, 3, 1]

    // Now if we Pop() another element from the stack...
    number = stak.Pop();
    Console.WritteLine(number);
    // Prints 5;
    // stack staus: [3, 1]
```
  
Use the IsEmpty IsFull to check quickly the status of the stack:
   
```C#
    Console.WriteLine(bigStack.IsEmty);
    // Prints true as bigStack has no elements.

    Console.WriteLine(stack.IsEmty);
    // Prints false as stack has some elements.

    Console.WriteLine(stack.IsFull);
    // Prints false as stack has some elements but has not reach its maximum.
```


> ### Conforms To
>    [INSStack](#insstack)
