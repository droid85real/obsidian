Js is a 
+ interpreted
+ jit compiled
+ multi-paradigm
+ prototype based (allows the creation of an object without first defining its class)
+ synchronous
+ single threaded
+ dynamic language (no need to define data type)

# JavaScript Variable Declarations: 
## `var`
- **Function-scoped**: Only accessible within the function where it's declared.
- **Hoisted**: Moves to the top of its scope, but **not initialized**, so accessing it before the declaration gives `undefined`.
- **Can be redeclared and updated**.

```js
function test() {
  console.log(a); // undefined (hoisted)
  var a = 10;
  console.log(a); // 10
}
```

## `let`
- **Block-scoped**: Only accessible within the `{}` block where it's declared.
- **Hoisted**, but **not initialized**: Accessing before declaration causes a **ReferenceError**.
- **Can be updated, but not redeclared** in the same scope.

```js
{
  console.log(b); // ReferenceError
  let b = 20;
}
```

## `const`

- **Block-scoped**, like `let`.
- **Must be initialized** at the time of declaration.
- **Cannot be updated or redeclared**.

```js
const PI = 3.14;
PI = 3.15; // TypeError
```

However, **objects and arrays declared with `const` can have their contents changed**:
```js
const obj = { name: "Alice" };
obj.name = "Bob"; // ✅ This is allowed
```

## ✅ Quick Summary

| Feature       | `var`           | `let`       | `const`     |
| ------------- | --------------- | ----------- | ----------- |
| **Scope**     | Function        | Block       | Block       |
| **Hoisting**  | Yes (undefined) | Yes (TDZ\*) | Yes (TDZ\*) |
| **Redeclare** | Yes             | No          | No          |
| **Reassign**  | Yes             | Yes         | No          |

> \*TDZ = Temporal Dead Zone — accessing the variable before it's declared throws a `ReferenceError`.


# ( && ) AND Operator 
+ first falsy and last truthy

# ( || ) OR Operator
+ first truthy and last falsy

### Falsy Values in JavaScript

In JavaScript, **falsy values** are values that evaluate to `false` in a boolean context. These include:
- `false`
- `0`
- `''` (empty string)
- `null`
- `undefined`
- `NaN` (not a number)
Any other value is considered **truthy**

## `undefined`
- A variable that has been declared but has not yet been assigned a value is `undefined`. It’s the default value of uninitialized variables.
- A function that doesn't return anything will implicitly return `undefined`.
- Accessing a non-existent property of an object or an array index that is out of bounds will return `undefined`.
- `typeof` undefined is `undefined`

## `null`
+ `null` is an explicit assignment that represents the intentional absence of any object value. It’s an object that represents "nothing" or "no value."
+ It's typically used when you want to explicitly indicate that a variable should be empty or has no value.
+ `typeof` null is object

>NOTE:
- **Loose equality (`==`)**: `undefined` and `null` are considered equal.
- **Strict equality (`===`)**: They are **not** the same.


`Number.MAX_VALUE` for largest positive number
`Number.MIN_VALUE` for smallest positive number

### Infinity 
+ **Infinity** is a special constant in JavaScript, but it's **not a data type** on its own

**Positive Infinity**: When you divide a positive number by zero, you get positive infinity.
```js
console.log(1 / 0);  // Infinity
```

**Negative Infinity**: When you divide a negative number by zero, you get negative infinity.
```js
console.log(-1 / 0);  // -Infinity
```



# Type coercion
+ It refers to the automatic or implicit conversion of values from one data type to another.

**Implicit coercion**
```js
console.log('5' + 5);        // "55" (string '5' is concatenated with 5)
console.log('5' - 5);        // 0 (string '5' is coerced to number and subtracted)
console.log('5' * '2');      // 10 (string '5' and '2' are coerced to numbers)
console.log(5 == '5');       // true (string '5' is coerced to number)
console.log(5 === '5');      // false (no coercion, different types)
console.log(null == undefined);  // true (they are loosely equal)
console.log(!!'hello');     // true (non-empty string is truthy)
console.log(!!0);           // false (0 is falsy)
```

**Explicit Coercion**
```js
let num1 = Number('123');    // 123
let num2 = parseInt('123px');  // 123 (parses integer part)
let num3 = parseFloat('123.45px');  // 123.45 (parses float part)

let str1 = String(123);   // "123"
let str2 = (123).toString(); // "123"
let str3 = `${123}`;        // "123" (template literal)

let bool1 = Boolean(0);   // false (0 is falsy)
let bool2 = Boolean('');   // false (empty string is falsy)
let bool3 = Boolean('hello');  // true (non-empty string is truthy)
```

---
# Ternary operator

`(condition) ? (true expression) : (false expression);`
```js
(num1>num2) ? (num1) : (num2===num1 ? "equal" : num2);
```
Above we checking, if `num1` is greater than `num2`, and if so, return `num1`. If `num1` and `num2` are equal, return `"equal"`. Otherwise, return `num2`



---
# Functions

**Function declaration**
```js
function greet(name) {
  return "Hello, " + name + "!";
}

console.log(greet("Alice")); // Output: Hello, Alice!
```

**Function expression**
```js
const greet=function(name){
	return "Hello, "+name+"!";
}

console.log(greet("droid85")); //Output: Hello, droid85!
```
+ `function ()` inherit `this` depends on how it is called.


**Arrow Function (ES6+)**
```js
const greet=(name)=>{
	return "Hello, "+name+"!";
};
console.log(greet("droid85")); //Output: Hello, droid85!
//or
const greetShort=name=> "Hello, "+name+"!";
console.log(greatShort("droid85")); //Output: Hello, droid85!
```
+ Arrow function inherit `this` from parent



