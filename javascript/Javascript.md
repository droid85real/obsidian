Js is a 
+ interpreted
+ jit compiled
+ multi-paradigm
+ prototype based (allows the creation of an object without first defining its class)
+ synchronous
+ single threaded
+ dynamic language (no need to define data type)

# JavaScript Variable Declarations: `let`, `const`, `var`
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


# Ternary operator

`(condition) ? (true expression) : (false expression);`
```js
(num1>num2) ? (num1) : (num2===num1 ? "equal" : num2);
```
Above we checking, if `num1` is greater than `num2`, and if so, return `num1`. If `num1` and `num2` are equal, return `"equal"`. Otherwise, return `num2`


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

object creation using new keyword then adding properties
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
## 3. Adding/Updating Properties

javascript

CopyEdit

`let person = { name: "Bob", age: 35 };  // Adding a new property person.city = "New York";  // Updating an existing property person.age = 36;  console.log(person);  // { name: 'Bob', age: 36, city: 'New York' }`

---

## 4. Deleting Properties

Use the `delete` operator:

javascript

CopyEdit

`let person = { name: "Charlie", age: 40, city: "London" };  delete person.city;  console.log(person);  // { name: 'Charlie', age: 40 }`

---

## 5. Object Methods

An object can have **methods**, which are functions that belong to the object.

javascript

CopyEdit

``let car = {   make: "Toyota",   model: "Corolla",   year: 2020,   displayInfo: function() {     return `${this.year} ${this.make} ${this.model}`;   } };  console.log(car.displayInfo());  // Output: 2020 Toyota Corolla``

---

## 6. Object Destructuring

javascript

CopyEdit

`let person = { name: "Emma", age: 28 };  // Destructuring let { name, age } = person;  console.log(name);  // Output: Emma console.log(age);   // Output: 28`

### Renaming variables during destructuring:

javascript

CopyEdit

`let person = { name: "David", age: 30 };  // Renaming variables let { name: firstName, age: yearsOld } = person;  console.log(firstName);  // Output: David console.log(yearsOld);   // Output: 30`

---

## 7. Nested Objects

javascript

CopyEdit

`let user = {   name: "Jake",   address: {     street: "123 Main St",     city: "Los Angeles",     zip: "90001"   } };  console.log(user.address.city); // Output: Los Angeles`

---

## 8. The `this` Keyword

Inside an object method, `this` refers to the object itself.

javascript

CopyEdit

`let person = {   firstName: "Sophia",   lastName: "Lee",   fullName: function() {     return this.firstName + " " + this.lastName;   } };  console.log(person.fullName());  // Output: Sophia Lee`

---

Let me know if you want to expand this into more advanced topics like prototypes, classes, or object inheritance!

pgsql

CopyEdit

``You can paste this into a file named `javascript-objects.md` and it will render nicely in any Markdown viewer or editor (like VSCode, GitHub, Obsidian, etc.). Let me know if you want a downloadable version instead!``

