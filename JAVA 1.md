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

+ **Class** are either **public or default** but can not be private or protected.
+ Nested Class can be public, protected , default , private



Note:
+ `javac *.java` to compile all java files at once.
+ `javac Filename.java` to compile single file.
+ `java Filename.java` to execute file.
+ orcale.com for documentation.
+ programiz.com to check in-built methods.


---
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


---
# Loops

**Note :**
```java
if (condition1 && condition2) {
    // Executes only if both condition1 and condition2 are true
}
```
above code: it check condition 1 and if it is true then check condition 2 otherwise returns false without checking condition 2



---
# In built methods :
**`strip()`** vs **`trim()`**: both remove white spaces and **`\n`** but strip is new and remove all kind of whitespaces like tab .

### `System.arraycopy():` 
+ Used to copy elements from one array to another **quickly and efficiently**.
```java
System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length);
```
### Parameters:
- `src`: Source array
- `srcPos`: Starting position in the source array
- `dest`: Destination array
- `destPos`: Starting position in the destination array
- `length`: Number of elements to copy


---
# Nested and Inner class
https://www.programiz.com/java-programming/nested-inner-class

+ A class within another class.

#### 1. Member Inner Class (defined inside a class but outside any method)
Syntax
```java
class Outer{
	//...
	class Inner{ //inner class
		//...
	}
}
```
+ Outer class can only be public or default
+ Inner class can be public, protected, default ,private, abstract , final

i.e.
```java
class Outer{
	class Inner{
		void show(){
			System.out.println("Member inner class");
		}
	}
	public static void main(String[] args){
		Outer outer=new Outer();
		Outer.Inner inner=outer.new Inner();
		inner.show();
		// new Outer().new Inner().show(); //using anonymous object
	}
}
```


#### 2. Static Nested Class (declared with `static`)
Syntax
```java
class Outer{
	//...
	static class StaticNested{
		//...
	}
}
```
+ Inner class can be public, protected, default ,private, abstract , final , static
+ static nested class cannot access the member variable of the outer class.
+ static nested class does not require an instance of the outer class but you still need to create an object to call non-static methods inside it.

i.e.
```java
class Outer{
	static class StaticInner{
		void show(){
			System.out.println("Static nested class");	
		}
		staic void display(){
			System.out.println("static method inside static nested class");	
		}
	}
	
	public static void main(String[] args){
		StaticInner inner=new StaticInner();
		inner.show();
		// Outer.StaticInner.show(); we can do this without creating Outer or Inner class cause display is static
	}
}
```

#### 3. Local Inner Class (defined inside a method)
Syntax
```java
class Outer{
	//...
	void method{
		//...
		class LocalInner{
			//...
		}
	}
}
```
Inner class can be final , abstract , default

i.e.
```java
class Outer{
	void outerMethod(){
		//Local inner class defined inside method
		class LocalInner{
			void show(){
				System.out.println("Local Inner Class");
			}
		}
		LocalInner inner=new LocalInner(); // Local inner class instantiated within the method
		inner.show();
	}
	public static void main(String[] args){
		new Outer().outerMethod(); // call outerMethod where LocalInner is used
	}
}
```


#### 4. Anonymous Class


---
# Anonymous object
+ An anonymous object that is created without explicitly assigning it to a reference variable. These objects are typically used when you need to use the object only  once.
+ One time method calls.

Syntax
```java
new MyClass().myMethod();
```
In this case:
`new MyClass()` creates an anonymous object
`.myMethod()` calls a method on that object.

i.e.
```java
new Scanner(System.in).nextLine();
```

---
# Anonymous class
https://takeuforward.org/java/java-anonymous-class/
https://youtu.be/bRbt5XR5t7U
https://www.programiz.com/java-programming/anonymous-class

+ It is a special, nameless inner class that is defined and instantiated in a single expression.
+ You instantiate the anonymous class at the same time as you define it.
+ Single use
+ Is always going to be a **subclass** 
	+ by **implementation** of an interface.
	+ by extending an abstract class

Syntax
```java
new SuperClassOrInterface(){
	//Override methods
}
```
where
+ `SuperClassOrInterface` is the class or interface you're either extending or implementing.
+ You override methods of that class/interface directly in the body `{}`

#### Anonymous class extending a class 
```java
abstract class Animal{
	abstract void makeSound();
}

public class Test{
	public static void main(String[] args){
		Animal dog=new Animal(){ // Anonymous class defined here
			@Override
			void makeSound(){
				System.out.println("Woof!");
			}
		};
		dog.makeSound(); //calling the method of anonymous class
	}
}

```


#### Anonymous class implementing an interface
```java
interface Greeting{
	void sayHello();
}
public class Test{
	public static void main(String[] args){
	// Anonymous class implementing Greeting interface
		Greeting g=new Greeting(){ // Anonymous class defined here
			@Override
			public void sayHello(){
				System.out.println("Hello there!");
			}
		};
		g.sayHello(); //calling the method of anonymous class
	}
}
```

>**Note:** 
+ Anonymous classes are defined inside an expression. So, semicolon is used at the end of anonymous classes to indicate the end of the expression.

---
# Functional Interface
https://youtu.be/Gs8ZPKCFlTc
+ Functional interface is an interface that contain only one abstract method
+ Can have multiple default or static methods but only **one abstract method**.
+ Functional interface are primarily used with **lambda expressions**, **methods reference** and **constructor references** .
+ Marked optionally with `@FunctionalInterface` annotation.
	+ It generate compile time error if more than one abstract method is added.
	+ To tell compiler that the interface is intended to be functional.

Functional interface executed using concrete class implementation
```java
@FunctionalInterface
interface MyFun{
	void execute();
}

class MyFunImpl implements MyFun{ // concrete class implementing the interface
	public void execute(){
		System.out.println("Executed using concrete class implementation");
	}
}

public class Main{
	public static void main(String[] args){
		MyFun mfi=new MyFunImpl();
		mfi.execute();
	}
}

```

Functional interface executed using anonymous class
```java
@FunctionalInterface
interface MyFunctionalInterface{
	void execute(); // only one abstract method
}
class Main{
	public static void main(String[] args){
		MyFunctionalInterface mfi=new MyFunctionalInterface(){ //anonymous class
			@Override
			public void execute(){
				System.out.println("Executed using anonymous inner class");
			}
		};
		mfi.execute(); // calling method of anonymous class
	}
}
```