**Anonymous Function**
+ Used when you don’t need to name a function, often as an argument:
```js
setTimeout(function() {
  console.log("This runs after 1 second");
}, 1000);
```


**Immediately Invoked Function Expression (IIFE)**
+ Runs as soon as it is defined:
```js
(function(){
	console.log("I run immediately");
})();
```

## Default parameter
```js
function sum(num1=0,num=0){
	console.log(`sum of the numbers is ${num1+num2}`);
}
sum(4,5);
sum(4); //safe due to default parameter
sum(); //safe due to default parameter
```

If a parameter is not provided when calling a function, its value will be `undefined`
```js
function greet(name){
 console.log(name);
}
greet(); //Output: undefined
```


---
# ARRAY

#### Array creation
```js
const cars=new Array('Volvo','BMW');
console.log(cars);

const students=['Alex','google','Sony',10,true];
console.log(students);
console.log(students[0]); //access element at Oth index
```

#### Adding and Removing elements
##### `push()`
+ Adds one or more elements to the end
```js
const arr=[1,2,3];
arr.push(4,5);
console.log(arr); //Output: [1,2,3,4,5]
```

##### `pop()`
+ Removes the last element
```js
const arr=[1,2,3];
arr.pop();
console.log(arr); //Output: [1,2]
```

##### `unshift()`
+ Adds one or more elements to the beginning
```js
const arr=[2,3];
arr.unshift(1);
console.log(arr); //Output: [1,2,3]
```

##### `shift()`
+ Removes the first element
```js
const arr=[1,2];
arr.shift();
console.log(arr); //Output: [2]
```

##### `slice()`
+ Returns a shallow copy of a portion of the array
```js
const arr=[1,2,3,4];
const slicedArr=arr.slice(1,3); //From index 1 to index 3 (not included)
console.log(slicedArr); // Output: [2,3]
```

##### `splice()`
+ Changes the content of an array by removing or replacing existing elements and/or adding new elements in place

```js
array.splice(startIndex, deleteCount, item1, item2, ..., itemN);
```
`startIndex`: The index at which to start changing the array
`deleteCount`: The number of elements to remove starting from `startIndex`. If set to 0, no elements will be removed.
`item1,item2...itemN`: Optional elements to add to the array, starting from `startIndex`.

```js
let arr=[1,2,3,4,5,6];
arr.splice(1,3,7,8,9); //start at index 1,remove 3 elements, insert 7,8,9
console.log(arr); // Output: [1,7,8,9,5,6]
```

#### Searching and Filtering
##### `indexOf(value)`
+ Returns the first index of an element, or -1 if not found
```js
const arr=[1,2,3];
console.log(arr.indexOf(3)); //returns 2
console.log(arr.indexOf(5)); //returns -1
```
##### `lastIndexOf(value)`
+ Returns the last index of the element `value` or -1 if not found
```js
const arr=[1,2,3,2];
console.log(arr.lastIndexOf(2)); //Output: 3
```

##### `include()`
+ Checks if the array contains a specific element
```js
const arr=[1,2,3,4];
console.log(arr.include(2)); //return true
console.log(arr.include(5)); //returns false
```

##### `filter()`
+ Returns an array of all elements that satisfy a condition
```js
const arr=[1,2,3,4];
const filteredArr=arr.filter(num=>num>2);
console.log(filteredArr); //Output: [3,4]
```

##### `find()`
+ will return the first element that matches the condition or undefined if not found
```js
const arr=[1,2,3,4];
const found=arr.find(num=>num>2);
console.log(found); //Output: 3
```

```js
const users = [
  {name: "Alice", age: 25},
  {name: "Bob", age: 30}
];
const found = users.find(user => user.age > 26);
console.log(found); // {name: "Bob", age: 30}
```

##### `findIndex(callback)`
+ Returns the index of the first element matching the condition or -1
```js
const numbers = [5, 12, 8, 130, 44];
const index = numbers.findIndex((num) => num > 10);
console.log(index); // Output: 1 (because 12 is the first number > 10)
```

#### Sorting and Reversing
##### `reverse()`
+ Reverse the array in place
```js
const arr=[1,2,3,4];
arr.reverse();
console.log(arr); //Output: [4,3,2,1]
```

##### `sort(comparison function)`
+ Sorts the array(mutates the original array)

when no comparison function is provided, it implicitly converts each array element to a string before sorting. The sorting happens lexicographically.
```js
let arr = [10, 2, 5, 1];
arr.sort();
console.log(arr); // Output: [1,10,2,5]
```
+ js converts the numbers to strings when sorting. The comparison happens based on **character-by-character** comparison.
- When comparing `"10"` and `"2"`, JavaScript first compares the first character in both strings, which are `'1'` and `'2'`. Since `'1'` is lexicographically smaller than `'2'`, `"10"` gets sorted before `"2"`.
- So the result of sorting `[10, 2, 5, 1]` is `[1, 10, 2, 5]`, which isn't numerically correct.

To fix this we provide comparison function
```js
let arr = [10, 2, 5, 1];
arr.sort((a, b) => a - b);  // Comparison function
console.log(arr);  //Output: [1, 2, 5, 10]
```
`(a, b) => a - b`:
- If `a - b` is **positive**, `a` is considered greater than `b`, and `b` will come before `a` in the array.
- If `a - b` is **negative**, `a` is considered smaller than `b`, and `a` will come before `b`.
- If `a - b` is **zero**, `a` and `b` are considered equal for sorting purposes.


#### Transforming Arrays
##### `map()`
+ Creates a new array by applying a function to each element.

Syntax
`let newArray=array.map(callback(currentValue,index,array));`

`callback`: A function that will be applied  to each element
`currentValue`: The current element being processed.
`index`: (optional) The index of the current element
`array`: (optional) The original array being processed

