# Naming Convention
## class name
- **No spaces** in the class name.
- **Case-sensitive**: `MyClass` and `myclass` are considered different.
- **Start with an uppercase letter** (by convention).
- **Cannot be a reserved keyword** (e.g., `class`, `public`, `interface`, etc.).
- **No special characters** other than underscores (`_`) and dollar signs (`$`).
- **Can start with an underscore (`_`) or a dollar sign (`$`)**.
- After the first character, a class name can contain:
    - Letters (A-Z, a-z)
    - Digits (0-9)
    - Underscores (`_`)
    - Dollar signs (`$`)
    Examples: `MyClass123`, `Helper_Class`, `My$Helper`

# Access Modifiers

| **Access Modifier**           | **Top-Level Class** | **Same Package (Class Member)** | **Subclass (Same Package)** | **Subclass (Different Package)** | **World (Other Classes)** |
| ----------------------------- | ------------------- | ------------------------------- | --------------------------- | -------------------------------- | ------------------------- |
| **public**                    | ✅ Yes               | ✅ Yes                           | ✅ Yes                       | ✅ Yes                            | ✅ Yes                     |
| **protected**                 | ❌ No                | ✅ Yes                           | ✅ Yes                       | ✅ Yes                            | ❌ No                      |
| **default (package-private)** | ✅ Yes               | ✅ Yes                           | ✅ Yes                       | ❌ No                             | ❌ No                      |
| **private**                   | ❌ No                | ✅ Yes (Only within class)       | ❌ No                        | ❌ No                             | ❌ No                      |

#### Explanation:
1. **`public`** → Accessible **everywhere** (inside and outside the package, subclass, and world).
2. **`protected`** → Accessible within the **same package** and **subclasses in other packages**.
3. **`default (package-private)`** → Accessible only within the **same package**.
4. **`private`** → Accessible only within the **same class** (not even in subclasses).

+ **Class** are either **public or default** but can not be private or protected.



# Loops

**Note :**
```java
if (condition1 && condition2) {
    // Executes only if both condition1 and condition2 are true
}
```
above code: it check condition 1 and if it is true then check condition 2 otherwise returns false without checking condition 2

# In built methods :
**`strip()`** vs **`trim()`**: both remove white spaces and **`\n`** but strip is new and remove all kind of whitespaces like tab .



---
# Searching and Sorting

# [Binary Search](https://www.w3schools.com/dsa/dsa_algo_binarysearch.php)
+ works on sorted array only




---
# OOPS

---

## this keyword
+ In Java, the `this` keyword refers to the current instance of a class. 
+ to get reference of current object
+ It is used to refer to instance variables, methods, or the current object. 
+ It is especially useful when you have parameter names that are the same as instance variables. i.e.
```java
public class Car {
    private int wheels;
    private String color;

    public Car(int wheels, String color) { //constructor
        this.wheels = wheels;
        this.color = color;
    }
}
```


## final keyword
+ to finalise(fix) value .
+ final function can not be override.
+ final class can not be inherited by other class 
+ final class can not inherit other class

## static keyword
<u><b>Use case Scenario :</b></u>
+ jo property or method same rehne wale h multiple instances(object) of class, unko hum static bana dete h.
+ when we want to call method without creating on object.
+ Agar koi property ya method individual objects par depend nahi karti aur class level par share ki jati hai, tab hum usse `static` bana dete hain.

+ we make main class as static so that JVM can call it with class name without making its instance.
+ `this` for `super` keyword can't be used inside static function.
+ constructor can't be static
+ static function can not use non static function and variable.
+ static method is accessed using class name not object.
```java
class MyClass {
    // Static method
    static void greet() {
        System.out.println("Hello from the static method!");
    }
}

public class Main {
    public static void main(String[] args) {
        // Accessing the static method using the class name
        MyClass.greet();
    }
}

//In this example, the `greet()` method is static, and it's called using `MyClass.greet()` instead of creating an object of `MyClass`.
```

## super keyword

+ **Calling a Parent Class Method and Property:** If the child class has a method with the same name as the one in the parent class, super allows you to call the parent class method.

+ **Calling the Parent Class Constructor:** super() can be used to call the constructor of the parent class when creating an object of the child class.
+ i.e. **`super()`**

# Constructor

**Constructor Format** :  `<Access Modifier> <Constructor Name> (parameters)`
+ used to initialize objects
+ constructor name same as class name
+ no return type
+ Automatically called when an object is created

# Encapsulation

+ All properties and methods related to that class at one place .
+ hiding of data using getter and setter


# Inheritance

+ Used for acquiring properties of other class.
+ Uses extend keyword.
+ When child class constructor is called to create object ,it also calls the parent class constructor which creates parent object too.(in inheritance).
+ You can not extend more than one class but can implement multiple interface in a class.
+ The class being inherited from is called the **superclass**, and the class that inherits is called the **subclass**.

```java
class Superclass {
    // Superclass fields and methods
}

class Subclass extends Superclass {
    // Subclass can have its own fields and methods
    // It can also override methods from the superclass
}
```


**Scenario 01:**
Suppose a vehicle has private property and it is accessible using getter and setter.
Now the car is extending vehicle . so the car also have that private property but can't directly access it. can access using getter and setter.


# Abstraction

<u><b>Use case Scenario :</b></u>
When you want a method should(forced) be implemented in every subclass but defined(not implemented) in parent class.

+ Means to show only necessary detail to user. 
+ why? for encapsulation
+ Use abstract keyword
+ Method can be abstract or non abstract
+ Can have constructor.
+ Can have static method.
+ If a method is abstract then the class is also have to be abstract. (parent class)  or (if a class contains **at least one abstract method**, the class itself **must be declared as abstract**.)
+ A class that inherits from an abstract class must provide implementations for the abstract methods, unless it is also abstract. (child class)

i.e.
```java 
abstract class Animal {
    // Abstract method (no implementation)
    abstract void sound();
    
    // Concrete method
    void sleep() {
        System.out.println("This animal sleeps.");
    }
}

class Dog extends Animal {
    // Providing implementation for the abstract method
    void sound() {
        System.out.println("Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.sound();  // Woof!
        myDog.sleep();  // This animal sleeps.
    }
}
```