Functional interface executed using lambda expression
```java
@FunctionalInterface
interface MyFun{
	void execute(); //only one abstract method
}

public class Main{
	public static void main(String[] args){
		MyFun mf=()->System.out.println("Executed via lambda expression"); //lambda implementation of MyFun
		mf.execute(); //call the method
	}
}
```
#### Default inside Functional Interface
+ `default`(in context of interfaces) is a method modifier that **allows a method to have a body inside an interface**.
+ A default method is a concrete method.
+ Marked with `default` keyword
+ Inherited by class, called via object, can override

```java
@FunctionalInterface
interface MyFun{
	void execute(); // by default abstract and public
	
	default void greet(){ // default concrete method
		System.out.println("Default greeting from interface");	
	}
}

class MyFunImpl implements MyFun{
	public void execute(){
		System.out.println("Executing something...");
	}
}

public class Main{
	public static void main(String[] args){
		MyFun obj=new MyFunImpl();
		obj.execute();  //from class
		obj.greet(); // from interface default
	}
}
```


#### Static Method in an interface
+ Introduced in java 8
+ Is a method with body
+ Must be called using the interface name, not an object
+ Cannot be overridden
+ Not inherited by class

```java
interface MathOperations{
	static int add(int a,int b){ //static method
		return a+b;
	}
	
	void operate(); // functional method // public and abstract by default
}

public class Main{
	public static void main(String[] args){
		int result=MathOperations.add(5,3); //calling static method
		System.out.println("Result: "+result);
	}
}
```


#### Sealed Classes and Sealed Interfaces
Used to
- Enforce **strict hierarchy** rules
- Prevent **unexpected extensions** (security, domain logic, etc.)
- Improve **readability** and **maintainability**
- Works nicely with **switch expressions** and **pattern matching**

Syntax: With Classes
```java
public sealed class Animal permits Dog, Cat {
    // base logic
}

final class Dog extends Animal {
    // allowed ✅
}

non-sealed class Cat extends Animal {
    // allowed ✅, but opens up to further inheritance
}
```

| Keyword      | Meaning                                                          |
| ------------ | ---------------------------------------------------------------- |
| `sealed`     | Limits which classes/interfaces can extend or implement the type |
| `permits`    | Explicitly lists the allowed subtypes                            |
| `final`      | No one can extend this class any further                         |
| `non-sealed` | Removes restriction — this subtype **can be extended** further   |

Syntax: With Interfaces too
```java
public sealed interface Shape permits Circle, Rectangle {}

final class Circle implements Shape {
    // ✅ allowed
}

non-sealed class Rectangle implements Shape {
    // ✅ allowed and can be further extended
}
```


>NOTE:
 All permitted classes must be: 
+ In same module (or same package if not using modules) 
+ Either `final`,`sealed` or `non-sealed` (failing to do so result in compiler error)
+ Explicitly listed in `permits` clause


---
# Lambda Expression
+ Lambda expression is used with functional interfaces.
+ Introduced in java 8
+ A lambda expression is a short block of code which takes in parameters and returns a value

Syntax
`(parameters) -> expression`

or
```java
(parameters) -> {
    // code block
    return value;
}
```

Use Cases
+ Iterating over collections (`forEach`)
+ Filtering, mapping, and reducing with streams
+ Passing behaviour as data

#### Lambda Expression with Zero Parameters

i.e.
```java
@FunctionalInterface
interface Task{
	void execute(); // public and abstract by default
}

public class Main{
	public static void main(String[] args){
		Task sayHello=()->System.out.println("Hello"); // lambda expression
		sayHello.execute(); //Output: Hello
	}
}
```

i.e. if you want to return something
```java
@FunctionalInterface
interface Supplier{
	String get();
}

public class Main{
	public static void main(String[] args){
		Supplier greeting=()->"Hello there";
		System.out.println(greeting.get()); //Output: Hello there
	}
}
```


#### Lambda Expression with One Parameter
```java
@FunctionalInterface
interface Printer {
    void print(String message);
}
public class Main{
	public static void main(String[] args){
		Printer p=message->System.out.println("Printing: "+message);
		p.print("Hello, there"); //Output: Printing: Hello, there
	}
}
```
If there's **only one parameter**, you **can omit parentheses** around it: `message -> ...`

#### Lambda Expression in `ArrayList`'s `forEach()` 
i.e. to print every item in the list and even numbers
```java
import java.util.ArrayList;

public class Main{
	public static void main(String[] args){
		ArrayList<Integer> numbers=new ArrayList<>();
		numbers.add(1);
		numbers.add(2);
		numbers.add(3);
		numbers.add(4);
		numbers.forEach(n->System.out.println("Number: "+n)); //use lambda to print each number
		numbers.forEach(n->{ //use lambda expression to print even numbers
			if(n%2==0){
				System.out.println("Even: "+n);
			}
		});
	}
}
```

#### Lambda with functional interface
```java
@FunctionalInterface
interface MyFun{
	int operation(int a,int b); //with return type and parameter
}

public class Main{
	public static void main(String[] args){
		MyFun add=(a,b)->a+b; 
		MyFun mul=(a,b)->a*b;
		
		System.out.println("Sum: "+add.operation(5,3));
		System.out.println("Product: "+mul.operation(5,2));
	}
}
```
Java **infers types** from the context, so `int` can often be skipped: `(a,b)`


# Lambda on primitive and object
- Primitive arrays need to be converted to `Stream` for lambda usage.
- Stream gives you access to `forEach`, `map`, `filter`, etc.
##### **1. For Primitive Arrays (like `int[]`, `double[]`)**
Use: `Arrays.stream(...)`  
Because: Primitive arrays can't be boxed into a `List` easily, and Java has special streams for them (`IntStream`, `DoubleStream`, etc.)

```java
import java.util.Arrays;

public class PrimitiveArrayExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3, 4, 5};
        // Using lambda with primitive array
        Arrays.stream(numbers)
              .forEach(n -> System.out.println("Number: " + n));
    }
}
```
`Arrays.stream(int[])` returns an `IntStream` that supports lambda operations.

##### **2. For Non-Primitive Arrays (like `String[]`, `Integer[]`, etc.)**
Use: `Arrays.asList(...)` or `Stream.of(...)`  
Because: These are object arrays, so they can be boxed into a collection or stream easily.

i.e. with `Arrays.asList()`
```java
import java.util.Arrays;

public class ObjectArrayExample1 {
    public static void main(String[] args) {
        String[] words = {"Java", "Lambda", "Cool"};
        // Using lambda with Arrays.asList()
        Arrays.asList(words)
              .forEach(w -> System.out.println("Word: " + w));
    }
}
```