i.e.
```js
const arr=[1,2,3];
const squaredArr=arr.map(num => num*num);
console.log(squaredArr); //Output: [1,4,9]
```

i.e Using traditional callback function
```js
const numbers=[1,2,3,4,5];
let squaredArr=numbers.map(function(num){
	return num*num;
});
console.log(squaredArr); // Output: [1,4,9,16,25]
```

i.e. Using map with index parameter
```js
let names=["Alice","Bob","Charlie"];
let indexedArr=names.map((name,index)=> `${index+1}.${name}`);
console.log(indexedArr); //Output: ['1. Alice', '2. Bob', '3. Charlie']
```

##### `reduce()`
+ Reduces the array to a single value

Syntax
```js
array.reduce((accumulator,currentValue,currentIndex,array)=>{
	//logic
},initialValue);
```
`accumulator`: accumulates the result
`currentValue`: current element being processed
`initialValue`: (optional) but good to provide

i.e. sum of array
```js
const arr=[1,2,3,4];
const sum=arr.reduce((acc,curr)=>acc+curr,0);
console.log(sum); // Outpuut: 10
```

i.e. count occurrences
```js
const fruits=["apple","banana","apple","orange","banana","apple"];
const count=fruits.reduce((acc,fruit)=>{
	acc[fruit]=(acc[fruit] || 0)+1;
	return acc;
},{});
console.log(count); //Output: { apple: 3, banana: 2, orange: 1 }
```
In above,`acc` is initially an empty object.
`acc[fruit] = (acc[fruit] || 0) + 1;` is equal to
```js
if (acc[fruit]) {
  acc[fruit] = acc[fruit] + 1;
} else {
  acc[fruit] = 0 + 1;
}
```
and when acc check for the first time it is undefined for apple
```js
acc['apple'] = (undefined || 0) + 1;
```
undefined is falsy, 0 is falsy too. || or operator returns last falsy value which is 0
0+1=1

i.e.
```js
function redFun(acc,curr){
	return curr%2==0 ? acc+curr : acc;
}
const numbers=[1,2,3,4,5,6];
const sumEven=numbers.reduce(redFun,0);
console.log(sumEven); //Output: 12
```

##### `flat()`
+ Flattens nested arrays into a single array
```js
const arr=[1,2,[3,4],[5,6]];
const flatArr=arr.flat();
console.log(flatArr); //Output: [1,2,3,4,5,6]
```


#### Iteration Method
##### `forEach(callback)`
Runs `callback` on each element, (doesn’t return a value).
```js
const arr=[1,2,3];
arr.forEach((elem,index)=>console.log(`Index ${index}: ${elem}`));
```

##### `every(callback)`
Returns true if all elements satisfy the condition
```js
const allPositive=[1,2,3].every(n=>n>0);
console.log(allPositive); // true
```

##### `some(callback)`
Returns true if any element satisfies the condition
```js
const someNegative=[1,-2,3].some(n=>n<0);
console.log(someNegative); // true
```

##### `values()`
+ Iterates over the actual elements of the array.
```js
const arr=["a","b","c"];
for(const value of arr.values()){
	console.log(value);
	// Output:
	//a
	//b
	//c
}
```

same as above
```js
const arr=["a","b","c"];
for(const val of arr){
	console.log(val);
}
// Output:
//a
//b
//c
```

```js
const arr=["a","b","c"];
for(let i in arr){
	console.log(i); // for index
	console.log(arr[i]); //for element
}
```

```js
const arr=["a","b","c"];
for(let i of arr){
	console.log(i); 
	//Output: 
	//a
	//b
	//c
}
```

##### keys
+ Iterates over the indexes of the array
```js
const arr=["a","b","c"];
for(const key of arr.keys()){
	console.log(key);
}
//Output:
//0
//1
//2
```

##### `entries()`
+ Iterates over `[index,value]` pairs like python's `enumerate()`
```js
const arr=["a","b","c"];
for(const[index,value] of arr.entries()){
	console.log(index,value);
}
// Output: 
//0 a
//1 b
//2 c
```

#### Checking
##### `Array.isArray(variable)`
+ Checks if the variable is an array
```js
const arr=[1,2,3];
console.log(Array.isArray(arr)); //returns true
console.log(Array.isArray("Hello")); //return false
```

##### `Array.from(iterable)`
+ Creates a new array from
```js
const str="hell";
const arrFromStr=Array.from(str);
console.log(arrFromStr); //Output: ['h','e','l','l']
```

##### `Array.of()`
+ Creates a array from the provided arguments
```js
const arr=Array.of(1,2,3,4);
console.log(arr); //Output: [1,2,3,4]
```

#### Filling and Copying Methods
##### `fill(value,start,end)`
+ Fills array elements with a value from start to end (end exclusive)
```js
const arr=[1,2,3,4,5];
arr.fill(0,1,4);
console.log(arr); //Output: [1,0,0,0,5]
```

##### `copywithin(target,start,end)`
+ copies elements from `start` (inclusive) to `end` (exclusive) and pastes them starting at index `target`. It modifies the original array in-place.
```js
const arr=[1,2,3,4,5];
arr.copywithin(0,3,5);
console.log(arr); //Output: [4,5,3,4,5]
```


#### Joining and Combining

##### `concate()`
+ Returns a new array by concatenating the array with other arrays/values
```js
const arr1=[1,2];
const arr2=[3,4];
console.log(arr1.concat(arr2,5);); //Output: [1,2,3,4,5]
```

##### `join()`
+ Joins array elements into string separated by separator
```js
const fruits=["apple","banana","cherry"];
console.log(fruits.join(",")); //Output: apple,banana,cherry
```