# Interface

+ Use interface keyword (parent class)
+ Its a pure abstract (only abstract methods)
+ All methods are abstract (by default).
+ Can also have default or static methods.
+ All properties (field) are either public , static or final.
+ In Java, interfaces cannot **`implement`** other interfaces
+ Multiple inheritance
	1. A **class** can implement more than one **interface**.
		When you **`implement`** an interface, you're creating a class that must provide implementations for the methods defined in the interface(s).
	2. An **interface** can extend more than one **interface**.
		When you **`extend`** an interface, you're creating a new interface that inherits the methods of the interfaces you're extending.
+ To inherit interface class we use implement keyword.
+ (child class) which uses implement either use abstract to make class abstract or implement all methods of parent class.
+ mostly not contain data member but if then it is of type final and static. (to store constant)

i.e.
```java
public interface VehicleInterface{
	public final static double PI=3.14; //data member
	public int getMaxSpeed(); // method
	public void print();  //method
}
```


| Feature                | **Static Binding**                         | **Dynamic Binding**                         | **Method Overloading**                     | **Method Overriding**                       |
|------------------------|----------------------------------------|----------------------------------------|----------------------------------------|----------------------------------------|
| **Definition**         | The method call is resolved at **compile-time**. | The method call is resolved at **runtime**. | Multiple methods in the same class with the same name but different parameters. | A subclass provides a specific implementation of a method that is already defined in its parent class. |
| **Binding Type**       | **Early Binding** (compile-time)       | **Late Binding** (runtime)            | **Early Binding** (compile-time)       | **Late Binding** (runtime)            |
| **Which Methods?**     | **Static, private, and final methods** | **Non-static (instance) methods**     | Any method with different parameters in the same class | Only instance (non-static) methods |
| **Decided At**         | **Compile-time**                       | **Runtime**                           | **Compile-time**                       | **Runtime**                           |
| **Polymorphism Type**  | **Not polymorphic** (No dynamic behavior) | **Runtime polymorphism**              | **Compile-time polymorphism**          | **Runtime polymorphism**              |
| **Inheritance Needed?** | ❌ No                                   | ✅ Yes (parent-child relationship)   | ❌ No                                   | ✅ Yes (must be in subclass)         |
| **Return Type**        | Can be different                       | Must be the same or covariant        | Can be different                       | Can be the same or covariant         |
| **Access Modifier Rule** | Can be more restrictive               | Cannot reduce visibility (must be the same or more accessible) | Can be different                       | Cannot be more restrictive than the overridden method |
| **Example**           | Calling a static method                | Calling an overridden method         | Methods with different parameters     | Subclass providing a different implementation |

# Static Binding (Early Binding)
- It occurs when the method to be called is determined at **compile-time**. This typically happens with **static methods**, **private methods**, and **final methods**, where the method call is resolved based on the reference type, not the actual object type.
i.e.
```java
class Animal {
    // Static method in parent class
    static void sound() {
        System.out.println("Animal makes a sound");
    }

    // Private method in parent class
    private void show() {
        System.out.println("I am an animal");
    }
}

class Dog extends Animal {
    // Static method in child class
    static void sound() {
        System.out.println("Dog barks");
    }

    // Private method in child class
    private void show() {
        System.out.println("I am a dog");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog();  // Reference is of type Animal, object is of type Dog
        // Static method: static binding happens based on reference type (Animal)
        animal.sound();  // Output: Animal makes a sound
        // Private method: can't override, and static binding occurs with reference type (Animal)
        // animal.show();  // Compiler error: show() has private access in Animal
    }
}

```

# Method hiding
* occurs when a **static method** in a parent class is overridden by a **static method** in a child class.
i.e.
```java
class Parent {
    static void show() {
        System.out.println("Parent show()");
    }
}

class Child extends Parent {
    static void show() {
        System.out.println("Child show()");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent p = new Parent();
        Parent c = new Child();
        
        p.show(); // prints: Parent show()
        c.show(); // prints: Parent show() because the reference type is Parent
    }
}
```

# Dynamic Binding(late binding)
+ **Dynamic binding** is the process of determining the method to call at runtime based on the actual object type, rather than the reference type.
+ Method Overriding is a perfect example of dynamic binding.

```java
class Parent {
    void show() { // Non-static method
        System.out.println("Dynamic Binding: Parent Class");
    }
}

class Child extends Parent {
    void show() { // Overriding method
        System.out.println("Dynamic Binding: Child Class");
    }

    public static void main(String[] args) {
        Parent obj = new Child(); // Reference of Parent, object of Child
        obj.show(); // Output: Dynamic Binding: Child Class
    }
}
```



# Polymorphism (multiple forms)

i.e. vehicle class is parent and car class is child then 
**`vehicle v = new car();`**  
This allows you to treat `Car`, `Truck`, `Bike`, etc., as a **general** `vehicle` type. The specific object (`car` in this case) is still able to perform its own actions, but the code that handles it is written generically for **all vehicles**.

why? bcz
**Reusability**:  
Your code can be reused for any subclass of `vehicle`. For example, `vehicle v = new Truck()` or `vehicle v = new Bike()` would work the same way. You can write methods that treat all vehicles in a unified way, no matter their specific type.

### 1. Compile Time polymorphism or Function overloading or Static Polymorphism
 + same method name but with different parameter.

```java
class Overloading {
    void show(int a) {
        System.out.println("Method with int: " + a);
    }

    void show(double b) {
        System.out.println("Method with double: " + b);
    }

    void show(String s) {
        System.out.println("Method with String: " + s);
    }

    public static void main(String[] args) {
        Overloading obj = new Overloading();
        obj.show(10);       // Output: Method with int: 10
        obj.show(10.5);     // Output: Method with double: 10.5
        obj.show("Hello");  // Output: Method with String: Hello
    }
}
```
 

### 2. Runtime Polymorphism or Function Overriding or Method Overriding