i.e. with `Stream.of()`
```java
import java.util.stream.Stream;

public class ObjectArrayExample2 {
    public static void main(String[] args) {
        String[] words = {"Java", "Lambda", "Cool"};
        // Using lambda with Stream.of()
        Stream.of(words)
              .forEach(w -> System.out.println("Word: " + w));
    }
}
```




TODO:
lambda expression for interface chatgpt example
method reference


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

Use a `public static` variable in a class to define a global variable accessible across multiple classes.
i.e.
```java
public class Main {
    public static int globalCount = 0; // global variable
}
```

+ we make main class as static so that JVM can call it with class name without making its instance.
+ `this` cannot be used in a static method, because it refers to the current instance and static methods do not belong to a specific instance.
+ `super` can be used inside static methods, but only to access static members(fields and methods) of the parent class.
+ constructor can't be static

+ static method can not use non static function and variable.
```java
class MyClass {
    int instanceVariable = 10;
    // Non-static method
    public void nonStaticMethod() {
        System.out.println("This is a non-static method. Instance variable: " + instanceVariable);
    }
    // Static method
    public static void staticMethod() {
        // Cannot directly call non-static method from static context
        // nonStaticMethod(); // This would result in a compilation error
        
        // Correct way: Create an instance of the class
        MyClass obj = new MyClass();
        obj.nonStaticMethod(); // Now we can call the non-static method
    }
    public static void main(String[] args) {
        // Calling the static method
        staticMethod();
    }
}
```

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

i.e. main class is static so we made `ArrayList` global but also static so we use it inside main but we can also define inside main without making it static.
```java
import java.util.ArrayList;

// Main class
public class ArrayListExample {
    // 🔹 Static (global) ArrayList - shared across all classes
    static ArrayList<String> list = new ArrayList<>();
	
    public static void main(String[] args) {
        // 🔹 Accessing static ArrayList directly inside static main()
        list.add("Hello from main()");
        list.add("Another from main");
		
        // 🔹 Print current state of list
        System.out.println("Inside main: " + list);
		
        // 🔹 Creating object of another class
        OtherClass obj = new OtherClass();
		
        // 🔹 Calling non-static method that modifies the same static list (static class can access non static method and variable)
        obj.addToList("Hello from OtherClass");
		
        // 🔹 Print list again after modification from other class
        System.out.println("After OtherClass: " + list);
    }
}

// 🔹 Another class to show access from non-static context
class OtherClass {
    public void addToList(String item) {
        // 🔹 Accessing static ArrayList from another class using class name because ArrayList is static
        ArrayListExample.list.add(item);
    }
}
```


**static block**
+ A **static block** in Java is a block of code that runs **once when the class is loaded**, even **before the `main()` method** or any object is created.

```java
public class Example {
    static int num; 
	
    static {  //static block
        num = 10;
        System.out.println("Static block executed.");
    }
	
    public static void main(String[] args) {
        System.out.println("Main method: num = " + num);
    }
}
```


---
## super keyword

+ **Calling a Parent Class Method and Property:** If the child class has a method with the same name as the one in the parent class, super allows you to call the parent class method.

+ **Calling the Parent Class Constructor:** super() can be used to call the constructor of the parent class when creating an object of the child class.
+ i.e. **`super()`**

---
# Constructor

**Constructor Format** :  `<Access Modifier> <Constructor Name> (parameters)`
+ used to initialize objects
+ constructor name same as class name
+ no return type
+ Automatically called at the time of object creation to initialize the object.
+ Constructor overloading is allowed.
+ When we do not explicitly define constructor for a class, then java creates a default constructor for the class

TODO: constructor overloading


---
# Encapsulation

+ All properties and methods related to that class at one place .
+ hiding of data using getter and setter

TODO: encapsulation example

---
# Inheritance

+ Used for acquiring properties of other class.
+ Uses `extend` keyword.
+ The class being inherited from is called the **superclass**, and the class that inherits is called the **subclass**.
+ You can not extend more than one class but can implement multiple interface in a class.

i.e.
```java
class Superclass {
    // Superclass fields and methods
}

class Subclass extends Superclass {
    // Subclass can have its own fields and methods
    // It can also override methods from the superclass
}
```


When child class constructor is called to create object ,it also calls the parent class constructor which creates parent object too.
i.e.
```java
class A {
    A() {
        System.out.println("Parent class constructor called.");
    }
}

class B extends A {
    B() {
        // Implicitly calls A() constructor first, before executing B's constructor
        System.out.println("Child class constructor called.");
    }
}

public class Main {
    public static void main(String[] args) {
        B obj = new B();  // Creating object of child class B
        //output :
        // Parent class constructor called.
		// Child class constructor called.
    }
}

```


i.e.
```java
// Superclass (Parent Class)
class Animal {
    void speak() {
        System.out.println("Animal makes a sound.");
    }
}

// Subclass (Child Class)
class Dog extends Animal {
    // Inherits the speak() method from Animal
}

public class Main {
    public static void main(String[] args) {
        Dog myDog = new Dog();
        myDog.speak();  // Output: Animal makes a sound.
    }
}
```



**Scenario 01:** Accessing private member of superclass using getter/setter
+ Suppose a vehicle has private property and it is accessible using getter and setter. Now the car is extending vehicle . so the car also have that private property but can't directly access it. but can access using getter and setter.

```java
// Superclass
class Vehicle {
    private int speed;

    public int getSpeed() {
        return speed;
    }

    public void setSpeed(int speed) {
        this.speed = speed;
    }
}

// Subclass
class Car extends Vehicle {
    public void showSpeed() {
        // Can't access `speed` directly here because it's private in Vehicle
        System.out.println("Speed from getter: " + this.getSpeed());
    }

    public void updateSpeed(int newSpeed) {
        // Setting the private property via setter
        this.setSpeed(newSpeed);
    }
}

// Main Class to Run
public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.updateSpeed(80);     // Setting speed using setter
        myCar.showSpeed();         // Getting speed using getter
    }
}
```

**for above :**
- In Java, when `Car` extends `Vehicle`, it inherits all **public/protected methods** of `Vehicle`.
- Even though `speed` is `private`, `Car` can access it using the **inherited** `getSpeed()` and `setSpeed()` methods.
- You can use `this.getSpeed()` because `Car` **inherits** the method — it’s treated like `Car`’s own.
- Or use `super.getSpeed()` if you want to **explicitly refer to the superclass** version.
- No need to create a `Vehicle` object — `Car` _is-a_ `Vehicle`.


**Scenario 02:** Accessing protected member of superclass