##### `toString()`
+ Converts array to string (comma-separated)
```js
const arr=[1,2,3];
console.log(arr.toString()); //Output: "1,2,3"
```




The **rest** and **spread** operators in JavaScript look the same (`...`), but they serve **opposite purposes** depending on context:

#### `Rest Operator(...)`
+ Collects multiple elements into a single variable.
+ Used in function parameters and destructuring.
```js
// Function parameter
function sum(...numbers){
	return numbers.reduce((acc,curr)=>acc+curr,0);
}
sum(1,2,3); //6

// Array destructuring
const [first,...rest]=[10,20,30,40];
console.log(rest); // [20,30,40]

// Object destructuring
const {a,...others}={a:1, b:2, c:3};
console.log({a}); // {a:1}
console.log(a); // 1
console.log(others); // {b:2, c:3}
```


#### `Spread Operator(...)`
+ Expands elements of an array or object.
+ Used to copy, merge or pass values.
```js
// Function args
const nums=[1,2,3];
Math.max(...nums); //3

// Array merging
const arr1=[1,2];
const arr2=[3,4];
const merged=[...arr1,...arr2]; //[1,2,3,4]

// Object merging
const obj1={a: 1};
const obj2={b: 2};
const combined={...obj1,...obj2}; // {a: 1,b: 2}
```


#### Array Destructuring

```js
const arr=[10,20,30];

const [a,b,c]=arr;

console.log(a); // 10
console.log(b); // 20
console.log(c); // 30
```


#### Skipping items and default values

```js
const arr=[10,20];

const [a, ,c=30]=arr;

console.log(a); // 10
console.log(c); // 30 default because arr[2] is undefined
```


#### Destructuring as an assignment pattern
This means you can **reassign existing variables** from array values in a clean way.
```js
let a,b;
[a,b]=[100,200];

console.log(a); // 100
conole.log(b); // 200
```


#### Array Swapping

```js
let a=10;
let b=20;

[a,b]=[b,a]
console.log(a,b); // 20 10
```


---
# Object

#### Object Creation
```js
const student={
	name: 'Alexa',
	age: 10,
	hobby: 'Dancing',
	show: function(){
		console.log('This is the student details section');
	},
	100: 'hundred', 
};

console.log(student);
console.log(student.name);
console.log(student["name"]);
console.log(student[100]);
student.show();
```

#### object creation using new keyword then adding properties
```js
const person=new Object(); // creates an object

person.firstName="John";
person.lastName="Doe";
person.age=50;

console.log(person); //Output: { firstName: 'John', lastName: 'Doe', age: 50 }
```



working


TODO: length,split,hasownproperty

week6,topic3,lec44
#### 3. Adding/Updating Properties

javascript

CopyEdit

`let person = { name: "Bob", age: 35 };  // Adding a new property person.city = "New York";  // Updating an existing property person.age = 36;  console.log(person);  // { name: 'Bob', age: 36, city: 'New York' }`

---

#### 4. Deleting Properties

Use the `delete` operator:
```js
let person = { name: "Charlie", age: 40, city: "London" };
delete person.city;
console.log(person); // { name: 'Charlie', age: 40 }
```


---

#### 5. Object Methods

An object can have **methods**, which are functions that belong to the object.

```js
let car = {
  make: "Toyota",
  model: "Corolla",
  year: 2020,
  displayInfo: function () {
    return `${this.year} ${this.make} ${this.model}`;
  },
};
console.log(car.displayInfo()); // Output: 2020 Toyota Corolla
```


---

#### 6. Object Destructuring

```js
const person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 30
};

const { firstName, age } = person;

console.log(firstName); // John
console.log(age);       // 30
```

#### Renaming variables during destructuring:

```js
const { firstName: fName, lastName: lName } = person;

console.log(fName); // John
console.log(lName); // Doe
```

#### Destructuring as an assignment pattern
Just like arrays, you can destructure in assignments (not just declarations):
```js
let fName, lName;

({ firstName: fName, lastName: lName } = person);

console.log(fName); // John
console.log(lName); // Doe
```
The parentheses `()` are necessary to tell JS this is an expression, not a block.


#### Default Value 

```js
const { middleName = "N/A" } = person;

console.log(middleName);  // N/A
```
Here, `middleName = "N/A"` means:  
If `middleName` doesn’t exist or is `undefined`, assign `"N/A"` instead.


---

#### 7. Nested Objects
```js
let user = {
  name: "Jake",
  address: { 
    street: "123 Main St", 
    city: "Los Angeles", 
    zip: "90001" 
  },
};
console.log(user.address.city); // Output: Los Angeles
```


#### Nested Object Destructuring
```js
const user = {
  id: 101,
  name: {
    first: 'Alice',
    last: 'Smith'
  }
};

const { name: { first, last } } = user;

console.log(first); // Alice
console.log(last);  // Smith
```

#### `this` Keyword in object method
+ Inside an object method, `this` refers to the object itself.

```js
let person = {
  firstName: "Sophia",
  lastName: "Lee",
  fullName: function () {
    return this.firstName + " " + this.lastName;
  },
};
console.log(person.fullName()); // Output: Sophia Lee
```


---

### Shallow Copy
- Copies **only one level** of the object/array.
- Nested objects/arrays are **still references** to the same memory.
- Changing nested data in one affects the other.
- `Object.assign({}, original)` or `.slice()` or `spread operator` for shallow copy

```js
const original = { name: "Amit", skills: ["JS", "React"] };
const shallow = { ...original }; // or Object.assign({}, original)

shallow.name = "Bob"; // only changes in shallow copy
console.log(original.name); // Amit
console.log(shallow.name); // Bob

shallow.skills.push("Node"); // also changes original.skills
console.log(shallow.skills); // ['JS', 'React', 'Node']
console.log(original.skills); // ["JS", "React", "Node"]
```