+ Function overriding occurs when a child class provides its own implementation of a method already defined in the parent class, replacing the parent's version.
+ Occurs in a subclass that inherits from a parent class.
+ if called then first it check if child has that method if not then parent class


i.e. vehicle is parent class and car is child class
```java
vehicle v=new car();
v.isconvertable();
```
+ but here we can't do car specific thing cause **`isconvertable`** is defined in car not in vehicle, and we can do only vehicle specific things. above code will give error.

+ but we can access car specific method by casting it to car type if instance of car exist.

```java 
class Vehicle {
    void move() {
        System.out.println("Vehicle is moving");
    }
}

class Car extends Vehicle {
    void isConvertible() {
        System.out.println("This car is convertible.");
    }

    @Override
    void move() {
        System.out.println("Car is driving");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle v = new Car();  // Vehicle reference to a Car object
        
        v.move();  // Calls Car's move() method (runtime polymorphism)

        // If we want to call Car-specific methods
        if (v instanceof Car) {
            Car car = (Car) v;  // Cast to Car
            car.isConvertible();  // Now you can call Car-specific methods
        }
    }
}

```


i.e. Let’s say both the **`Vehicle`** class and the `Car` class have a **`print()`** method.

```java
class Vehicle {
    void print() {
        System.out.println("Printing Vehicle details");
    }
}

class Car extends Vehicle {
    @Override
    void print() {
        System.out.println("Printing Car details");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle v = new Car();  // Vehicle reference to a Car object
        v.print();  // This will call the print() method from the Car class
    }
}

```

**Dynamic Method Dispatch**: (only for method overriding)
- In the line **`Vehicle v = new Car();`**, the reference **`v`** is of type **`Vehicle`**, but it actually points to a **`Car`** object.


# Exception Handling

### Basic Steps for Handling Exceptions:

1. **Throwing an Exception**:  
    A method can throw an exception when it encounters an error and cannot handle it itself.
    
2. **Declaring Exceptions**:  
    If a method throws an exception, it must either handle it or declare it using `throws`.
    
3. **Exception Propagation**:  
    If an exception is thrown and not handled in the method, it propagates (bubbles up) to the calling method. This continues until it reaches the `main()` method or the program terminates.

4. **Handling Exceptions**:  
    A method can catch exceptions using a `try-catch` block, or it can propagate it further by declaring it with `throws`.


### Throwing exception

using **`throw`** keyword
```java
throw new Exception("This is a custom exception.");
```

When a method might throw a checked exception, it must either handle it or declare it using the **`throws`** keyword in the method signature.
```java
public void readFile() throws ExceptionType {
    // Code that may throw an Exception
    throw new Exception("This is a custom exception.");
}
```

```java
public class ExceptionType extends Exception {

}
```


### Handling exception using **`try-catch`** block

in main block
```java
try {
    // Code that might throw an exception
} catch (ExceptionType e) {
    // Code to handle the exception
} finally {
    // Code that will run no matter what (optional)
}
```

**NOTE :** 
+ We are not allowed to catch generalized exception before specific exception.



# Generics

<u><b>Use case Scenario :</b></u>
Generics in Java allow us to create one class or method that works with **any type** of data, like `Integer`, `String`, or even custom types, without needing to write separate versions for each.

+ Generics in Java allow you to write classes, interfaces, and methods that can operate on objects of various types while providing compile-time type safety.
+ uses angle brackets (`< >`)
+ `<T>` is a placeholder for a type that will be specified when an object is created (e.g., `Pair<Integer>` or `Pair<String>`).

i.e.
```java
package generics;

public class Pair<T> {
	private T first;
	private T second;
	
	public Pair(T first,T second){
		this.first=first;
		this.second=second;
	}
	
	public T getFirst(){
		return this.first;
	}
	
	public T getSecond(){
		return this.second;
	}
	
	public void setFirst(T first){
		this.first=first;
	}
	
	public void setSecond(T second){
		this.second=second;
	}
}
```

```java
package generics;

public class PairUse{
	public static void main(String[] args){
		Pair<Integer> p1=new Pair<Integer>(5,10); //Integer is a wrapper class
		p1.setFirst(10);
		int f1=p1.getFirst();
		
		Pair<Integer> p2=new Pair<>(5,10); //this is also fine
	}
}
```

Above we used Wrapper class **`Integer`** 

### Wrapper class
+ It wraps the primitive data type into an object so we can use it as object.
+ Like collections (i.e Arraylist) can only store objects.

| Primitive Type | Wrapper Class  |
|----------------|----------------|
| `int`          | `Integer`      |
| `char`         | `Character`    |
| `byte`         | `Byte`         |
| `short`        | `Short`        |
| `long`         | `Long`         |
| `float`        | `Float`        |
| `double`       | `Double`       |
| `boolean`      | `Boolean`      |
## Multiple Generic Types:
This refers to use of multiple generic type parameters in class , method or interface.

i.e.
```java
public class Pair<T,U>{
	private T first;
	private U second;
	
	public Pair(T first,U second){
		this.first=first;
		this.second=second;
	}
	
	private void setFirst(T first){
		this.first=first;
	}
	
	private void setSecond(U second){
		this.second=second;
	}
	
	private T getFirst(){
		return this.first;
	}
	
	private U getSecond(){
		return this.second;
	}
}
```

```java
public class PairUse{
	public static void main(String[] argss){
		Pair<Integer,String> p1=new Pair<>(45,"Hello");
	}
}
```

## Chained Generic Type
Chained generic types occur when you use one generic type as the argument for another generic type.

```java
package generics;
public class Pair<T,U>{
	private T first;
	private U second;
	
	public Pair(T first,U second){
		this.first=first;
		this.second=second;
	}
	
	public T getFirst(){
		return this.first;
	}
	
	public U getSecond(){
		return this.second;
	}
	
	public void setFirst(T first){
		this.first=first;
	}
	
	public void setSecond(U second){
		this.second=second;
	}
}
```