```java
class A {
    protected int x = 10;  // Protected data member

    protected void display() {  // Protected method
        System.out.println("Display from class A");
    }
}

class B extends A {
    void callDisplay() {
        System.out.println("Value of x: " + x);  // Accessing protected data member
        display();  // Calling the inherited protected method
    }
}

public class Main {
    public static void main(String[] args) {
        B obj = new B();
        obj.callDisplay();  // Output: Value of x: 10
                            // Output: Display from class A
    }
}
```

**for above :**
+ `B` inherit protected data member `x` and method `display()` from `A` and it treat it as `B`'s own property and method.
+ The `x` and `display()` are accessible inside `B` and are treated as if they are part of `B`.


---
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

- Cannot create an **object** of an **abstract class** directly.
- Acts as an **incomplete blueprint** — may have concrete methods, but missing abstract ones.
- You **must extend** it and **implement all abstract methods** in a concrete subclass to create objects.


A class that inherits from an abstract class must provide implementations for the abstract methods, unless it is also abstract. (child class)
i.e.
```java 
abstract class Animal {
    abstract void sound(); // Abstract method (no implementation only declared)
    
    void sleep() { // Concrete method
        System.out.println("This animal sleeps.");
    }
}

class Dog extends Animal {
    void sound() { // Providing implementation for the abstract method
        System.out.println("Woof!");
    }
}

// Abstract Cat class that doesn't implement sound() is declared abstract
abstract class Cat extends Animal {
    // Concrete method specific to cats
    void scratch() {
        System.out.println("The cat scratches the furniture.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.sound();  // Woof!
        myDog.sleep();  // This animal sleeps.
	    
        // Can't create an instance of Cat since it's abstract
        // Cat myCat = new Cat(); // Compile-time error
    }
}
```


---
# Interface

+ Use interface keyword (parent class)
+ Its a pure abstract (only abstract methods)
+ All methods are abstract and public (by default).
+ Can also have default or static methods.
+ All properties (field) are either public , static or final.
+ In Java, interfaces cannot **`implement`** other interfaces
+ Multiple inheritance
	1. A **class** can implement more than one **interface**.
		When you **`implement`** an interface, you're creating a class that must provide implementations for the methods defined in the interface(s).
	2. An **interface** can extend more than one **interface**.
		When you **`extend`** an interface, you're creating a new interface that inherits the methods of the interfaces you're extending.
+ To inherit interface class we use implement keyword.

mostly not contain data member but if then it is of type final and static. (to store constant)
i.e.
```java
public interface VehicleInterface{
	public final static double PI=3.14; //data member
	public int getMaxSpeed(); // method
	public void print();  //method
}
```

You cannot create an object of an interface directly because it is abstract and incomplete. However, you can use the interface in the following ways:
By implementing it in a class and creating an object of that class.
i.e.
```java
interface A {
    void show();
}

class B implements A {
    public void show() {
        System.out.println("Hello");
    }
}

public class Main {
    public static void main(String[] args) {
        A obj = new B(); // ✅ using interface reference
        obj.show();      // Output: Hello
    }
}
```


If a class implements an interface, it must either:
- Use `abstract` keyword (and skip method implementation),
- Or implement **all methods** from the interface.
i.e.
```java
interface Animal {
    void sound();
    void sleep();
}

// Abstract class: partially implements interface, so must be abstract
abstract class Dog implements Animal {
    public void sound() {
        System.out.println("Dog barks: Woof!");
    }
    // sleep() is not implemented
}

// Concrete class: fully implements all interface methods
class Cat implements Animal {
    public void sound() {
        System.out.println("Cat meows: Meow~");
    }
	
    public void sleep() {
        System.out.println("Cat sleeps peacefully.");
    }
}

public class Main {
    public static void main(String[] args) {
        // You can't create an object of abstract class directly
        // Dog d = new Dog();              // ❌ Error
        // Animal b = new Dog();           // ❌ Error
		
        // You can create object of concrete class that implements interface
        Animal a = new Cat();              // ✅ Valid
        a.sound();                         // Output: Cat meows: Meow~
        a.sleep();                         // Output: Cat sleeps peacefully.
    }
}
```


---


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


---
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

---
# Exception Handling
Exception in Java is an error condition that occurs when something wrong happens during the program execution.
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


i.e.
```java
public class MyClass {
    public void someMethod() throws Exception {
        boolean someCondition = true; // Just for demo
        if (someCondition) {
            throw new Exception("Something went wrong!");
        }
    }
	
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        try {
            obj.someMethod();
        } catch (Exception e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }
}
```

i.e. : Check Queue implementation using Linked list

**NOTE :** 
+ We are not allowed to catch generalized exception before specific exception.


### Exception hierarchy
```
Throwable
├── Error (Unchecked)
│   ├── VirtualMachineError
│   │   ├── OutOfMemoryError
│   │   └── StackOverflowError
│   ├── AssertionError
│   └── LinkageError
│       ├── NoClassDefFoundError
│       └── UnsatisfiedLinkError
│
└── Exception (Checked)
    ├── IOException
    │   ├── FileNotFoundException
    │   ├── EOFException
    │   └── SocketException
    │       └── ConnectException
    ├── SQLException
    ├── InterruptedException
    ├── ParseException
    ├── ClassNotFoundException
    ├── InvocationTargetException
    └── RuntimeException (Unchecked)
        ├── ArithmeticException
        ├── NullPointerException
        ├── IllegalArgumentException
        │   └── NumberFormatException
        ├── IndexOutOfBoundsException
        │   ├── ArrayIndexOutOfBoundsException
        │   └── StringIndexOutOfBoundsException
        ├── ClassCastException
        ├── SecurityException
        ├── UnsupportedOperationException
        ├── IllegalStateException
        ├── ConcurrentModificationException
        ├── NoSuchElementException
        └── MissingResourceException
```



https://www.geeksforgeeks.org/exceptions-in-java/

TODO : 
+ multiple exception from chatgpt example
+ multiple catch
+ how jvm handle error and exception

---
# Multithreading

+ Once a thread object is created, you invoke the `start()` method to begin its execution. The `start()` method internally calls the `run()` method.
+ **run( )**: The entry point for the thread

**Creating a Thread by Extending the `Thread` Class**
```java
public class BasicThread extends Thread {
	@Override
    public void run() {
        System.out.println("Thread is running");
    }
	
    public static void main(String[] args) {
        BasicThread t1 = new BasicThread(); // create thread instance
        t1.start(); // start thread
    }
}
```


**Creating a Thread by Implementing the `Runnable` Interface**
```java
public class MyTask implements Runnable {
    @Override
    public void run() {
        System.out.println("Task is running in a separate thread");
    }
	
    public static void main(String[] args) {
        MyTask task = new MyTask();
        Thread t1 = new Thread(task);  // Passing Runnable to Thread
        t1.start();  // Start the thread to execute the task
    }
}
```