### Deep Copy
- Copies **everything recursively**.
- Nested objects/arrays are also new copies.
- Changing one object never affects the other.

```js
const original = { name: "Amit", skills: ["JS", "React"] };

// Simple deep copy using JSON (works only for JSON-safe data)
const deep = JSON.parse(JSON.stringify(original));

deep.skills.push("Node");

console.log(original.skills); // ["JS", "React"]
console.log(deep.skills); // ["JS", "React", "Node"]
```


---
### Passing the reference happens in objects not in primitive data type

##### 1️⃣ **Primitives**

Types: `string`, `number`, `boolean`, `null`, `undefined`, `bigint`, `symbol`
- Stored directly in memory as the value itself.
- When you assign them to another variable, a **copy of the value** is made.
- Changing one does **not** affect the other.


### 2️⃣ **Objects** (includes arrays, functions, dates, etc.)

- Stored in memory by reference — the variable **doesn’t hold the object itself**, but a **pointer (address)** to where it lives in memory.
- When you assign an object to another variable, **the reference is copied**, not the object.
- Now both variables point to the **same object**.
- Changing the object through one variable will show up in the other.



---


week 6 | topic 3 |
pending above and skipped some topic need to revisit


---

### Working of js

Execution Contexts https://youtu.be/zdGfo6I1yrA

pending

week 6| topic 4 |
+ lec 1

---
---
### OOPs in js
+ Objects in js are key value pairs

**Creating object and calling it** 

```js
const movie={
	title: "The Avengers",
	year: 2012,
	genre: "Action, Sci-fi, Thriller",
	cast: {
		main_lead: "Robert Downey Jr.",
		others: "Chris Evans",
	},
	getDetails: function(){
		console.log(
			`Title: ${movie.title}\nYear: ${movie.year}\nGenre: ${movie.genre}`
		);
	},
	getMovieDetails: function(detail){
		console.log(movie[detail]);
	},
};

console.log(movie.title); // The Avengers

movie.getDetails();
//Title: The Avengers
//Year: 2012
//Genre: Action, Sci-fi, Thriller

movie.getMovieDetails("year"); // 2012

console.log(movie.cast.main_lead); // Robert Downey Jr.

```

---
### `this` keyword
https://www.w3schools.com/js/js_this.asp

- `this` refers to the **context object** in which a function is executed.
- But **what that object is depends on HOW the function is called, not where or how it is defined.**
	+ Alone, `this` refers to the **global object**.
	+ In a function, `this` refers to the **global object**.
	+ In a function, in strict mode, `this` is `undefined`.
	+ In an object method, `this` refers to the **object**.
	+ In an event, `this` refers to the **element** that received the event.
	+ Methods like `call()`, `apply()`, and `bind()` can refer `this` to **any object**.

#### Four main ways `this` behaves
1. **Global Context (default binding)**
```js
console.log(this); // In browser, Logs: Window object

function fun(){
	console.log(this);
}

fun(); // In non-strict mode: Window (global object)
```



2. **Method Invocation (Object context)**

```js
const obj={
	name: "Joe",
	greet(){
		console.log(this.name);
	}
};

obj.greet(); // Joe
```
Here, `this` inside `greet` points to `obj`.



3. **Constructor Invocation (with `new`)**
When you call a function with `new`, `this` points to the **newly created object**.
```js
function Person(name){
	this.name=name;
}

const obj=new Person("Person1");
console.log(obj.name); // Person1

```


4. **Explicit Binding (`call`,`apply`,`bind`)**
You can manually set `this` using `call`, `apply`, or permanently with `bind`.
```js
function greet() {
  console.log(this.name);
}

const user = { name: 'droid85' };

greet.call(user);  // Logs: droid85

const boundGreet = greet.bind(user);
boundGreet();     // Logs: droid85
```

- `call` = invoke now, args individually.
- `apply` = invoke now, args as array.
- `bind` = return a new function with `this` fixed, invoke later.

`call` and `apply` both can be used to call an object method with another object as argument

**`call` example**
The example below calls person1.fullName with person2 as an argument, **this** refers to person2, even if fullName is a method of person1
```js
const person1={
	fullName: function(){
		return this.firstName+" "+this.lastName;
	}
}

const person2={
	firstName: "John",
	lastName: "Doe",
}

person1.fullName.call(person2); //John Doe
```


**`apply` example**
pass arguments as array
```js
const person1={
	fullName: function(title,suffix){
		return `${title} ${this.firstName} ${this.lastName} ${suffix}`
	}
};

const person2={
	firstName: "John",
	lastName: "Doe"
};
// Using apply with arguments passed as array
const result=person1.fullName.apply(person2,["Mr.","Jr."]); 

console.log(result); // "Mr. John Doe Jr."
```


`bind` example
with `bind()` a function can borrow a method from another object

```js
const person={
	firstName: "John",
	lastName: "Doe",
	fullName: function(){
		return this.firstName+" "+this.lastName;
	}
}

const member={
	firstName: "Hege",
	lastName: "Nilsen",
}

let fullName=person.fullName.bind(member);
console.log(fullName()); // Hege Nilsen
```
- `bind` **does NOT call the function immediately**.
- Instead, it returns a **new function** where `this` is permanently set to `member`.
- You can call this new function later, whenever you want.


**Special case: Arrow Functions**

Arrow functions don’t have their own `this`. Instead, they **inherit `this` from the surrounding lexical scope** — the function or context where they are defined.
```js
const obj = {
  name: 'droid85',
  greet: function() {
    const arrow = () => console.log(this.name);
    arrow();
  }
};

obj.greet();  // Logs: droid85
```