```java
package generics;
public class PairUse{
	public static void main(String[] args){
		int a=10;
		int b=20;
		int c=30;
		Pair<Integer,Integer> p1=new Pair<>(a,b);
		Pair<Pair<Integer,Integer>,Integer> p2=new Pair<>(p1,c);
		System.out.println(p2.getSecond()); //to get third integer
		System.out.println(p2.getFirst().getSecond()); // to get second integer
		System.out.println(p2.getFirst().getFirst()); // to get first integer
	}
}
```

## Generic Method
Methods can also be made generic, which means you can specify a type parameter for the method, independent of the class.

i.e.
```java
public class GenericMethodExample{
    // [access modifier] [other modifier] <T> [return type] [method name] ([parameter type] [parameter name])
    //other modifier i.e. static,final,abstract etc
	public static <T> void printArray(T[] arr){  //T[] arr parameter array of type T is an array
		for(T element: arr){
			System.out.println(element+" ");
		}
		System.out.println();
	}
	
	
	public static void main(String[] args){
		Integer[] intArray={1,2,3,4}; //wrapper class Integer
		String[] strArray={"Hello","World"}; //wrapper class String
		
		printArray(intArray); // output: 1 2 3 4
		printArray(strArray); //output: Hello World
	}
}
```


## Bounded Type Parameters
You can restrict the types that can be passed to a generic class, method, or interface by using bounds.

```java
public class BoundedTypeExample{
	//Method with bounded type parameter
	public static <T extends Number> void printNumber(T num){
		System.out.println("Number"+num);;
	}
	
	public static void main(String[] args){
		printNumber(5); //works (Integer extends Number) ,here we didn't used wrapper bcz of autoboxing
		printNumber(5.5); //works (Double extends Number)
		
		//printNumber("Hello") //compile-time error (String does not extend Number)
	}
}
```

In this example, the method `printNumber` only accepts objects of types that extend `Number` (such as `Integer`, `Double`, etc.).

we can also use extend of different class i.e. Vehicle class

### autoboxing mechanism
Java automatically converts primitive types like int or double to their corresponding wrapper objects (Integer, Double, etc.) because the type parameter `T` extends `Number`.

## Wildcards in Generics

Wildcards allow for more flexibility in generics. There are two types of wildcards:

- **Unbounded Wildcard (`?`)**: Represents any type.
- **Upper Bounded Wildcard (`? extends T`)**: Restricts the wildcard to be a subtype of `T`.
- **Lower Bounded Wildcard (`? super T`)**: Restricts the wildcard to be a supertype of `T`.
```java
// Unbounded wildcard
public static void printList(List<?> list) {
    for (Object obj : list) {
        System.out.println(obj);
    }
}

// Upper bounded wildcard
public static void printNumbers(List<? extends Number> list) {
    for (Number num : list) {
        System.out.println(num);
    }
}

// Lower bounded wildcard
public static void addNumbers(List<? super Integer> list) {
    list.add(10);
    list.add(20);
}

public static void main(String[] args) {
    List<Integer> intList = new ArrayList<>();
    List<Double> doubleList = new ArrayList<>();
    
    // Unbounded
    List<String> strList = Arrays.asList("a", "b", "c");
    printList(strList);
    
    // Upper bounded
    printNumbers(intList); // Works with Numbers or its subtypes
    
    // Lower bounded
    addNumbers(intList); // Works with Integer or its supertypes
}
```

## Generic interfaces
Interfaces can also be generic, which allows the definition of more flexible and reusable code.

```java
public interface Pair<K, V> {
    K getKey();
    V getValue();
}

public class SimplePair<K, V> implements Pair<K, V> {
    private K key;
    private V value;

    public SimplePair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    @Override
    public K getKey() {
        return key;
    }

    @Override
    public V getValue() {
        return value;
    }
}
```



---
# DSA

---
**Note :**
+ Add at end, remove at end = LIFO (Stack)
+ Add at end, remove at front = FIFO (Queue)

# Dynamic Array

+ Dynamic array in java i.e. ArrayList, Vector etc
+ ArrayList takes object. That's why we use wrapper classes like Integer, Boolean
+ It is a collection.

## ArrayList

```java
import java.util.ArrayList;

public class ArrayListUse{
	public static void main(String[] args){
		ArrayList<Integer> a1=new ArrayList<Interger>();
		
		a1.add(10); //add to the last
		a1.add(30);
		a1.add(40);
		
		a1.add(0,20); // add at specified location
		
		System.out.println(a1.size()); //arraylist size
		
		System.out.println(a1); //printing arraylist
		
		System.out.println(a1.get(0)); //get element at index 0
		
		//printing the list
		for (int i=0;i<a1.size();i++){
			System.out.println(a1.get(i));
		}
		
		a1.remove(0); //remove index from specific element
		
		a1.set(1,50); //set replaces the element
		
		//print all element using for each
		for(int element: a1){
			System.out.println(element+" ");
		}
	}
}
```



# LinkedList

## Singly Linked list
i.e. generic type singly linked list
```java
public class Node<T>{
	private T data;
	private Node<T> next;
	
	public Node(T data){
		this.data=data;
		this.next=null;
	}
	
	public T getData(){
		return this.data;
	}
}
```

```java
public class NodeUse{
	public static void main(String[] args){
		Node<Integer> n1=new Node<>(10);
		Node<Integer> n2=new Node<>(20);
		Node<Integer> n3=new Node<>(30);
		
		n1.next=n2; //n1.next is used to access the field(or instance variable) of Node object
		n2.next=n3;
		
		System.out.println(n1.getData()); //to print n1 data
		
		//to print whole list
		Node<Integer> head=n1;
		while(head!=null){
			System.out.print(head.getData()+"->");
			head=head.next;
		}
	}
}
```


**Generic type Node for Linked List Implementation**
```java
public class Node<T> {
	private T data;
	private Node<T> next;
	
	public Node(T data){
		this.data=data;
		this.next=null;
	}
	public T getData(){
		return this.data;
	}
	public Node<T> getNext(){
		return this.next;
	}
	public void setData(T data){
		this.data=data;
	}
	public void setNext(Node<T> next){
		this.next=next;
	}
}
```