**MIX Of BOTH**
```java
class Thread1 extends Thread {
	public void run() {
		for (int i = 1; i <= 10; i++) {
			System.out.println("i=" + i);
		}
	}
}

class Thread2 implements Runnable {
	public void run() {
		for (int k = 1; k <= 10; k++) {
			System.out.println("k=" + k);
		}
	}
}

public class CreatingThread {
	
	public static void main(String[] args) {
		Thread1 t1 = new Thread1(); // extends Thread
		Thread t2 = new Thread(new Thread2()); // Thread2 implements Runnable
		
		System.out.println("Starting 1st");
		t1.start();
		
		System.out.println("Starting 2nd");
		t2.start();
		
		System.out.println("End of main");
	}
}
```

## Thread Lifecycle
#### **Key Concepts to Learn:**

- **Thread States:**
    - **New:** When a thread is created but not yet started.
    - **Runnable:** After calling `start()`, the thread enters this state, ready for CPU allocation.
    - **Blocked:** When a thread is waiting for a resource that another thread is holding.
    - **Waiting:** When a thread is waiting indefinitely for some condition or event.
    - **Timed Waiting:** When a thread is waiting for a specific time period (e.g., `Thread.sleep()`).
    - **Terminated:** When a thread finishes its execution.

**Code to understand Thread States**
```java
class MyThread extends Thread{
	
	public void run(){
		System.out.println("Thread is running");
		try {
			Thread.sleep(1000);
		} catch (InterruptedException e) {
			System.out.println(e.getMessage());
		}
	}
}

public class ThreadStatesExample {
	public static void main(String[] args) throws InterruptedException {
		MyThread t1=new MyThread();
		System.out.println(t1.getState());
		t1.start();
		System.out.println(t1.getState());
		Thread.sleep(100);
		System.out.println(t1.getState());
		t1.join();
		System.out.println(t1.getState());
    }
}
```


