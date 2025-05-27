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

### Naming Conventions Recap:
- **Classes**: `ParentClass`, `ChildClass` (PascalCase)
- **Methods**: `display`, `main` (camelCase)
- **Variables**: Same as methods, follow camelCase.

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

#### For-each
i.e. using for-each loop to print each element of an array
```java
class Main{
	public static void main(String[] args){
		int arr[]={1,2,3,4,5};
		
		for(int e : arr){ //for-each
			System.out.println(e+""); //Output: 1 2 3 4 5
		}
	}
}
```


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
		static void display(){
			System.out.println("static method inside static nested class");	
		}
	}
	
	public static void main(String[] args){
		StaticInner inner=new StaticInner();
		inner.show();
		// Outer.StaticInner.show(); we cannot do this without creating Outer or Inner class cause show is not static
		Outer.StaticInner.display();
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
		new Outer().outerMethod(); // call outerMethod where LocalInner is used (anonymous object)
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
https://youtu.be/LNpUj80JLGI
https://youtu.be/4YnGBOyA2Q4

+ It is a special, nameless inner class that is defined and instantiated in a single expression.
+ You instantiate the anonymous class at the same time as you define it.
+ Single use
+ Is always going to be a **subclass** 
	+ by **implementation** of an interface.
	+ by **extending** an abstract class

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
# Functional Programming
 https://youtu.be/tPeLYpSQ37k
 + We have functional interface, lambda expression, method reference to support functional programming style(paradigm) in java
 + Functional programming in Java emphasizes treating functions as first-class citizens, enabling functions to be 
	 + passed as arguments, returned as values, and assigned to variables. 
	 + This paradigm promotes immutability, pure functions, and declarative style, enhancing code readability, maintainability, and testability.

Functional programming in Java refers to using functions as first-class citizens — meaning we can:
- Pass functions (via lambdas or method references)
- Return functions (using functional interfaces)
- Avoid mutability and side effects
- Embrace expressions over statements (e.g., stream pipelines instead of loops)

---
# Functional Interface
https://youtu.be/Gs8ZPKCFlTc
https://www.geeksforgeeks.org/java-functional-interfaces/

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
	public void execute(){ // cause by default methods in interface are abstract and public
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
The lambda `()->System.out.println(...)` is the implementation of the single method in `MyFun`

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


#### Built-In Java Functional Interface

| Interface             | Method Signature                      | Description                                                                                        |
| --------------------- | ------------------------------------- | -------------------------------------------------------------------------------------------------- |
| **Runnable**          | `void run()`                          | Executes code on a thread, no input/output.<br>Only contains the `run()` method                    |
| **Callable**          | `V call()`                            | Like Runnable, but returns a result and can throw exceptions.<br>Only contains the `call()` method |
| **Comparable**        | `int compareTo(T o)`                  | Compares current object with another. Used in sorting.<br>Only contains the `compareTo()` method   |
| **Comparator**        | `int compare(T o1, T o2)`             | Compares two different objects. Used in sorting collections.                                       |
| **ActionListener**    | `void actionPerformed(ActionEvent e)` | Used in GUI for button or event handling.<br>Only contains the `actionPerformed()` method          |
| **Predicate**         | `boolean test(T t)`                   | Tests a condition (like filters).                                                                  |
| **Function<T,R>**     | `R apply(T t)`                        | Takes input `T`, returns output `R`                                                                |
| **Consumer**          | `void accept(T t)`                    | Takes input `T`, performs an action (no return)                                                    |
| **Supplier**          | `T get()`                             | Provides a result of type `T` (no input)                                                           |
| **BiFunction<T,U,R>** | `R apply(T t, U u)`                   | Takes `T` and `U`, returns `R`                                                                     |
| **UnaryOperator**     | `T apply(T t)`                        | A special `Function` where input and output are same type.                                         |
| **BinaryOperator**    | `T apply(T t1, T t2)`                 | A special `BiFunction` where all types are the same.                                               |

##### Runnable
i.e.
```java
public class LambdaRunnableDemo{
	public static void main(String[] args){
		Runnable r=()->System.out.println("Thread is running");
		new Thread(r).start();
	}
}
```

##### Comparator 
i.e.

# Types of Functional Interfaces in Java
- Java 8 added the `java.util.function` package with a bunch of **ready-to-use lambdas** (Predicate, Function, etc.)
#### 1. Consumer 

#### 2. Predicate
#### 3. Function
#### 3. Supplier
A `Supplier<T>` is a function that takes no input and returns a value of type `T` when you call `.get()`
Use case:  for lazy loading or injecting dependencies later

TODO: incomplete





---
# Sealed Classes and Sealed Interfaces
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


---
# Method Reference
https://youtu.be/ar5jQQRWxFM
https://www.geeksforgeeks.org/method-references-in-java-with-examples/
+ Method reference are a shorthand notation of a lambda expression to call a single method directly.
+ They allow you to refer to methods or constructors without invoking them.

```java
//lambda expression
list.forEach(name->System.out.println(name));

//method reference
list.forEach(System.out::println);

```

Key Benefits
+ Improved Readability
+ Reusability
+ Functional Programming Support

#### Types of Method Reference

##### 1. Reference to a static method

Syntax: `ClassName::staticMethodName`
Use case: You have a static method you want to pass as behaviour

i.e.
```java
import java.util.Arrays;

public class Main{
	public static void print(String s){ //static method print
		System.out.println(s);
	}
	
	public static void main(String[] args){
		String[] names={"Alice","Bob","Charlie"};
		Arrays.stream(names).forEach(Main::print); //using method reference to print all names
		//Output: 
		//Alice
		//Bob
		//Charlie
	}
}
```

i.e.
```java
class Demo{
	public static void sayHello(){
		System.out.println("Hello");
	}
	
	public static void main(String[] args){
		Runnable r=Demo::sayHello;
		r.run();
	}
}
```


##### 2. Reference to an instance method of a particular object

Syntax: `insttance::instanceMethodName`
Use case: when you want to use method from specific object
i.e.
```java
import java.util.Arrays;

class Printer{
	void print(String msg){
		System.out.println(msg);
	}
}
public class Main{
	public static void main(String[] args){
		Printer p=new Printer();
		//intead of writing msg->p.print(msg)
		Arrays.asList("one","two").forEach(p::print);
	}
}
```


i.e.
```java
class Demo{
	void sayHello(){
		System.out.println("Hello");
	}
	
	public static void main(String[] args){
		Demo obj=new Demo();
		Runnable r=obj::sayHello;
		r.run();
	}
}
```


##### 3. Reference to an instance method of an arbitrary object of a particular type

Syntax: `ClassName::instanceMethodName`
Use case: Each element in a collection has that method. You want to apply it to each

```java
import java.util.Arrays;
import java.util.List;

public class Main{
	public static void main(String[] args){
		List<String> list=Arrays.asList("one","two");
		
		//intead of writing s->s.toUpperCase()
		list.stream().map(String::toUpperCase).forEach(System.out::println);
	}
}
```



##### 4. Reference to a  constructor

Syntax: `ClassName::new`
Use case: when you want to create new objects dynamically like in streams, dependency injection, factories etc

```java
import java.util.function.Supplier;

class Demo{
	Demo{
		System.out.println("New demo created");
	}
}

public class Main{
	public static void main(String[] args){
		//Instead of writing ()->new Demo()
		Supplier<Demo> s=Demo::new;
		s.get(); //Triggers constructor
	}
}
```
Whenever someone calls `.get()`, run `new Demo()` and return it.
`Supplier<T>` takes no input and returns a value of type `T` when you call `.get()`

.i.e.
```java 
interface MessageCreator{
	Message createMessage(String msg);
}

class Message{
	Message(String msg){
		System.out.println(msg);
	}
}

public class ConstructorReferenceDemo{
	public static void main(String[] args){
		MessageCreator creator=Message::new;
		creator.createMessage("hello");
	}
}
```
`Message::new` is a **constructor reference**.
+ which(constructor) creates and returns a `Message` object — so the return type must be `Message` in interface
It matches the method in the `MessageCreator` interface:
So Java links the `createMessage(String)` method to the constructor `Message(String)`.


---
# Java Base64 Encode and Decode
https://www.baeldung.com/java-base64-encode-and-decode
Base64 in Java is a way of **encoding binary data into an ASCII string format** using a **set of 64 characters** (A-Z, a-z, 0-9, +, /). It's **not encryption**, just a way to make data safely transferable or storable.
+ binary to text encoding scheme
+ Takes 3 bytes of binary data and turns it into 4 ASCII characters
+ It's part of the `java.util.Base64` class (added in java 8)

i.e. Base64 Encode and Decode
```java
import java.util.Base64;

class Base64ConvertExample{
	public static void main(String[] args){
		String str="Example of base 64 conversion";
		byte[] b=str.getBytes();
		System.out.println("bytearray: "+b);
		//Converting into Base64 (Encoding)
		String base64=Base64.getEncoder().encodeToString(b);
		System.out.println("encoded string: "+base64);
		//Converting Base64 to binary (Decoding)
		byte[] decodedBytes=Base64.getDecoder().decode(base64);
		String s=new String(decodedBytes); //s is decoded string
		System.out.print(s);
	}
}
```

In Base64 encoding, the length of an output encoded string must be a multiple of four. If necessary , the encoder adds one or two padding characters(=) at the end of the output as needed in order to meet this requirement.
Upon decoding the decoder discards these extra padding characters

.i.e. skipping padding while encoding
```java
import java.util.Base64;

class Base64ConvertExample {
    public static void main(String[] args) {
        String originalString = "Example of base 64 conversion";
        // Encode
        String encodedString =Base64.getEncoder().withoutPadding().encodeToString(originalString.getBytes());
        System.out.println("Encoded: " + encodedString);
        // Decode
        byte[] decodedBytes = Base64.getDecoder().decode(encodedString);
        String decodedString = new String(decodedBytes);
        System.out.println("Decoded: " + decodedString);
    }
}
```


---
# Try with Resources
+ Is a try block that declares and initializes one or more resources (objects that implement `AutoCloseable` or `Closeable`)
+ These resources are automatically closed at the end of the statement, even if an exception is thrown
+ try-with-resources block can still have the catch and finally

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

class TryWithResourcesExample{
	public static void main(String[] args){
		try(BufferedReader reader=new BufferedReader(new FileReader("file.txt"))){
			String line;
			while((line=reader.readLine())!=null){
				System.out.println(line);
			}
		}catch(IOException e){
			e.printStackTrace();
		}
	}	
}
```
No need to call `reader.close()` — Java handles it for you.


---
# yield keyword in switch expression (java 14+)
https://dev.java/learn/language-basics/switch-expression/
https://www.geeksforgeeks.org/scala-yield-keyword/
https://www.geeksforgeeks.org/switch-statement-in-java/

+ Used to **pause the function** and send a value to the caller.
+ No fall-through between cases in switch expression.
+ Think of `yield` as the **equivalent of `return` inside a switch block** — but only **within switch expressions** .

i.e.
```java
class YieldTest {
    public enum Day {
        SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
    }

    public static void main(String[] args) {
        Day[] dayNow = Day.values(); // create array of enum using enum values

        for (Day currDay : dayNow) { // for-each
            boolean result = switch (currDay) {
                case MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY -> {
                    System.out.println(currDay + " is a weekday");
                    yield true;
                }
                case SATURDAY, SUNDAY -> {
                    System.out.println(currDay + " is a holiday");
                    yield false;
                }
            };
            System.out.println("Result: " + result);
            System.out.println(result ? "students are present" : "students are absent");
            System.out.println();
        }
    }
}
```
- `break` is illegal in **switch expressions** with `->` and it does not return value so we  can't use it here.
- `break` is for exiting **switch statements**, not expressions.
- If you had used **`return`** inside your `switch`, it would have exited the entire `main()` method **immediately**, so none of this would have printed:
```java
System.out.println("Result: "+result);
System.out.println(result ? "student's are present": "student's are absent");
System.out.println();
```


---
# Text Blocks
https://www.geeksforgeeks.org/text-blocks-in-java-15/
+ It allows you to write multi-line string literals in a more readable and clean way using double quotes `"""`
- **Begins and ends** with triple double quotes: `"""`
- Automatically handles **newlines and indentation**.
- Great for **HTML, JSON, SQL**, or other multi-line content.

```java
String textBlock = """
    This is a text block.
    It spans multiple lines.
    No need for \n or + for concatenation.
    """;
```


---
# Annotations 
https://www.programiz.com/java-programming/annotations
https://www.geeksforgeeks.org/annotations-in-java/

+ These are metadata for our program source code that provide additional information about the program and this information is used by compiler and JVM
+ Syntax: `@AnnotationName`

There are 5 categories of annotations as listed:
##### 1. Marker Annotations
+ **Definition**: An annotation with no elements/parameters
+ **Purpose**: Used to mark or flag something. The presence of the annotation alone gives information

i.e.
```java
@override
public void run(){}
```

##### 2. Single Value Annotation
- **Definition:** Contains **only one element**.
Syntax:
`@AnnotationName(elementName = "elementValue")`

If there is only one element, it is a convention to name that element as value.
`@AnnotationName(value = "elementValue")`

In this case, the element name can be excluded as well. The element name will be value by default.
`@AnnotationName("elementValue")`

##### 3. Full Annotations
- **Definition:** Annotation with **multiple elements** (key-value pairs).
Syntax: `@TestAnnotation(owner=”Rahul”, value=”Class Geeks”)`

##### 4. Type Annotations
- **Definition:** Used to **annotate types** such as class, interface, type parameters, etc.
Syntax: `@NonNull String str;`
This declaration specifies non-null variable `str` of type `String` to avoid `NullPointerException`.

##### 5. Repeating Annotations
- **Definition:** Allows using the **same annotation multiple times** on the same element.
+ For an annotation to be repeatable it must be annotated with the **@Repeatable** annotation, which is defined in the `java.lang.annotation` package.

---
# Local Variable Type Inference
https://www.baeldung.com/java-10-local-variable-type-inference
https://www.geeksforgeeks.org/local-variable-type-inference-or-lvti-in-java-10/
+ Introduced in java 10
+ It allows you to declare local variables without explicitly specifying their type, and the compiler infers the type based on the context.

Syntax: `var variableName = expression;`
The type of `variableName` is inferred from the right-hand side `expression`.

i.e.
```java
var message = "Hello, Java";  // Inferred as String
var number = 42;              // Inferred as int
var list = new ArrayList<String>();  // Inferred as ArrayList<String>
```
### Rules & Limitations

1. **Only for local variables**:
    - Inside methods
    - In loops (e.g., `for` loops)
    - Not allowed for instance variables or method parameters/return types.

2. **Cannot be used without initialization**:
    `var name;  // ❌ Compilation error`

3. **Type is fixed after assignment**:
```java
var value = 10;    // int
value = "hello";   // ❌ Error: incompatible types
```

---
# Records






---
TODO: 
+ Annotation
+ java module system
+ Records
+ Stream api

---
# Searching and Sorting

# [Binary Search](https://www.w3schools.com/dsa/dsa_algo_binarysearch.php)
+ works on sorted array only




---
# OOPS

---

## `this` keyword
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

---
## `final` keyword
+ to finalise(fix) value .
+ final function can not be override.
+ final class can not be inherited by other class 
+ final class can not inherit other class

---
## `static` keyword
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
## `super` keyword

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
+ method overriding means the child class method should have the same method signature as the parent class method
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