**`TakeInput`** Time Complexity O(n^2)
```java
import java.util.Scanner;
public class LinkedList{
	private static Node<Integer> takeInput(){
		Node<Integer> head=null;
		Scanner s=new Scanner(System.in);
		int data=s.nextInt();
		
		while(data==-1){
			Node<Integer> newNode=new Node<>(data);
			if(head==null){
				head=newNode;
			}
			else{
				Node<Integer> temp=head;
				while(temp.getNext()!=null){
					temp=temp.getNext();
				}
				temp.setNext(newNode);
			}
			data.s.nextInt();
		}
		s.close();
		return head;
	}
	
	private static void printLL(Node<Integer> head){
		Node<Integer> temp=head;
		while(temp!=null){
			System.out.print(temp.getData()+"->");
			temp=temp.getNext();
		}
		System.out.println();
	}
	
	public static void main(String[] args){
		Node<Integer> head=takeInput();
		printLL(head);
	}
}
```

**`TakeInput`** Time Complexity : O(n)

# Linked List Operations in Java

## Linked List implementation
```java
import java.util.Scanner;

public class LinkedListBetter{
    //repetedly take input and create linked list
    public static Node<Integer> takeInput(Scanner s){
        int data=s.nextInt();
        Node<Integer> head=null,tail=null;
		
        while (data!=-1) {
            Node<Integer> newNode=new Node<Integer>(data);
            if(head==null){
                head=newNode;
                tail=newNode;
            }else{
                tail.setNext(newNode);
                tail=newNode;
            }
            data=s.nextInt();
        }
        return head;
    }
    // insert at given position
    public static Node<Integer> insert(Node<Integer> head,int pos,int data){
        Node<Integer> temp=head;
        Node<Integer> newNode=new Node<>(data);
        int count=0;
		
        if(pos==0){
            newNode.setNext(temp);
            head=newNode;
            return head;
        }else{
            while (count!=pos && temp!=null) { //here temp!=null bcz we also want to insert at last position
                temp=temp.getNext();
                count++;
            }
            if(temp!=null){ // Insert after the found node
                Node<Integer> rightLL=temp.getNext();
                temp.setNext(newNode);
                newNode.setNext(rightLL);
            }else{
                System.out.println("position out of bound");
            }
        }
        return head;
    }
	
    //length of linked list
    private static int length(Node<Integer> head){
        Node<Integer> temp=head;
        int count=0;
        while(temp!=null){
            temp=temp.getNext();
            count++;
        }
        return count;
    }
	
    // delete node from the given position in linked list
    private static Node<Integer> delete(Node<Integer> head,int pos){
        Node<Integer> temp=head,prev=null;
        int count=0;
        if(head==null){
            System.out.println("List is empty");
            return head;
        }
        else if(pos==0){
            head=temp.getNext();
            return head;
        }else{
            while (count!=pos && temp!=null) {
                prev=temp;
                temp=temp.getNext();
                count++;
            }
            if(temp!=null && temp.getNext()!=null){ 
                prev.setNext(temp.getNext());
            }else if(temp.getNext()==null){
                prev.setNext(null);
            }
            else{
                System.out.println("positon is out of bound");
            }
        }
        return head;
    }
	
    // print whole linked list
    public static void printLL(Node<Integer> head){
        Node<Integer> temp=head;
        while (temp!=null) {
            System.out.print(temp.getData()+"->");
            temp=temp.getNext();
        }
        System.out.println();
    }
	
    // print data of given position in linked list
    private static void printAt(Node<Integer> head,int pos){
        int count=0;
        System.out.println("Enter the position to print value : ");
        Node<Integer> temp=head;
        while(count!=pos && temp!=null){
            temp=temp.getNext();
            count++;
        }
        if(count==pos && temp!=null){
            System.out.println("Data at position " + pos + ": " + temp.getData());
        }else{
            System.out.println("position out of bound");
        }
    }
	
    //increase all value in linked list by 1
    private static Node<Integer> increment(Node<Integer> head){
        Node<Integer> temp=head;
        while(temp!=null){
            int data=temp.getData();
            data++;
            temp.setData(data);
            temp=temp.getNext();
        }
        return head;
    }
	
    //searching the element (Last encounter)
    private static int findNodeLast(Node<Integer> head,int element){
        Node<Integer> temp=head;
        int pos=-1,count=0;
		
        while (temp!=null) {
            count++;
            if(temp.getData()==element){
                pos=count;
            }
            temp=temp.getNext();
        }
        return pos;
    }
	
    //searching the element (first encounter)
    private static int findNodeFirst(Node<Integer> head,int element){
        Node<Integer> temp=head;
        int pos=0;
        while (temp!=null) {
            if(temp.getData()==element){
                return pos;
            }else{
                temp=temp.getNext();
                pos++;
            }
        }
        return -1;
    }
	
    //append last N nodes to first and return head
    private static Node<Integer> appendLastN(Node<Integer> head,int nth,int length){
        Node<Integer> temp=head,prevR=null,tempL=null,lasNode=null;
        int count=0;
		
        if(nth==0){
            return head;
        }else if(nth>length-1){
            System.out.println("provided position is out of bound");
            return head;
        }
		
        while (temp!=null) {
            if(count==nth){ // for target node
                tempL=temp;
            }else if(count==nth-1 && count!=0){ // for node previous to target node
                prevR=temp;
            }else if(count==length-1){ // for last node
                lasNode=temp;
            }
            count++;
            temp=temp.getNext();
        }
        
        prevR.setNext(null);
        lasNode.setNext(head);
        head=tempL;
		
        return head;
    }
	
    //remove consecutive duplicate nodes
    private static Node<Integer> removeConsecutiveDuplicate(Node<Integer> head){
        Node<Integer> temp=head;
        if(temp==null){
            return head;
        }
        while (temp!=null && temp.getNext() != null) {
            if(temp.getData()==temp.getNext().getData()){
                temp.setNext(temp.getNext().getNext());
            }else{
                temp=temp.getNext();
            }
        }
        return head;
    }
	
    //reverse LL Iteratively 
    private static Node<Integer> reverseLLIteratively(Node<Integer> head){
        Node<Integer> currNode=head,prvNode=null,fwdNode=null;
		
        while (currNode!=null) {
            fwdNode=currNode.getNext(); //1->2 3->4->5->null where 3 is current and 2 is prev ,fwd store next of 3
            currNode.setNext(prvNode);// we make 3 point to 2
            prvNode=currNode; // shift previous node to 1 step forward and make current as new previous
            currNode=fwdNode; // shift current node to 1 step forward and make forward as new current
        }
        head=prvNode; // after loop current reaches null and previous reaches to last node and last node is head of reversed LL
        return head;
    }
	
    //find middle node (returns the node before mid for even length)
    private static Node<Integer> findMid(Node<Integer> head){
        if(head==null) return null;
        Node<Integer> slow=head,fast=head.getNext();
		
        //move slow by one step and fast by two steps, to find mid element , by the end of loop slow is at mid point
        while(fast!=null && fast.getNext()!=null){
            slow=slow.getNext();
            fast=fast.getNext().getNext();
        }
		
        return slow;
    }
	
    //check palindrome
    private static boolean checkPalindrome(Node<Integer> head){
        if(head==null || head.getNext()==null){
            return true; // Empty or single node list is always a palindrome
        }
        // step-1: Find the middle element using slow and fast pointer approach
        Node<Integer> mid=findMid(head);
		
        // step-2: split the list and reverse the second half
        Node<Integer> secondHalf=mid.getNext();
        mid.setNext(null); //This is the crucial step that was missing
		
        // step 2: reverse the second half of the list starting from the mid(slow) node
        secondHalf=reverseLLIteratively(secondHalf);
		
        // step 3 : compare the first and second halves
        Node<Integer> firstHalf=head;
		
        while (secondHalf!=null) {
            if(!firstHalf.getData().equals(secondHalf.getData())){
                return false;
            }
            firstHalf=firstHalf.getNext();
            secondHalf=secondHalf.getNext();
        }
		
        return true;
    }
	
    public static void main(String[] args) {
        Scanner s=new Scanner(System.in);
        Node<Integer> head=takeInput(s); //to take input and create linked list
        printLL(head); // to print linked list
        System.out.println("Length of linked list "+length(head)); //to print length of linked list
        
        System.out.println("Enter position to print value at given position");
        int pos=s.nextInt();
        printAt(head,pos);
		
        System.out.println("Enter position to insert new data at a given position");
        int pos2=s.nextInt();
        System.out.println("Enter the data to be inserted");
        int data2=s.nextInt();
        head=insert(head,pos2,data2);
        printLL(head);
		
        System.out.println("Enter the position of node to be deleted");
        int pos3=s.nextInt();
        head=delete(head, pos3);
        printLL(head);
        
        head=increment(head); // to incease all data values by 1
        printLL(head);
		
        System.out.println("Enter the element you searching for");
        int element=s.nextInt();
        int pos4=findNodeFirst(head,element);
        printAt(head, pos4);
		
        System.out.println("Enter the Nth node");
        int nth=s.nextInt();
        head=appendLastN(head,nth,length(head));
        printLL(head);
		
        head=removeConsecutiveDuplicate(head);
        printLL(head);
		
        head=reverseLLIteratively(head); //to reverse linked list using Iterative method
        
        System.out.println(checkPalindrome(head)); //checking palindrome
		
		
        s.close();
    }
}
```

 **Note :** 