- **Thread Life Cycle Methods:**
    - `void start()`: method causes the JVM to initiate a new **native thread** (in the operating system's thread pool) to begin executing the `run()` method. 
    - `join()`: Waits for a thread to finish before continuing. When one thread calls the `join()` method of another thread, it pauses the execution of the current thread until the thread being joined has completed its execution.

| **Method**                  | **Description**                                                                                                                                                                            | **Life Cycle State Affected**   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------- |
| `start()`                   | Starts the thread; moves from **New** to **Runnable**                                                                                                                                      | New → Runnable                  |
| `run()`                     | Code executed by the thread (usually overridden)                                                                                                                                           | Runnable → Running (internally) |
| `sleep(long millis)`        | Pauses the thread for a specified time                                                                                                                                                     | Running → Timed Waiting         |
| `join()`                    | Waits for another thread to die                                                                                                                                                            | Running → Waiting               |
| `join(long millis)`         | Waits for another thread to die, with timeout                                                                                                                                              | Running → Timed Waiting         |
| `yield()`                   | Hints the scheduler to pause and give other threads a chance to run.<br>It **does not change the state**, but may result in the thread being moved **back to Runnable** so others can run. | Still Runnable                  |
| `wait()` (from `Object`)    | Makes the thread wait until notified                                                                                                                                                       | Running → Waiting               |
| `wait(long timeout)`        | Waits for a limited time                                                                                                                                                                   | Running → Timed Waiting         |
| `notify()` / `notifyAll()`  | Wakes up threads waiting on the object's monitor                                                                                                                                           | Waiting → Runnable              |
| `interrupt()`               | Interrupts a thread if it's in a blocking state                                                                                                                                            | Affects Waiting/Sleep/Join      |
| `isAlive()`                 | Checks if the thread is alive (not yet dead)                                                                                                                                               | Any state                       |
| `isInterrupted()`           | Checks if the thread has been interrupted                                                                                                                                                  | Any state                       |
| `setPriority(int priority)` | Sets thread’s priority (1 to 10)                                                                                                                                                           | Runnable (affects scheduling)   |
| `getPriority()`             | Gets thread’s priority                                                                                                                                                                     | Any state                       |
| `setName(String)`           | Assigns a name to the thread                                                                                                                                                               | Any state                       |
| `getName()`                 | Returns the thread’s name                                                                                                                                                                  | Any state                       |
| `setDaemon(boolean)`        | Marks thread as a daemon thread                                                                                                                                                            | Must be called before `start()` |
| `isDaemon()`                | Checks if the thread is a daemon                                                                                                                                                           | Any state                       |
| `currentThread()`           | Static method to get a reference to the currently running thread                                                                                                                           | Running                         |

>NOTE:
>`wait()`, `notify()`, and `notifyAll()` are methods from `java.lang.Object`, not `Thread`, but they are critical for thread synchronization and lifecycle transitions.



```
                 +------------------+
                 |      New         |
                 |------------------|
                 | Thread created   |
                 +------------------+
                         |
                         v
                 +------------------+
                 |    Runnable      |
                 |------------------|
                 | start() called   |
                 +------------------+
                         |
                         v
                 +------------------+
                 |     Running      |
                 |------------------|
                 | CPU time allocated|
                 +------------------+
                         |
       +-----------------+-----------------+
       |                 |                 |
       v                 v                 v
+---------------+ +---------------+ +---------------+
|   Waiting     | |  Timed Waiting| |    Blocked    |
|---------------| |---------------| |---------------|
| wait()        | | sleep(time)   | | I/O operation |
| join()        | | wait(time)    | | synchronized  |
| park()        | | join(time)    | | block()       |
+---------------+ +---------------+ +---------------+
       |                 |                 |
       +-----------------+-----------------+
                         |
                         v
                 +------------------+
                 |      Dead        |
                 |------------------|
                 | run() completes  |
                 | stop() called    |
                 +------------------+
```


## Thread Synchronization

When multiple threads access shared resources, data inconsistency may occur. **Synchronization** is the mechanism used to control the access of multiple threads to shared resources.

#### **Key Concepts to Learn:**

- **What is Synchronization?**
    - Synchronization ensures that only one thread can access a **critical section** of code at a time, preventing race conditions.

- **`synchronized` Keyword:**
    - You can use the `synchronized` keyword to lock a method or block of code so that only one thread can execute it at a time.
```java
public synchronized void increment() {
    counter++;
}
```

- **Deadlocks:**
    - A deadlock occurs when two or more threads are blocked forever, waiting for each other. It’s crucial to understand how to avoid deadlocks.

- **Reentrant Locks:**
    - Instead of using the `synchronized` keyword, you can use explicit locks such as `ReentrantLock` for more advanced locking mechanisms.


TODO:
### **6. Thread Pooling and Executor Framework**

### **7. Fork/Join Framework (Advanced)**
### **8. Handling Exceptions in Threads**

### **Recommended Study Plan**

1. **Week 1:** Basics of Threads (Creation, Lifecycle, `Runnable`, `Thread` class)
    
2. **Week 2:** Thread Synchronization (Race Conditions, `synchronized`, Deadlocks)
    
3. **Week 3:** Thread Communication (`wait()`, `notify()`, `notifyAll()`, Producer-Consumer Problem)
    
4. **Week 4:** Thread Pooling and Executor Framework
    
5. **Week 5:** Fork/Join Framework (Advanced Parallelism)
    
6. **Week 6:** Exception Handling, Best Practices, and Common Pitfalls
    
7. **Week 7-8:** Hands-on projects using multiple conc

---
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

- **Unbounded Wildcard (`?`)**: Represents any type. Used when you don't care about the type and want to accept any object.
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




# [Collection Framework](https://youtu.be/rzA7UJ-hQn4)



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



---
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

# Linked List Operations in Java

## Linked List implementation

**`TakeInput`** Time Complexity : O(n)
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


---
# Stack

# Stack Implementation using Array

`StackUsingArray.java`
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
	
    public void push(int element){
        if (size() == data.length) {
            doubleCapacity();
        }
        this.top++;
        this.data[top] = element;
    }
    
    private void doubleCapacity(){
		int[] temp=data;
		data=new int[temp.length*2];
		
		for(int i=0;i<temp.length;i++){
			data[i]=temp[i];
		}
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

`StackFullException.java`
```java
public class StackFullException extends Exception {
}
```

`StackEmptyException.java`
```java
public class StackEmptyException extends Exception {

}
```

`StackUse.java`
```java
public class StackUse {
    public static void main(String[] args) throws StackFullException {
        StackUsingArray s1 = new StackUsingArray();
        
        // Push elements into the stack
        for (int i = 1; i <= 5; i++) {
            s1.push(i);
        }
		
        // Pop elements from the stack and print them
        while (!s1.isEmpty()) {
            try {
                System.out.println(s1.pop());
            } catch (Exception e) {
                // Handle any exceptions (though unlikely in this example)
            }
        }
    }
}
```


# Stack Implementation using Linked List

`Node.java`
```java
public class Node<T> {
    private T data;
    private Node<T> next;
	
    public Node(T data){
        this.data = data;
        this.next = null;
    }
	
    public void setData(T data){
        this.data = data;
    }
	
    public void setNext(Node<T> next){
        this.next = next;
    }
	
    public T getData(){
        return this.data;
    }
	
    public Node<T> getNext(){
        return this.next;
    }
}
```

`StackUsingLL.java`
```java
public class StackUsingLL<T> {
    private Node<T> head;
    private int size;
	
    public StackUsingLL(){
        this.head = null;
        size = 0;
    }
	
    public int size(){
        return size;
    }
	
    public T top() throws StackEmptyException {
        if(size == 0){
            throw new StackEmptyException();
        }
        return head.getData();
    }
	
    public boolean isEmpty(){
        // return (size == 0 ? true : false );
        return (size == 0);
    }
	
    public void push(T data){
        Node<T> newNode = new Node<>(data);
        newNode.setNext(head); // make the new node point to the old head
        head = newNode;  // update head to the new node
        size++;
    }
	
    public T pop() throws StackEmptyException {
        if(size == 0){
            throw new StackEmptyException();
        }
        T data = head.getData();
        head = head.getNext();
        size--;
        return data;
    }
}
```

`StackEmptyException.java`
```java
public class StackEmptyException extends Exception {

}
```

`StackUsingLLUse.java`
```java
public class StackUsingLLUse {
    public static void main(String[] args) {
        StackUsingLL<Integer> s1 = new StackUsingLL<>();
        // push data into stack
        for (int i = 0; i < 3; i++) {
            s1.push(i + 1);
        }
		
        // pop data from stack
        while (!s1.isEmpty()) {
            try {
                System.out.println(s1.pop());
            } catch (Exception e) {
                // TODO: handle exception
            }
        }
    }
}
```


# [`java.util.Stack`](https://www.programiz.com/java-programming/stack)

```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        Stack<Integer> s1 = new Stack<>();
		
        // Push elements onto the stack
        s1.push(10);  // Adds 10 to the stack
        s1.push(20);  // Adds 20 to the stack
        s1.push(30);  // Adds 30 to the stack
        System.out.println("Stack after pushes: " + s1);  // Prints the stack
		
        // Peek at the top element (without removing it)
        System.out.println("Top element: " + s1.peek());  // Prints the top element (30)
		
        // Pop an element from the stack (removes and returns it)
        int poppedElement = s1.pop();
        System.out.println("Popped element: " + poppedElement);  // Pops and prints 30
        System.out.println("Stack after pop: " + s1);  // Prints the updated stack
		
        // Check if the stack is empty
        System.out.println("Is stack empty? " + s1.isEmpty());  // Prints false
		
        // Check the size of the stack
        System.out.println("Size of stack: " + s1.size());  // Prints the size (2 in this case)
		
        // Search for an element in the stack (returns the 1-based index)
        int position = s1.search(20);  
        System.out.println("Position of 20 in stack: " + position);  // Prints the position (1-based)
		
        // Try popping all elements
        while (!s1.isEmpty()) {
            System.out.println("Popped element: " + s1.pop());
        }
        System.out.println("Stack after popping all elements: " + s1);  // Should print an empty stack
    }
}
```



# Queue 

# Queue Implementation using Array

```java
public class QueueUsingArray {
    private int[] data;
    private int rear;
    private int front;
    private int size;
	
    public QueueUsingArray() {
        this.data = new int[10];
        this.rear = -1;
        this.front = -1;
        this.size = 0;
        // Note: default capacity is set to 10
    }
	
    public QueueUsingArray(int capacity) {
        this.data = new int[capacity];
        this.rear = -1;
        this.front = -1;
        this.size = 0;
        // Note: allows creating queue with custom initial capacity
    }
	
    public boolean isEmpty() {
        return (size == 0);
        // Note: simple check using size field for constant time operation
    }
	
    public int size() {
        return size;
        // Note: size tracks the current number of elements in the queue
    }
	
    public int front() throws QueueEmptyException {
        if (front == -1) {
            throw new QueueEmptyException();
            // Note: -1 front indicates the queue is empty
        }
        return data[front];
        // Note: returns element at front index without removing it
    }
	
    public void enqueue(int data) throws QueueFullException {
        if (size == this.data.length) {
            // throw new QueueFullException();
            doubleCapacity(); // dynamically increases capacity instead of throwing an error
        }
        if (size == 0) { // first element added, front must be initialized
            front = 0;
        }
		
        size++;
        // rear = (rear + 1) % this.data.length; instead of below rear++ and if we can write this
        rear++;
        if (this.rear == this.data.length) { // handles circular indexing manually
            rear = 0;
        }
        
        this.data[rear] = data; // assigns new data at the calculated rear position
    }
	
    private void doubleCapacity() {
        int[] temp = data;
        data = new int[temp.length * 2];
        int index = 0;
		
        // this copy data from front to last
        for (int i = front; i < temp.length; i++) {
            data[index] = temp[i];
            index++;
        }
		
        // this copy data from start to front-1
        for (int i = 0; i <= front - 1; i++) {
            data[index] = temp[i];
            index++;
        }
		
        front = 0;
        rear = temp.length;
        // Note: resets front to 0 and rear to the last valid index in old array
        // Now queue is linear in memory again
    }
	
    public int dequeue() throws QueueEmptyException {
        if (front == -1) {  // underflow check - queue is empty
            throw new QueueEmptyException();
        }
		
        int temp = data[front];
		
        // front = (front + 1) % this.data.length; instead of below front++ and if we can write this
        front++;
        if (this.front == this.data.length) { // handles circular increment of front
            front = 0;
        }
		
        size--;
		
        if (size == 0) { // reset queue if it becomes empty
            front = -1;
            rear = -1;
        }
		
        return temp; // returns the removed element
    }
}
```

```java
public class QueueFullException extends Exception{
	
	public QueueFullException(){
		super("Queue is full");
	}
}
```

```java
public class QueueEmptyException extends Exception{
	
	public QueueEmptyException(){
		super("Queue is empty");
	}
}
```

```java
public class QueueUse {
    public static void main(String[] args) {
        QueueUsingArray q1 = new QueueUsingArray();
		
        // Enqueue elements
        for (int i = 1; i <= 10; i++) {
            try {
                q1.enqueue(i);
            } catch (QueueFullException e) {
                System.out.println("Failed to enqueue " + i + ": " + e.getMessage());
            } catch (Exception e) {
                System.out.println("Unexpected error during enqueue: " + e.getMessage());
            }
        }
		
        // Dequeue elements
        while (!q1.isEmpty()) {
            try {
                System.out.println(q1.dequeue());
            } catch (QueueEmptyException e) {
                System.out.println("Failed to dequeue: " + e.getMessage());
            } catch (Exception e) {
                System.out.println("Unexpected error during dequeue: " + e.getMessage());
            }
        }
    }
}
```


# Queue Implementation using Linked List

`Node.java`
```java
public class Node<T> {
    private T data;
    private Node<T> next;
	
    public Node(T data){
        this.data = data;
        this.next = null;
    }
	
    public void setData(T data){
        this.data = data;
    }
	
    public void setNext(Node<T> next){
        this.next = next;
    }
	
    public T getData(){
        return this.data;
    }
	
    public Node<T> getNext(){
        return this.next;
    }
}
```


```java
public class QueueUsingLL<T> {
    private Node<T> front;
    private Node<T> rear;
    private int size;
	
    public QueueUsingLL() {
        this.front = null;
        this.rear = null;
        this.size = 0;
    }
	
    public int size() {
        return this.size;
    }
	
    public boolean isEmpty() {
        return (size == 0);
    }
	
    public T front() throws Exception {
        if (size == 0) { // when list is empty
            throw new Exception("Queue is empty");
        }
        return front.getData();
    }
	
    public void enqueue(T data) {
        Node<T> newNode = new Node<T>(data);
        if (this.rear == null) {
            front = newNode;
            rear = newNode;
        } else {
            rear.setNext(newNode);
            rear = newNode;
        }
        size++;
    }
	
    public T dequeue() throws Exception {
        if (size == 0) { // when list is empty
            throw new Exception("Queue is empty");
        }
        T temp = front.getData();
        front = front.getNext();
        if (size == 1) { // when removing last element
            front = null;
            rear = null;
        }
        size--;
		
        return temp;
    }
}
```


```java
public class QueueUse {
    public static void main(String[] args) {
        QueueUsingLL<Integer> q1 = new QueueUsingLL<>();
        
        for (int i = 1; i <= 10; i++) {
            q1.enqueue(i);
        }
		
        while (!q1.isEmpty()) {
            try {
                System.out.println(q1.dequeue());
            } catch (Exception e) {
                // TODO: handle exception
                System.out.println(e.getMessage());
            }
        }
    }
}
```



# [`java.util.queue`](https://www.programiz.com/java-programming/queue)

Since the Queue is an interface, we cannot provide the direct implementation of it.

In order to use the functionalities of Queue, we need to use classes that implement it:
+ `ArrayDeque`
+ `LinkedList`
+ `PriorityQueue`

```java
import java.util.*;

public class QueueExample {
    public static void main(String[] args) {
        Queue<String> q = new LinkedList<>();
		
        // 1️⃣ add() – Adds element, throws exception if fails
        q.add("A");
        q.add("B");
		
        // 2️⃣ offer() – Adds element, returns false if fails (better for capacity-restricted queues)
        q.offer("C");
		
        // Queue: [A, B, C]
		
        // 3️⃣ peek() – Returns head without removing, returns null if empty
        System.out.println("Peek: " + q.peek()); // Output: A
		
        // 4️⃣ element() – Same as peek() but throws exception if empty
        System.out.println("Element: " + q.element()); // Output: A
		
        // 5️⃣ poll() – Removes and returns head, returns null if empty
        System.out.println("Poll: " + q.poll()); // Output: A
		
        // 6️⃣ remove() – Removes and returns head, throws exception if empty
        System.out.println("Remove: " + q.remove()); // Output: B
		
        // Remaining Queue: [C]
        System.out.println("Queue: " + q); // Output: [C]
    }
}
```




# Tree

# Tree implementation using ArrayList

```java
import java.util.ArrayList;

public class TreeNode<T> {
    public T data;
    public ArrayList<TreeNode<T>> children;
	
    public TreeNode(T data){
        this.data = data;
        children = new ArrayList<>();
    }
}
```

```java
public class TreeUse {
    public static void main(String[] args) {
        TreeNode<Integer> root = new TreeNode<Integer>(4);
        TreeNode<Integer> node1 = new TreeNode<Integer>(2);
        TreeNode<Integer> node2 = new TreeNode<Integer>(3);
        TreeNode<Integer> node3 = new TreeNode<Integer>(5);
        TreeNode<Integer> node4 = new TreeNode<Integer>(6);
        
        root.children.add(node1);
        root.children.add(node2);
        root.children.add(node3);
		
        node2.children.add(node4);
    }
}
```


```java
import java.util.*; // added for Queue

public class TreeUse {
    
    // DFS-style recursive tree input
    public static TreeNode<Integer> takeInput() {
        Scanner s = new Scanner(System.in);
        
        // Ask for node data
        System.out.println("Enter next node data");
        int r = s.nextInt();
        
        // Create current node
        TreeNode<Integer> root = new TreeNode<Integer>(r);
        
        // Ask how many children this node has
        System.out.println("Enter number of children for " + r);
        int childCount = s.nextInt();
		
        // Recursively build child subtrees
        for (int i = 0; i < childCount; i++) {
            TreeNode<Integer> child = takeInput();
            root.children.add(child);
        }
		
        return root;
    }
	
    // DFS-style tree printing (flat view)
    private static void print(TreeNode<Integer> root) {
        String s = root.data + ":";
		
        // Append all immediate children
        for (int i = 0; i < root.children.size(); i++) {
            s = s + root.children.get(i).data + ",";
        }
        System.out.println(s);
		
        // Recursively print each child subtree
        for (int i = 0; i < root.children.size(); i++) {
            print(root.children.get(i));
        }
    }
	
    // ASCII Tree Printer (Pretty structure view)
    public static void printBetter(TreeNode<Integer> root) {
        printBetterHelper(root, "", true);
    }
	
    /**
     * Recursively prints tree with ASCII branches
     * 
     * @param node Current node
     * @param prefix Indentation + lines to show depth/branching
     * @param isTail True if node is last child (for └──), else false (for ├──)
     */
    private static void printBetterHelper(TreeNode<Integer> node, String prefix, boolean isTail) {
        if (node == null) return;
		
        // Print current node with proper branch symbol
        System.out.println(prefix + (isTail ? "└── " : "├── ") + node.data);
		
        // Handle all children except the last
        for (int i = 0; i < node.children.size() - 1; i++) {
            printBetterHelper(node.children.get(i), prefix + (isTail ? "    " : "│   "), false);
        }
		
        // Handle last child with a └──
        if (node.children.size() > 0) {
            printBetterHelper(node.children.get(node.children.size() - 1), prefix + (isTail ? "    " : "│   "), true);
        }
    }
	
    // BFS-style tree print (level-wise display)
    public static void printLevelWise(TreeNode<Integer> root) {
        if (root == null) return;
		
        Queue<TreeNode<Integer>> queue = new LinkedList<>();
        queue.add(root);
		
        while (!queue.isEmpty()) {
            TreeNode<Integer> currentNode = queue.poll();
            String output = currentNode.data + ":";
			
            for (int i = 0; i < currentNode.children.size(); i++) {
                output += currentNode.children.get(i).data;
                if (i != currentNode.children.size() - 1) {
                    output += ",";
                }
                queue.add(currentNode.children.get(i));
            }
			
            System.out.println(output);
        }
    }
	
    // count total number of nodes in tree
    private static int numNodes(TreeNode<Integer> root){
        if(root == null){
            return 0;
        }
        return numNodesHelper(root);
    }

    private static int numNodesHelper(TreeNode<Integer> root){
        int count = 1;
        for(int i = 0; i < root.children.size(); i++){
            count += numNodes(root.children.get(i));
        }
        return count;
    }

    // sum of all nodes
    private static int sumOfNodes(TreeNode<Integer> root){
        if(root == null) return 0;

        int sum = 0;
        sum += root.data;
        for(int i = 0; i < root.children.size(); i++){
            sum += sumOfNodes(root.children.get(i));
        }
        return sum;
    }

    // find node with maximum value
    private static int maxNode(TreeNode<Integer> root){
        if(root == null) return Integer.MIN_VALUE;
        
        int max = root.data;
        for(TreeNode<Integer> child : root.children){
            max = Math.max(max, maxNode(child));
        }
        return max;
    }

    // returns number of nodes greater than the given number
    private static int numNodesGreater(TreeNode<Integer> root){
        Scanner s = new Scanner(System.in);
        int num = s.nextInt();
        return numNodesGreaterHelper(root, num);
    }
    
    private static int numNodesGreaterHelper(TreeNode<Integer> root, int num){
        if (root.data == null) return 0;

        int count = 0;
        if (root.data > num) count++;

        for(TreeNode<Integer> child : root.children) {
            count += numNodesGreaterHelper(child, num);
        }
        return count;
    }

    // calculates height of the tree
    private static int getHeight(TreeNode<Integer> root) {
        if (root == null) return 0;
    
        int maxChildHeight = 0; // Track tallest child height
    
        for (TreeNode<Integer> child : root.children) {
            int childHeight = getHeight(child);
            maxChildHeight = Math.max(maxChildHeight, childHeight);
        }
    
        return maxChildHeight + 1; // Height = 1 (self) + tallest child
    }
    
    // Entry point of program
    public static void main(String[] args) {
        TreeNode<Integer> root = takeInput();
        
        System.out.println("Basic Tree Print");
        print(root); // DFS-style flat tree print
        
        System.out.println("ASCII Tree Print");
        printBetter(root); // Tree structure with branches
        
        System.out.println("Level-wise Tree Print");
        printLevelWise(root); // BFS-style level-wise print

        System.out.println("Number of nodes");
        System.out.println(numNodes(root)); // print number of nodes

        System.out.println("Sum of all nodes");
        System.out.println(sumOfNodes(root)); // print sum of all nodes

        System.out.println("Largest node");
        System.out.println(maxNode(root)); // print node with maximum value

        System.out.println("Number of nodes greater than given value");
        System.out.println(numNodesGreater(root)); // print number of nodes greater than the given value

        System.out.println("Height of tree");
        System.out.println(getHeight(root)); // print height of tree
    } 
}
```

Above `printBetter` use ASCII **branches like └──, ├──, │**. to print tree
i.e.
└── 1
    ├── 2
    │   ├── 4
    │   └── 5
    └── 3

`private static void printBetterHelper(TreeNode<Integer> node, String prefix, boolean isTail)`

`printBeterHelper` is just a wrapper function. It calls the recursive helper with:

 Parameters:
- **`node`** – Current node we’re printing.
- **`prefix`** – Indentation + lines (`│` or   ) that represent vertical branches.
- **`isTail`** – Is this node the last child of its parent? (Used to decide whether to draw `└──` or `├──`