**Common mistakes**
Assigning a method to a variable and calling it loses the original `this`.

```js
const obj = {
  name: 'droid85',
  greet() {
    console.log(this.name);
  }
};

const fn = obj.greet;
fn();  // undefined or Window.name depending on mode, because `this` is lost
```
- To fix, bind `this` or call method on object directly.




---
### Constructor
+ special function used to create and initialize objects

**Classic Constructor Function**
```js
function Person(firstName,lastName){
	this.firstName=firstName;
	this.lastName=lastName;
	this.fullName=function(){
		return this.firstName+" "+this.lastName;
	};
}

const person1=new Person("John","Doe");
console.log(person1.fullName()); // John Doe
```
+ Methods like fullName are recreated for every new object (waste of memory)

**Using Prototypes (Classic way)**
```js
function Person(firstName,lastName){
	this.firstName=firstName;
	this.lastName=lastName;
}
Person.prototype.fullName=function(){
	return this.firstName+" "+this.lastName;
};

const person1=new Person("John","Doe");
const person2=new Person("Jane","Smith");

console.log(person1.fullName()); // John Die
console.log(person2.fullName()); // Jane Smith
```
- Methods live on the prototype — shared across all instances.


**ES6 Classes (Modern Way) Syntactic sugar for constructors+prototype**
```js
class Person{
	constructor(firstName,lastName){
		this.firstName=firstName;
		this.lastName=lastName;
	}
	
	fullName(){
		return `${this.firstName} ${this.lastName}`;
	}
}

const person1=new Person("John","Doe");
console.log(person1.fullName()); // John Doe

console.log(person1.hasOwnProperty("firstName")); // true
console.log(person1.hasOwnProperty("fullName")); // false
console.log(Person.prototype.hasOwnProperty("fullName")); // true
// to check if instance has a method on its prototype chain
console.log(typeof person1.fullName==="function"); // true 
```


**Factory Function**
```js
function movie(title, year) {
  const movieObj = {
    title: title,
    year: year,
    getDetails() {
      console.log(
        `Title: ${this.title}
			 Year: ${this.year}
			`
      );
    },
  };
  return movieObj;
}

const movie1=movie("The Avengers",2012);
console.log(movie1);
movie1.getDetails();

const movie2=movie("Avatar",2015);
console.log(movie2);
movie2.getDetails();
```






```js
const arr = [1, 2, 3];
console.log(arr.constructor === Array); // true
```
- When you create an array literal `[]`, it’s actually an instance of the built-in **`Array`** class.
- Every object in JS has a `.constructor` property pointing to the function that created it (unless you mess with its prototype).
- For arrays, that’s the built-in `Array` constructor.




---
### Prototype Inheritance
https://www.geeksforgeeks.org/javascript/prototype-inheritance-in-javascript/

+ Constructor creates object.
+ Objects need a way to share methods and properties without duplicating them in memory. That’s where prototypes come in.
+ Every JavaScript object has an internal link to another object called its **prototype**.
+ If you try to access a property/method on the object and it doesn’t exist there, JavaScript automatically looks for it in the prototype. This forms a **prototype chain**.


```js
function Person(name){
	this.name=name;
}

Person.prototype.sayHello=function(){
	console.log(`Hi, I'm ${this.name}`);
};

const p1=new Person("Alice");
const p2=new Person("Bob");

p1.sayHello(); // Hi, I'm Alice
p2.sayHello(); // Hi, I'm Bob
```
+ `sayHello` lives once in `Person.prototype`
+ `p1` and `p2` don’t have their own copies — they _inherit_ it through the prototype chain.


##### Using `__proto__` (old but quick)

```js 
const animal={
	eats: true
}

const dog={
	barks: true
}

dog.__proto__=animal; // link dog to animal

console.log(dog); 
console.log(dog.eats); // true 
```


##### Using `Object.setPrototypeOf()` (modern)

```js
const animal={
	eats: true
}

const dog={
	barks: true
}

Object.setPrototypeOf(dog,animal); // link dog to animal

console.log(dog.eats); // true
```

##### Using `Object.create()`

```js
const animal={
	eats: true
}
// Create a new object with animal as its prototype
const dog=Object.create(animal);

dog.barks=true;

console.log(dog.eats);  // true (inherited from animal)
console.log(dog.barks); // true (own property)
```

- `__proto__`: Legacy way to set an existing object's prototype; mutable but discouraged.
- `Object.setPrototypeOf()`: Official method to set an existing object's prototype; safer and preferred over `__proto__`.
- `Object.create()`: Creates a new object with the specified prototype; cleaner and more explicit for inheritance.

---

TODO:
+ super keyword
+ Enum
+ User Input
+ Abstraction
+ Polymorphism
+ Interface

---
# ES6 Classes
- **Syntactic sugar** over JavaScript’s existing prototype-based inheritance.
- They provide a **clearer, more concise, and familiar syntax** for creating constructor functions and inheritance.
- Underneath, it’s still prototype-based — no magic objects.
- Classes are not hoisted.
- Classes get executed in strict mode only.

#### class declaration 

```js
class Person{
	constructor(name,age,){
		this.name=name;
		this.age=age;
	}
	
	greet(){
		return `Hello, I'm ${this.name} and I'm ${this.age} years old`;
	}
}

const p1=new Person("Amit",50);
console.log(p1.greet());
```


#### class expression

```js
// Named class expression
const Person=class PersonClass{
	constructor(name){
		this.name=name;
	}
	greet(){
		return `Hello, I'm ${this.name}`;
	}
};

const p1=new Person("Amit");
console.log(p1.greet());
```


#### Anonymous class expression

```js
const Car=class{
	constructor(brand){
		this.brand=brand;
	}
	drive(){
		return `${this.brand} is driving.`;
	}
};