**`temp!= null`**
+ to check that current node is not` null`
+ used when iterating over each node in the list

**`temp.next!= null`** 
+ avoid trying to access **`temp.next`** in body when **`temp`** is the last node in loop

when calling **`temp.next.next`** make sure **`temp.next`** is not `null`


# Slow And Fast pointer approach or **tortoise and hare** algorithm

**Concept:**
- **Slow Pointer**: Moves **1 step** at a time.
- **Fast Pointer**: Moves **2 steps** at a time.

 **Key Applications:**

1. **Cycle Detection**:
    - If there's a cycle, **slow** and **fast** pointers will eventually meet inside the cycle.
    - If there's no cycle, **fast** will reach `null` (end of the list).

2. **Finding the Middle**:
    - For an **odd number** of nodes, **slow** ends up at the middle node.
    - For an **even number** of nodes, **slow** ends up at the **first middle node**.
    - If you need the **second middle node** (for even-length lists), you can adjust the approach slightly by moving the `slow` pointer one extra step when `fast` reaches the end.
    
**Time Complexity**: **O(n)** (Linear time)

**Space Complexity**: **O(1)** (Constant space)

i.e. used in above given code in check palindrome.

## MergeTwoSortedLL (In place sorting)

```java
public class MergeTwoSortedLL {
    
    private static Node<Integer> makeLL(int[] arr){
        Node<Integer> head=null,tail=null;
		
        for(int i=0;i<arr.length;i++){
            Node<Integer> newNode=new Node<Integer>(arr[i]);
            if(head==null){
                head=newNode;
                tail=newNode;
            }else{
                tail.setNext(newNode);
                tail=newNode;
            }
        }
        return head;
    }
	
    private static Node<Integer> mergeLL(Node<Integer> LL1,Node<Integer> LL2){
        if(LL1==null){
            return LL2;
        }else if(LL2==null){
            return LL1;
        }
        Node<Integer> head=null,tail=null,t1=LL1,t2=LL2;
        
        if(t1.getData()<=t2.getData()){
            head=t1;
            tail=t1;
            t1=t1.getNext();
        }else{
            head=t2;
            tail=t2;
            t2=t2.getNext();
        }
        
        while (t1!=null && t2!=null) {
            if(t1.getData()<=t2.getData()){
                tail.setNext(t1);
                tail=t1;
                t1=t1.getNext();
            }else{
                tail.setNext(t2);
                tail=t2;
                t2=t2.getNext();
            }
        }
		
        if(t1!=null){
            tail.setNext(t1);
        }
		
        if(t2!=null){
            tail.setNext(t2);
        }
        return head;
    }
	
    private static void print(Node<Integer> head){
        Node<Integer> temp=head;
        while (temp!=null) {
            System.out.print(temp.getData()+"->");
            temp=temp.getNext();
        }
    }
	
    public static void main(String[] args) {
        int[] arr1={1,3,5};
        int[] arr2={2,4,6};
		
        Node<Integer> LL1=makeLL(arr1);
        Node<Integer> LL2=makeLL(arr2);
		
        Node<Integer> LL3=mergeLL(LL1,LL2);
        print(LL3);
    }
}
```


# Implementing Singly Linked List with Recursive Functions

```java
import java.util.Scanner;

public class LinkedListRecursive {
    // Create Linked list using recursion
    private static Node<Integer> makeLLRecursive(Scanner s){
        int data = s.nextInt();
		
        if(data == -1){
            return null;
        }
        Node<Integer> newNode = new Node<Integer>(data);
        newNode.setNext(makeLLRecursive(s));
		
        return newNode;
    }
	
    // Insert node at position using recursion
    private static Node<Integer> insertRecursive(Node<Integer> head, int pos, int data){
        if(pos < 0){ // Prevent insertion at a negative index
            System.out.println("Error: Position can't be negative");
            return head;
        }
		
        if(pos == 0){
            Node<Integer> newNode = new Node<Integer>(data);
            newNode.setNext(head);
            return newNode;
        }
		
        if (head == null) {  // If we reached the end of the list without inserting
            System.out.println("Error: Position out of bounds.");
            return head;
        }
		
        head.setNext(insertRecursive(head.getNext(), pos-1, data));
        return head;
    }
	
    // Delete node at given position
    private static Node<Integer> deleteRecursive(Node<Integer> head, int pos){
        if(pos < 0){
            System.out.println("Error: Position can't be negative");
            return head;
        }
		
        if(head == null){ // This happens when we reach the end of the linked list
            System.out.println("Error: Position is out of bound");
            return null;
        }
		
        if(pos == 0){
            return head.getNext(); // Skip the current node (delete it)
        }
		
        // Recursive case: Move to the next node and decrease the position
        head.setNext(deleteRecursive(head.getNext(), pos-1));
        return head;
    }
	
    // Reverse linked list using recursion
    private static void reverseLLRecursive(Node<Integer> head){
        if(head == null){
            return;
        }
        reverseLLRecursive(head.getNext());
        System.out.println(head.getData());
    }
	
    // Reverse linked list using recursion (different approach)
    private static Node<Integer> reverseLLRecursive2(Node<Integer> head){
        // If the list is empty or has only one element, return the head
        if(head == null || head.getNext() == null){
            return head;
        }
		
        // Reverse the rest of the list recursively
        Node<Integer> reversedHead = reverseLLRecursive2(head.getNext());
		
        // After the recursive call, adjust the pointers
        head.getNext().setNext(head); // Make the next node point to the current node 
        head.setNext(null); // Set the current node's next to null
		
        return reversedHead; // Return the head of the reversed list
    }
	
    // Print Linked list using recursion
    private static void printRecursive(Node<Integer> head){
        if(head == null){
            return;
        }
        System.out.print(head.getData() + "->");
        printRecursive(head.getNext());
    }
	
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
		
        Node<Integer> head = makeLLRecursive(s);
		
        reverseLLRecursive(head); // Reverse linked list using recursion
		
        System.out.println("Enter position to insert new data at a given position (0 to n):");
        int pos1 = s.nextInt();
        System.out.println("Enter the data to be inserted:");
        int data1 = s.nextInt();
        head = insertRecursive(head, pos1, data1);  // Insert at the given position using recursion
		
        System.out.println("Enter the position of the node to be deleted:");
        int pos2 = s.nextInt();
        head = deleteRecursive(head, pos2); // Delete element at the given position
		
        reverseLLRecursive2(head);
		
        printRecursive(head); // Print linked list using recursion
		
        s.close();
    }
}
```


# Implement `MergeSort` on LinkedList
```java
import java.util.Scanner;

public class MergeSortLL {
    // Make linked list
    private static Node<Integer> makeLL(Scanner s) {
        Node<Integer> head = null, tail = null;
        int data = s.nextInt();
		
        while (data != -1) {
            Node<Integer> newNode = new Node<Integer>(data);
            if (head == null) {
                head = newNode;
                tail = newNode;
            } else {
                tail.setNext(newNode);
                tail = newNode;
            }
            data = s.nextInt();
        }
        return head;
    }
	
    // Print linked list
    private static void printLL(Node<Integer> head) {
        Node<Integer> temp = head;
        if (temp == null) {
            return;
        }
        System.out.print(temp.getData());
        if (temp.getNext() != null) {
            System.out.print(" -> ");
        }
        printLL(temp.getNext());
    }
	
    // Find middle node (returns the node before mid for even length)
    private static Node<Integer> findMid(Node<Integer> head) {
        if (head == null) return null;
        Node<Integer> slow = head, fast = head.getNext();
		
        while (fast != null && fast.getNext() != null) {
            slow = slow.getNext();
            fast = fast.getNext().getNext();
        }
		
        return slow;
    }
	
    // Sort and merge two linked lists
    private static Node<Integer> mergeLL(Node<Integer> LL1, Node<Integer> LL2) {
        Node<Integer> head = null, tail = null, t1 = LL1, t2 = LL2;
		
        // Handle case where one of the lists is empty
        if (t1 == null) return t2;
        if (t2 == null) return t1;
		
        // Initial comparison between the two lists
        if (t1.getData() <= t2.getData()) {
            head = t1;
            tail = t1;
            t1 = t1.getNext();
        } else {
            head = t2;
            tail = t2;
            t2 = t2.getNext();
        }
		
        // Merge the remaining list
        while (t1 != null && t2 != null) {
            if (t1.getData() <= t2.getData()) {
                tail.setNext(t1);
                tail = t1;
                t1 = t1.getNext();
            } else {
                tail.setNext(t2);
                tail = t2;
                t2 = t2.getNext();
            }
        }
		
        // Appending the remaining nodes of the non-empty list
        if (t1 != null) tail.setNext(t1);
        if (t2 != null) tail.setNext(t2);
		
        return head;
    }
	
    // Merge sort on linked list
    private static Node<Integer> mergeSortLL(Node<Integer> head) {
        if (head == null || head.getNext() == null) {
            return head;
        }
		
        Node<Integer> mid = findMid(head); // Get middle node
        Node<Integer> partHead2 = mid.getNext();
        mid.setNext(null); // Split the linked list into two parts
		
        Node<Integer> partHead1 = head;
		
        partHead1 = mergeSortLL(partHead1); // Recursively sort first part
        partHead2 = mergeSortLL(partHead2); // Recursively sort second part
        return mergeLL(partHead1, partHead2); // Merge sorted halves
    }
	
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        Node<Integer> head = makeLL(s);
		
        head = mergeSortLL(head);
		
        printLL(head);
        s.close();
    }
}
```