const c1=new Car("Tesla");
console.log(c1.drive()); // Tesla is driving
```


### Static Method

```js
class MathHelper{
	static square(x){
		return x*x;	
	}
}

console.log(MathHelper.square(5)); // 25
// Can't call on instance: new MathHelper().square() -> error
```


#### Private Fields (ES2020 and beyond)

```js
class Counter {
  #count = 0; // private field

  increment() {
    this.#count++;
  }

  getCount() {
    return this.#count;
  }
}

const c = new Counter();
c.increment();
console.log(c.getCount()); // 1
// console.log(c.#count); // SyntaxError can not access private field
```


---
### Encapsulation
Wrapping data (properties) and methods that operate on that data into a single unit (an object or class) and **restricting direct access** to some of the object’s components.
```js
// Encapsulation example with private field
class Person{
	#age; // private field
	
	constructor(name,age){
		this.name=name; // public
		this.#age=age; // private
	}
	
	getAge(){
		return this.#age; // controlled access
	}
	
	setAge(newAge){
		if(newAge>0){
			this.#age=newAge;
		}else{
			console.log("Age must be positive");
		}
	}
}

const p1=new Person("Amrita",5);
console.log(p1.getAge());
p1.setAge(-10);
p1.setAge(10);
console.log(p1);

// Direct access is blocked:
//console.log(p.#age); // SyntaxError
```
we can even create private method too


#### Getter and Setter
Getters can return values that aren’t stored but are calculated on the fly.

```js
class Person {
	#_age; // private field
	
	constructor(name, age) {
		this.name = name;  // public
		this.age = age; // ✅ uses setter → applies validation
	}
	
	// Getter → runs when reading `person.age`
	get age() {
		return this.#_age;
	}

	// Setter → runs when assigning `person.age = value`
	set age(value) {
		if (value > 0 && value < 120) {
			this.#_age = value;
		} else {
			throw new Error("Invalid age");
		}
	}
}

const p = new Person("Amit", 25);

console.log(p.age);   // ✅ Getter → 25
p.age = 50;           // ✅ Setter → changes private field
console.log(p.age);   // 30

// Direct access is blocked:
// console.log(p.#_age); // ❌ SyntaxError
```


```js 
class Rectangle{
	constructor(width,height){
		this.width=width;
		this.height=height;
	}
	
	get area(){
		return this.width * this.height;
	}
}
const r=new Rectangle(10,5);
console.log(r.area); // 50
```
- There’s **no `area` property stored** anywhere on the object.
- When you write `r.area`, JS actually calls the `get area()` method behind the scenes, does the math, and returns the result.


---
### Inheritance

```js
class Person{
	constructor(name,age){
		this.name=name;
		this.age=age;
	}
	
	greet(){
		return `Hi, I'm ${this.name} and I'm ${this.age} years old.`;
	}
}

class Employee extends Person{
	constructor(name,age,jobTitle){
		super(name,age); // Calls person constructor
		this.jobTitle=jobTitle;
	}
	
	work(){
		return `${this.name} is working as a ${this.jobTitle}`;
	}
}

const p1=new Person("Amit",50);
console.log(p1.greet());

const emp1=new Employee("Bob",51,"Developer");
console.log(emp1.greet()); 
console.log(emp1.work()); 
```
- Use `extends` to inherit from another class.
- `super()` calls the parent class constructor.

+ In ES6 class inheritance, if a subclass has its own `constructor`, it **must** call `super()` **before** using `this`.


---
#### Built in classes
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects

TODO: 
- **Object** – base class for all objects (`Object.keys()`, `Object.assign()` etc.)
- **Array** – for ordered lists of data (`map`, `filter`, `reduce` etc.)
- **Map** – key–value pairs with any type of key (better than plain objects for some cases)
- **Set** – unique values collection
- **Date** – date & time manipulation
- **Error** (and its subclasses like `TypeError`, `ReferenceError`) – for handling exceptions
- **RegExp** – regular expressions for pattern matching
- **Promise** – async operation handling
- **Function** – base class for all functions



---

#### JSON (Javascript Object Notation)
https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/JSON

##### `JSON.stringify()`
- Converts a JavaScript value → JSON string
```js
const obj={name: "Amit", age: 25};
const jsonStr=JSON.stringify(obj);
console.log(jsonStr); // {"name":"Amit","age":25}
```

##### `JSON.parse()`
- Converts JSON string → JavaScript value
```js
const parsed=JSON.parse('{"name":"Amit","age":25}');
console.log(parsed.name); // Amit
console.log(typeof parsed.name); // string
```



---

# DOM Manipulation


pending week8 | topic2 | lec1



---

# Asynchronous JavaScript

+ JavaScript runs in a **single thread** — only one thing at a time.  
+ If you do something that takes a long time (e.g., network request, file reading), it’ll **block** everything else unless you use **asynchronous** code.

There are three main async patterns in JS

### Callbacks
+ Old-school, used before promises.
+ A callback is a function passed as an argument to another function

```js
function printMessage(){
	console.log("After 2 seconds");
}

setTimeout(printMessage,2000);
```


**Using async `setTimeout()`**
+ When using the JavaScript function `setTimeout()`, you can specify a `callback` function to be executed on time-out.
```js
console.log("Start");

setTimeout(()=>{
	console.log("After 2 seconds");
},2000);

console.log("End");

//Output:
//Start
//End
//After 2 seconds
```

**Pros:** Simple
**Cons:** Leads to callback hell if many async tasks depend on each other.


**Using async `setInterval()`**
+ When using the JavaScript function `setInterval()`, you can specify a `callback` function to be executed for each interval

```js
console.log("Start");
let count=0;
setInterval(()=>{
	console.log(count);
	count++;
},1000);