# `java.util.LinkedList`

```java
import java.util.LinkedList;

public class LinkedListExample {

    public static void main(String[] args) {
        
        // Create a LinkedList of integers
        LinkedList<Integer> list = new LinkedList<>();
		
        // addFirst() - Adds an item to the beginning of the list
        list.addFirst(10); // List: [10]
        list.addFirst(20); // List: [20, 10]
        System.out.println("After addFirst(): " + list); // Output: [20, 10]
		
        // addLast() - Adds an item to the end of the list
        list.addLast(30); // List: [20, 10, 30]
        System.out.println("After addLast(): " + list); // Output: [20, 10, 30]
		
        // removeFirst() - Removes an item from the beginning of the list
        list.removeFirst(); // List: [10, 30]
        System.out.println("After removeFirst(): " + list); // Output: [10, 30]
		
        // removeLast() - Removes an item from the end of the list
        list.removeLast(); // List: [10]
        System.out.println("After removeLast(): " + list); // Output: [10]
		
        // getFirst() - Retrieves the item at the beginning of the list
        int first = list.getFirst(); // first = 10
        System.out.println("First element: " + first); // Output: First element: 10
		
        // getLast() - Retrieves the item at the end of the list
        list.addLast(40); // List: [10, 40]
        int last = list.getLast(); // last = 40
        System.out.println("Last element: " + last); // Output: Last element: 40
		
        // Additional methods
		
        // add() - Adds an item to the end of the list (similar to addLast())
        list.add(50); // List: [10, 40, 50]
        System.out.println("After add(): " + list); // Output: [10, 40, 50]
		
        // peekFirst() - Retrieves the first element without removing it (returns null if empty)
        Integer peekFirst = list.peekFirst(); // peekFirst = 10
        System.out.println("Peek First: " + peekFirst); // Output: Peek First: 10
		
        // peekLast() - Retrieves the last element without removing it (returns null if empty)
        Integer peekLast = list.peekLast(); // peekLast = 50
        System.out.println("Peek Last: " + peekLast); // Output: Peek Last: 50
		
        // remove() - Removes the first occurrence of the specified element
        list.remove(Integer.valueOf(40)); // List: [10, 50]
        System.out.println("After remove(Integer): " + list); // Output: [10, 50]
		
        // clear() - Removes all elements from the list
        list.clear(); // List: []
        System.out.println("After clear(): " + list); // Output: []
    }
}
```

# [HashMap](https://www.programiz.com/java-programming/hashmap)
<u><b>Use case Scenario :</b></u>
to Store key value pair

+ unordered, means elements are not placed in the way they entered.
+ provides **constant time complexity** (O(1)) for most operations like **get()**, **put()**, and **containsKey()**.
+ **value-related operations** in a `HashMap` can take more time than **key-related operations**

```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        // Creating a HashMap
        HashMap<Integer, String> map = new HashMap<>();
		
        // put(K key, V value) - Adds key-value pairs to the map
        map.put(1, "Apple");
        map.put(2, "Banana");
        map.put(3, "Cherry");
		
        // get(Object key) - Retrieves the value for the given key
        System.out.println("Value for key 2: " + map.get(2)); // Output: Banana
		
        // containsKey(Object key) - Checks if a key exists
        System.out.println("Contains key 3? " + map.containsKey(3)); // Output: true
		
        // containsValue(Object value) - Checks if a value exists
        System.out.println("Contains value 'Apple'? " + map.containsValue("Apple")); // Output: true
		
        // remove(Object key) - Removes an entry by key
        map.remove(1);
        System.out.println("After removing key 1: " + map);
		
        // size() - Returns the number of key-value pairs
        System.out.println("Size of map: " + map.size()); // Output: 2
		
        // isEmpty() - Checks if the map is empty
        System.out.println("Is map empty? " + map.isEmpty()); // Output: false
		
        // keySet() - Returns a set of all keys
        System.out.println("Keys: " + map.keySet()); // Output: [2, 3]
		
        // values() - Returns a collection of all values
        System.out.println("Values: " + map.values()); // Output: [Banana, Cherry]
		
        // entrySet() - Returns a set of key-value pairs
        System.out.println("Entries: " + map.entrySet());
		
        // Iterating using for-each loop
        for (HashMap.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
		
        // clear() - Removes all entries
        map.clear();
        System.out.println("After clearing: " + map); // Output: {}
    }
}
```





# Stack

```java
public class StackUsingArray {
    private int data[];
    private int top;
	
    public StackUsingArray() {  // Constructor
        this.data = new int[10];
        this.top = -1;
    }
	
    public StackUsingArray(int capacity) {  // Constructor with capacity parameter
        this.data = new int[capacity];
        this.top = -1;
    }
	
    public boolean isEmpty() {
        return (top == -1);
    }
	
    public int size() {
        return (top + 1);
    }
	
    public int peek() throws StackEmptyException {
        if (size() == 0) {
            StackEmptyException e = new StackEmptyException();
            throw e;
        }
        return data[top];
    }
	
    public void push(int element) throws StackFullException {
        if (size() == data.length) {
            StackFullException e = new StackFullException();
            throw e;
        }
        this.top++;
        this.data[top] = element;
    }
	
    public int pop() throws StackEmptyException {
        if (size() == 0) {
            StackEmptyException e = new StackEmptyException();
            throw e;
        }
        int temp = data[top];
        top--;
        return temp;
    }
}
```









TODO:
Stack
Queue