console.log("End");
```



TODO:
+ CallBack hell





---
### Promises
https://youtu.be/NJwRQgsu1Q8
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
https://www.w3schools.com/js/js_promise.asp

+ A Promise is basically an object representing a future value.
+ The **`Promise`** object represents the eventual completion (or failure) of an asynchronous operation and its resulting value.
+ A **Promise** is like a _placeholder_ for a value that you’ll get **later** (either success or failure).


**Syntax for promises to create and consume**
```js
let myPromise = new Promise((resolve, reject) => {
  let success = true; // pretend some work happens here
  
  setTimeout(() => { 
    if (success) {
      resolve("Task completed successfully");
    } else {
      reject("Oops, something went wrong");
    }
  }, 2000);
});

myPromise
  .then((result) => {
    console.log(result);
  })
  .catch((err) => {
    console.log(err);
  })
  .finally(() => {
    console.log("I will run irrespective of failure or success");
  });
```

- **`then()`** runs when resolved.
- **`catch()`** runs when rejected.
- **`finally()`** runs in both cases.

**Above code can also be written as** 
```js
new Promise((resolve, reject) => {
  let success = true; // pretend some work happens here
  setTimeout(() => {
    if (success) {
      resolve("Task completed successfully");
    } else {
      reject("Oops, something went wrong");
    }
  }, 1000);
})
  .then((result) => {
    console.log(result);
  })
  .catch((err) => {
    console.log(err);
  })
  .finally(() => {
    console.log("I will run irrespective of failure or success");
  });
```


**Instead of using `then` and `catch` we can also use `async` and `await` to consume promises**
```js
let myPromise=new Promise((resolve,reject)=>{
	let success=true;// pretend some work happens here
	
	setTimeout(()=>{
		if(succes){
			resolve("Task completed successfully");
		}else{
			reject("Oops, something went wrong");
		}
	},2000);
});

async function handlePromise(){
	try{
		const result=await myPromise;
		console.log(result);
	}catch(err){
		console.log(err);
	}finally{
		console.log("I will run irrespective of failure or success");
	}
}
```



---
### async/await



---
### `XMLHttpRequest` (old AJAX) 
+ is a built-in JavaScript object that lets your code talk to a server — sending and receiving data — without reloading the whole web page.
+ can work with JSON, HTML, or plain text 

Basic workflow:
- **Create** an `XMLHttpRequest` object.
- **Open** a request (`GET`, `POST`, etc.) with a URL.
- **Send** it.
- **Listen** for the server’s response.

```js
let req = new XMLHttpRequest();
req.open("GET", "https://api.example.com/data", true);
req.onload = function () {
  if (req.status === 200) {
    console.log(req.responseText);
  }
};
req.send();
```



#### User Card Project utilizing `XMLHttpRequest()`

```HTML
<!DOCTYPE html>
<html>
  <head>

    <style>
      body{
        margin: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
      }
      .card {
        border: 1px solid #ccc;
        padding: 10px;
        width: 200px;
        text-align: center;
      }
      .card img {
        width: 80px;
        height: 80px;
        border-radius: 50%;
      }
    </style>

  </head>
  <body>
    <div id="card"></div>

    <script>
      function fetchUser(id) {
        const req = new XMLHttpRequest();
        req.open("GET", `https://dummyjson.com/users/${id}`);
        req.addEventListener("load",()=>{
          if (req.status === 200) {
            const data = JSON.parse(req.responseText);
            document.getElementById("card").innerHTML = `<div class="card">
            <img src="${data.image}">
            <h3>${data.firstName} ${data.lastName}</h3>
            <p>${data.email}</p>
          </div>`;
          }
        req.send();
        });
      }
      fetchUser(Math.floor(Math.random()*30)+1);
    </script>

  </body>
</html>
```


---
### `fetch()` API (modern standard)
https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch
https://www.geeksforgeeks.org/javascript/javascript-fetch-method/
+ The Fetch API provides a JavaScript interface for making HTTP requests and processing the responses.
+ `fetch()` is promise based

**Basic Syntax**
```js
fetch(url, options)
  .then(response => response.json()) // convert response to JSON
  .then(data => console.log(data))   // do something with the data
  .catch(error => console.error(error));
```
- `url` → where to send the request
- `options` → optional config (method, headers, body, etc.)


**GET Request**
```js
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));
```
- Default method is `GET`
- Returns a `Promise`
- You must manually convert the response with `.json()` (or `.text()` / `.blob()`)


**POST request**
```js
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    title: 'foo',
    body: 'bar',
    userId: 1
  })
})
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));
```
- `method: 'POST'` → tells the server you’re sending data
- `headers` → tells the server the type of data
- `body` → your actual data (must be a string for JSON)


**Async/Await version (cleaner)**
```js
async function getPost() {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/posts/1');
    if (!res.ok) throw new Error(`HTTP Error: ${res.status}`);
    const data = await res.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

getPost();
```
- Easier to read than chained `.then()`


**PUT request**
```js
const updatedData = { id: 1, price: 300 };

fetch('https://fakestoreapi.com/products/1', {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(updatedData)
})
    .then(response => response.json())
    .then(result => console.log(result));
```


**DELETE request**
```js
fetch('https://fakestoreapi.com/products/1', {
    method: 'DELETE'
  })
    .then(response => response.json())
    .then(result => console.log('Deleted:', result));
```


Key Points
- `fetch` **does not** reject on HTTP errors (like 404) → you need to check `response.ok`.
- Can be used for **GET, POST, PUT, DELETE, etc.**
- Works in browsers and also in Node.js (v18+ has native `fetch`, else use `node-fetch`)



---
Microtasks vs Macrotasks




---
 week10 | topic1 | lec1


