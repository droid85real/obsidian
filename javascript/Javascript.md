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

Quick Summary

| Feature       | `var`           | `let`       | `const`     |
| ------------- | --------------- | ----------- | ----------- |
| **Scope**     | Function        | Block       | Block       |
| **Hoisting**  | Yes (undefined) | Yes (TDZ\*) | Yes (TDZ\*) |
| **Redeclare** | Yes             | No          | No          |
| **Reassign**  | Yes             | Yes         | No          |

> \*TDZ = Temporal Dead Zone — accessing the variable before it's declared throws a `ReferenceError`.


###### ( && ) AND Operator 
+ first falsy and last truthy

###### ( || ) OR Operator
+ first truthy and last falsy

### Falsy Values in JavaScript

In JavaScript, **falsy values** are values that evaluate to `false` in a boolean context. These include:
- `false`
- `0`
- `-0`
+ `0n`
- `''` (empty string)
- `null`
- `undefined`
- `NaN` (not a number)
Any other value is considered **truthy**

---

Strict mode in JavaScript is a restricted version of JS that enforces cleaner coding rules and throws errors for unsafe or ambiguous behavior.

You enable it using:
```js
"use strict";
```

Key points (interview-ready):
- Prevents silent errors by throwing exceptions
- Disallows undeclared variables
- Stops duplicate parameter names in functions
- Restricts use of `this` (undefined in functions instead of global object)
- Makes debugging easier and code more secure
- Helps JS run in a more optimized way internally

Example:
```js
"use strict";

x = 10; // ❌ ReferenceError: x is not defined
```

Strict mode is a feature in JavaScript that enforces stricter parsing and error handling, helping catch bugs early and make code safer and more predictable.


---
### Type coercion
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


The easiest interview trick is to memorize **what each operator wants**.

|Operator|What it wants|Example|Result|
|---|---|---|---|
|`+`|Number **or** String|`1 + "2"`|`"12"` (concatenation)|
|`-`, `*`, `/`, `%`, `**`|**Only Number**|`"5" - 2`|`3`|
|`<`, `>`, `<=`, `>=`|Numbers (unless both are strings)|`"5" > 2`|`true`|
|`==`|Loose comparison (does type coercion)|`"5" == 5`|`true`|
|`===`|No coercion|`"5" === 5`|`false`|

### The conversion table (most asked in interviews)

|Value|`Number()`|`String()`|`Boolean()`|
|---|---|---|---|
|`undefined`|`NaN`|`"undefined"`|`false`|
|`null`|`0`|`"null"`|`false`|
|`true`|`1`|`"true"`|`true`|
|`false`|`0`|`"false"`|`false`|
|`""`|`0`|`""`|`false`|
|`"123"`|`123`|`"123"`|`true`|
|`"abc"`|`NaN`|`"abc"`|`true`|

 Interview trick (remember this)
- **`+` is greedy for strings.**
    - If **either operand is a string**, `+` concatenates.
    - Otherwise, it adds numbers.
- **Every other arithmetic operator (`- * / % **`) is greedy for numbers.**
    - It converts operands to numbers.
    - If conversion fails → `NaN`.

 Examples
```js
1 + "2"          // "12"
"5" - 2          // 3
"5" * "2"        // 10
undefined + 1    // NaN
undefined * 2    // NaN
null + 1         // 1
true + 2         // 3
```

**Only `+` can concatenate strings. All other arithmetic operators first convert operands to numbers. If that conversion fails, the result is usually `NaN`.**



---
# Data Types

Primitive
- Number
- String
- Boolean
- null
- undefined
- Symbol
- BigInt

Reference
- Object
- Array
- Function
- Date
- RegExp
- Map
- Set
- WeakMap
- WeakSet


### `undefined`
- A variable that has been declared but has not yet been assigned a value is `undefined`. It’s the default value of uninitialized variables.
- A function that doesn't return anything will implicitly return `undefined`.
- Accessing a non-existent property of an object or an array index that is out of bounds will return `undefined`.
- `typeof` undefined is `undefined`

### `null`
+ `null` is an explicit assignment that represents the intentional absence of any object value. It’s an object that represents "nothing" or "no value."
+ It's typically used when you want to explicitly indicate that a variable should be empty or has no value.
+ `typeof` null is object

>NOTE:
- **Loose equality (`==`)**: `undefined` and `null` are considered equal.
- **Strict equality (`===`)**: They are **not** the same.

```js
[] == []              // false     (different array objects)
[] === []             // false
{} == {}              // false     (different object references)
{} === {}             // false
```
Reason: different memory reference


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


### Map
+ A `Map` is a built-in collection that stores **key-value pairs** where **keys can be of any data type**.
- Maintains **insertion order**.

Syntax: `const map = new Map();`

Or with initial values:
```js
const map = new Map([
    ["name", "John"],
    ["age", 25],
    ["city", "Delhi"]
]);

console.log(map);
//Output:
// Map(3) {
//   'name' => 'John',
//   'age' => 25,
//   'city' => 'Delhi'
// }
```


```js
const map = new Map([
    ["key0", "value0"],
    ["key1", "value1"],
]);

console.log(map);
// Output:
// Map(2) {
//   'key0' => 'value0',
//   'key1' => 'value1'
// }

const arr = [...map];
console.log(arr);
// Output:
// [
//   ['key0', 'value0'],
//   ['key1', 'value1']
// ]

const keys = [...map.keys()];
console.log(keys);
// Output:
// ['key0', 'key1']

const values = [...map.values()];
console.log(values);
// Output:
// ['value0', 'value1']
```


| Method            | Description                    |
| ----------------- | ------------------------------ |
| `set(key, value)` | Add or update a key-value pair |
| `get(key)`        | Get value by key               |
| `has(key)`        | Check if key exists            |
| `delete(key)`     | Remove a key                   |
| `clear()`         | Remove all entries             |
| `size`            | Returns number of entries      |


`set(key, value)` - Add a new key-value pair
```js
map.set("key2", "value2");
console.log(map);
// Output:
// Map(3) {
//   'key0' => 'value0',
//   'key1' => 'value1',
//   'key2' => 'value2'
// }
```

`set(key, value)` - Update an existing key
```js
map.set("key1", "updatedValue1");
console.log(map);
// Output:
// Map(3) {
//   'key0' => 'value0',
//   'key1' => 'updatedValue1',
//   'key2' => 'value2'
// }
```

`get(key)` - Retrieve value by key
```js
console.log(map.get("key1"));
// Output:
// updatedValue1
```

`has(key)` - Check if key exists
```js
console.log(map.has("key2"));
// Output:
// true

console.log(map.has("key3"));
// Output:
// false
```

`size` - Number of key-value pairs
```js
console.log(map.size);
// Output:
// 3
```

`delete(key)` - Remove a key-value pair
```js
map.delete("key2");
console.log(map);
// Output:
// Map(2) {
//   'key0' => 'value0',
//   'key1' => 'updatedValue1'
// }
```

`clear()`- Remove all entries
```js
map.clear();
console.log(map);
// Output:
// Map(0) {}
```


| Feature           | Object                                                                                                                           | Map                                                                     |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| **Key Types**     | Only strings and symbols are valid keys                                                                                          | Any value can be used as a key (objects, functions, primitives)         |
| **Key Order**     | Keys are unordered (in practice, insertion order is mostly preserved for string keys, but not guaranteed)                        | Keys are ordered by insertion; iteration follows insertion order        |
| **Size Property** | No built-in way to get the number of keys; must use `Object.keys(obj).length`                                                    | Use the `.size` property for the number of entries                      |
| **Iterability**   | Not directly iterable; must use `Object.keys`, `Object.values`, or `Object.entries`                                              | Directly iterable with `for...of`, `.keys()`, `.values()`, `.entries()` |
| **Prototype**     | Has a prototype chain; may have default properties that can collide with custom keys (can be avoided with `Object.create(null)`) | Does not have a prototype, so there are no default keys                 |
| **Performance**   | May be less efficient for frequent additions/removals                                                                            | Optimized for frequent additions and deletions                          |
| **Serialization** | Can be easily serialized to JSON                                                                                                 | Cannot be directly serialized to JSON                                   |



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



###### **Anonymous Function**
+ Used when you don’t need to name a function, often as an argument:
```js
setTimeout(function() {
  console.log("This runs after 1 second");
}, 1000);
```

###### **Immediately Invoked Function Expression (IIFE)**
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


###### Generator Function
Think of a **generator** as a function that **doesn't run all at once**. It runs a little, stops, remembers where it stopped, and continues later when you ask it to.

Before generators, a normal function behaves like this:

```js
function greet() {
  console.log("Hello");
  console.log("World");
}
greet();
// Output:
// Hello
// World
```
The function starts from the top and runs until the end. **You cannot pause it in the middle.**


What changes with a generator?

A generator is declared with `function*`.
```js
function* greet() {
  console.log("Hello");
  yield;
  console.log("World");
}
```

Notice two new things:
- `function*`
- `yield`

When you call it:
```js
const gen = greet();
console.log(gen);
```

It doesn't print anything.

Why?
Because calling a generator **does not execute its code.**
Instead, it returns a **generator object**.

Think of it like this:
```
function* greet() {
   ...
}

↓ call

const gen = greet();

gen =
┌──────────────────────┐
│ paused function      │
│ ready to execute     │
└──────────────────────┘
```
Nothing inside has run yet.

What does `next()` do?

`next()` tells the generator:
"Start (or continue) executing until you hit a `yield`."

Example:
```js
function* greet() {
  console.log("Hello");
  yield;
  console.log("World");
}
const gen = greet();
gen.next();
```

Execution:
```
Start

console.log("Hello")
↓

Hello

yield
↓
PAUSE
```

Output:
```
Hello
```

Notice that `"World"` wasn't printed.
The function literally stopped at `yield`.

Call `next()` again
```js
gen.next();
```

Now execution resumes **right after the previous `yield`.**
```
yield
↓
console.log("World")
↓
End
```

Output:
```
World
```
Now the generator has finished.


What if `yield` returns a value?

Your example:
```js
function* generator(i) {
  yield i;
  yield i * 2;
}

const gen = generator(10);
```

Again:
```
generator(10)
```
does **not** execute the function.

It only creates:
- gen
- paused generator

First `next()`
```js
gen.next();
```

Execution:
```
function* generator(i) {
yield i;
```

`i` is `10`.
So
```
yield 10
```

`yield` does two things:
1. returns `10`
2. pauses the function

So
```js
gen.next()
```

returns
```js
{
  value: 10,
  done: false
}
```

because it paused—not finished.
```
console.log(gen.next().value);
```

prints
```
10
```

The generator is now paused here:
```
yield i;
      ^
```


Second `next()`
```js
gen.next();
```

Execution resumes after the first `yield`.
```
yield i;
↓
yield i * 2;
```

Now
```
10 * 2 = 20
```

So it returns
```js
{
  value: 20,
  done: false
}
// Output:
// 20
```
Again, it pauses.

Third `next()`
```js
gen.next();
```

There is nothing left.
So the function ends.

It returns
```js
{
  value: undefined,
  done: true
}
```
`done: true` means
"The generator has completely finished."


**Why are generators useful?**
Imagine reading a huge file with **10 million lines**.
Without generators: All 10 million lines are loaded into memory before you process them.

Notes to remember
- `function*` → Defines a generator function.
- Calling a generator **does not execute it**; it returns a generator object.
- `yield` → Returns a value **and pauses** execution.
- `next()` → Starts or resumes execution until the next `yield` (or the end).
- `next()` returns an object:

```js
{
  value: <yielded value>,
  done: <true if finished, otherwise false>
}
```
- Unlike `return`, a generator can produce **multiple values** over time.


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
+ make changes to original array and return the removed elements

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


|`slice()`|`splice()`|
|---|---|
|Does **not** modify the original array (immutable)|Modifies the original array (mutable)|
|Returns a **shallow copy** (subset) of selected elements|Returns an array of the **removed** elements|
|Used to **extract** elements from an array|Used to **add**, **remove**, or **replace** elements in an array|
|Syntax: `array.slice(start, end)`|Syntax: `array.splice(start, deleteCount, ...items)`|

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
### Object

###### Object Creation
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

console.log(student.name); // Alexa
console.log(student["name"]); // Alexa
console.log(student[100]); // hundred
student.show(); // This is the student details section

console.log(student);
// {
//   '100': 'hundred',
//   name: 'Alexa',
//   age: 10,
//   hobby: 'Dancing',
//   show: [Function: show]
// }
```

###### object creation using new keyword then adding properties
```js
const person=new Object(); // creates an object

person.firstName="John";
person.lastName="Doe";
person.age=50;

console.log(person); //Output: { firstName: 'John', lastName: 'Doe', age: 50 }
```

###### Adding/Updating Properties
```js
let person = { name: "Bob", age: 35 };  // Adding a new property 
person.city = "New York";  // Updating an existing property 
person.age = 36;  
console.log(person);  // { name: 'Bob', age: 36, city: 'New York' }
```


```js
const property = "firstName";
const name = "Piyush Agarwal";

const user = {
	[property]: name,
};
console.log(user.firstName);
```

###### Deleting Properties
Use the `delete` operator:
```js
let person = { name: "Charlie", age: 40, city: "London" };
delete person.city;
console.log(person); // { name: 'Charlie', age: 40 }
```

###### Object Methods
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

###### Accessing value using dot notation
```js
const user = {
  name: "Alice",
  age: 25,
  city: "Delhi"
};

console.log(user.name); // Alice
console.log(user.age);  // 25
```

###### Access a value using bracket notation
```js
const user = {
  name: "Alice",
  age: 25
};

console.log(user["name"]); // Alice

const key = "age";
console.log(user[key]); // 25
```

| Method                | Returns                       |
| --------------------- | ----------------------------- |
| `Object.keys(obj)`    | Array of keys                 |
| `Object.values(obj)`  | Array of values               |
| `Object.entries(obj)` | Array of `[key, value]` pairs |
###### Get all keys
```js
const user = {
	name: "Alice",
	age: 25,
	city: "Delhi",
};
const keys = Object.keys(user);
console.log(keys); // ["name", "age", "city"]
```

###### Get all values
```js
const user = {
	name: "Alice",
	age: 25,
	city: "Delhi",
};
const values = Object.values(user);
console.log(values);// ["Alice", 25, "Delhi"]
```

###### Get both keys and values
```js
const user = {
	name: "Alice",
	age: 25,
	city: "Delhi",
};
const entries = Object.entries(user);
console.log(entries);
// [
//   ["name", "Alice"],
//   ["age", 25],
//   ["city", "Delhi"]
// ]
```

###### Using `for...in`
```js
for (const key in user) {
  console.log(key, user[key]);
}
// name Alice
// age 25
// city Delhi
```

###### Object Destructuring
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

###### Renaming variables during destructuring:
```js
const person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 30
};

const { firstName: fName, lastName: lName } = person;

console.log(fName); // John
console.log(lName); // Doe
```

###### Destructuring as an assignment pattern
Just like arrays, you can destructure in assignments (not just declarations):
```js
const person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 30
};

let fName, lName;

({ firstName: fName, lastName: lName } = person);

console.log(fName); // John
console.log(lName); // Doe
```
The parentheses `()` are necessary to tell JS this is an expression, not a block.

###### Default Value 
```js
const person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 30
};
const { middleName = "N/A" } = person;

console.log(middleName);  // N/A
```
Here, `middleName = "N/A"` means:  
If `middleName` doesn’t exist or is `undefined`, assign `"N/A"` instead.

###### Nested Objects
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

###### Nested Object Destructuring
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

###### `this` Keyword in object method
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



TODO: length,split,hasownproperty
week6,topic3,lec44


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

The preferred modern approach is `structuredClone()`, which deep clones most built-in JavaScript data structures and supports circular references. 
```js
const obj = {
    name: "John",
    address: {
        city: "Delhi"
    }
};

const clone = structuredClone(obj);

clone.address.city = "Mumbai";

console.log(obj);
console.log(clone);
// Output:
// { name: 'John', address: { city: 'Delhi' } }
// { name: 'John', address: { city: 'Mumbai' } }
```

For simple JSON-compatible objects, `JSON.parse(JSON.stringify(obj))` works but loses types like `Date`, `Map`, `Set`, `undefined`, and functions. 
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

###### **Execution Contexts** 
- https://youtu.be/zdGfo6I1yrA
- https://youtu.be/ZvbzSrg0afE?list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP

An Execution Context (EC) is the environment in which JavaScript code is executed.
It contains:
- Variable environment (variables, functions)
- Scope chain (lexical scope access)
- `this` binding

Types of Execution Context
1. Global Execution Context (GEC)
- Created when JS file starts executing
- One per program
- `this` points to:
    - `window` (browser)
    - `global` (Node.js)

2. Function Execution Context (FEC)
- Created whenever a function is called
- One per function call
- Has its own:
    - local variables
    - arguments object
    - `this`


**Execution Context Phases**
Every execution context is created in **2 phases**:

1. Memory Creation Phase (Hoisting phase)
JS scans the code and allocates memory:
- `var` → initialized as `undefined`
- `let` / `const` → declared but in **Temporal Dead Zone (TDZ)**
- function declarations → fully stored in memory

Example:
```js
console.log(a); // undefined
var a = 10;

console.log(b); // ReferenceError (TDZ)
let b = 20;

foo(); // works

function foo() {
  console.log("hello");
}
```

2. Execution Phase
Code runs line by line:
- variables assigned real values
- functions executed
- expressions evaluated



JavaScript allocates memory for variables and functions during the creation phase of the execution context, before executing the code.

**Execution Context creation in action**

Example
```js
var x = 1;

function foo() {
  var y = 2;
  console.log(x + y);
}

foo();
```

What happens
Global creation phase
```
x → undefined
foo → function
```

Global execution
```
x → 1
foo() → new execution context
```

foo creation
`y → undefined`

**foo execution**
`y → 2 console.log(3)`

Then `foo` context is popped.



**Each function call = a sealed memory box**
Every time a function is invoked, JS creates a **new execution context** with:
- its own variable environment
- its own `x`, even if the name matches something outside

```js
var x = 1;
a();
b();
console.log(x);

function a() {
  var x = 10;
  console.log(x);
}

function b() {
  var x = 100;
  console.log(x);
}
```

Output:
10
100
1

Why this is inevitable:
- `a` gets its **own `x`**
- `b` gets its **own `x`**
- global `x` is untouched


Call stack controls _where_ code runs, not _what_ memory exists
The stack only decides **which execution context is active**.

Stack timeline
```
Start        → [Global]
a() called   → [Global, a]
a() ends     → [Global]
b() called   → [Global, b]
b() ends     → [Global]
Program end  → []
```

When a context pops:
- its **local variables are gone**
- unless captured by a closure (important later)



**Variable lookup rule**
When JS sees `x`, it does this:
1. Check current execution context
2. If not found → check outer context(parent)
3. Repeat until global
4. If still not found → ReferenceError
```js
var x = 5;

function test() {
  console.log(x);
}

test(); // 5
```
`test` has no `x`, so lookup climbs outward.



**Why functions don’t overwrite globals by accident**
```js
var count = 0;

function increment() {
  var count = 10;
}

increment();
console.log(count); // 0
```
Reason:
- `var count` inside `increment` creates **new memory**
- no mutation of outer scope happens
Isolation is the default, not the exception.



**When global does change**
Only if you explicitly target it.
```js
var x = 1;

function change() {
  x = 99; // no local var
}

change();
console.log(x); // 99
```
Now lookup finds:
- no local `x`
- outer `x` exists → mutate it


`setTimeout`
 https://youtu.be/eBTBG4nda2A?si=SNw6liELHt-BfE4l

```js
console.log("start");

setTimeout(() => {
  console.log("timer");
}, 1000);

console.log("end");

// output
// start
// end
//timer
```
Actual sequence inside the engine:
1. `"start"` → Call Stack → executed
2. `setTimeout` → callback registered with Web APIs + timer
3. JS **moves on immediately**
4. `"end"` → Call Stack → executed
5. After 1s → callback pushed to **Task Queue**
6. Event Loop checks: stack empty → moves callback to stack


**In depth understanding of the above code**

First: What an Execution Context Actually Contains
Every execution context has three main components:
1. Variable Environment
2. Lexical Environment
3. This binding

In modern engines, Variable Environment and Lexical Environment are very similar. For global scope, they both point to the global environment record.


Now let’s build your Global Execution Context step by step.

PHASE 1 — Creation Phase
JS scans the code before running it.
In your code:
- No `var`
- No `let`
- No `const`
- No function declarations

So what gets stored?
Practically nothing from your code.

But the GEC still contains:
Lexical Environment:
- Outer reference → null (because global has no outer scope)
- Environment Record → empty (for your script)

Variable Environment:
- Same as above (empty for this code)

This Binding:
- In browser → `window`
- In Node → `global`

So internally it looks like:

Global Execution Context  
{  
LexicalEnvironment: {  
EnvironmentRecord: { },  
Outer: null  
},  
VariableEnvironment: {  
EnvironmentRecord: { },  
Outer: null  
},  
ThisBinding: window  
}
Your script adds no variables, so the environment record stays empty.



**Whole process behind the scene for the code**

```js
console.log("start");

setTimeout(() => {
  console.log("timer");
}, 1000);

console.log("end");
```
We assume browser environment.

STEP 0 — Script Loads

JS engine receives the file.
It creates:
**Global Execution Context (GEC)**

As you understood:
```
GEC = {
  LexicalEnvironment: { empty },
  VariableEnvironment: { empty },
  ThisBinding: window
}
```
Then:

**GEC is pushed to Call Stack**
Stack:
```
[ Global EC ]
```


**STEP 1 — Creation Phase of GEC**
Engine scans entire script.
Finds:
- No var
- No let
- No const
- No function declarations
So environment records remain empty.
Creation phase ends.
Now execution phase begins.

**STEP 2 — Execution Phase (Line by Line)**
We now execute code top to bottom.

LINE 1
```js
console.log("start");
```
What happens internally:
1. Engine resolves identifier `console`
    - Not in local env
    - Found on global object (window.console)
2. Resolves `log`
3. Calls `console.log`

A new Execution Context is created for `log`.

Stack:
```
[ console.log EC ]
[ Global EC     ]
```

`console.log` executes native code → prints:
```
start
```
Then:
`console.log EC` is popped.

Stack:
```
[ Global EC ]
```

LINE 2
```js
setTimeout(() => {
  console.log("timer");
}, 1000);
```
Now slow down. This is where people hallucinate.

Step A — Resolve setTimeout
- Not in script env
- Found on `window.setTimeout`

Step B — Arrow Function Creation
Before `setTimeout` runs, the arrow function is created as a function object in memory (heap).

Important:  
It closes over current lexical environment (Global EC).  
In this case, nothing interesting is captured.

So we now have:
```
callbackFunction → stored in heap
```

Step C — Call setTimeout
A new Execution Context is created for `setTimeout`.

Stack:
```
[ setTimeout EC ]
[ Global EC     ]
```

Now critical understanding:
`setTimeout` is **not implemented inside JS engine**.

It is a Web API provided by the browser.

Inside `setTimeout`:
1. The callback reference is passed to Web APIs.
2. Timer of 1000ms is started in browser timer system.
3. Browser stores something like:
```
TimerRecord {
  callback: reference_to_arrow_function,
  delay: 1000ms
}
```
Then `setTimeout` returns immediately.
No waiting happens here.

Step D — setTimeout finishes
`setTimeout EC` popped.

Stack:
```
[ Global EC ]
```
JS moves forward instantly.


LINE 3
```js
console.log("end");
```
Same process as before:

Push console.log EC:
```
[ console.log EC ]
[ Global EC     ]
```

Prints:
```
end
```
Pop console.log EC.

Stack:
```
[ Global EC ]
```


**STEP 3 — Script Finishes**

No more synchronous code.
Global Execution Context completes.

It is popped.

Stack:
```
(empty)
```
Now JS engine is idle.


**Meanwhile — Outside the JS Engine**

Inside browser Web APIs:
Timer is counting down 1000ms.

JS engine does nothing about it.

After ~1000ms:
Browser timer system finishes.
Now it does NOT execute the callback directly.

Instead:
It pushes the callback reference into:

**Task Queue (Macrotask Queue)**

Queue:
```
[ callback ]
```
Still not executed.


**STEP 4 — Event Loop**
The Event Loop constantly runs this algorithm:
```
while(true) {
  if (CallStack is empty) {
    move first task from TaskQueue to CallStack
  }
}
```
At this moment:

Call Stack:
```
(empty)
```

Task Queue:
```
[ callback ]
```
Condition satisfied.

So:
Callback is moved from Task Queue → Call Stack.


**STEP 5 — Callback Execution**

Stack:
```
[ callback EC ]
```

Now inside callback:
```js
console.log("timer");
```

New Execution Context for console.log:
```
[ console.log EC ]
[ callback EC    ]
```

Prints:
```
timer
```

Then:
Pop console.log EC.  
Pop callback EC.

Stack:
```
(empty)
```
Execution complete.

Final Output Order
```
start
end
timer
```


**Important Precision Points (Interview Gold)**
- setTimeout does NOT wait. It registers and exits.
- Timer countdown happens outside JS engine.
- Callback goes to Task Queue, not Call Stack.
- Event Loop moves tasks only when stack is empty.
- 1000ms is minimum delay, not guaranteed exact execution time.

If stack were busy for 5 seconds,  
timer would run after 5 seconds.


**Full Ordered Timeline (Condensed)**
1. GEC created
2. GEC pushed to stack
3. Creation phase runs
4. console.log("start") executes
5. Arrow function created
6. setTimeout registers callback in Web APIs
7. console.log("end") executes
8. GEC popped
9. Timer completes in Web APIs
10. Callback pushed to Task Queue
11. Event Loop sees empty stack
12. Callback pushed to stack
13. console.log("timer") executes
14. Stack empty again


---
###### **Hoisting** 
means: **declarations are processed before code execution**, but **initializations are not**.

JavaScript runs in two phases:
1. **Creation phase** – memory is allocated
2. **Execution phase** – code runs line by line

During creation, the engine scans the code and “lifts” certain declarations into memory. That lifting illusion is called _hoisting_.
**Hoisting** in JavaScript is the behavior where few declarations are processed before the code executes.

`var` hoisting (the dangerous one)
```js
console.log(a);   // undefined
var a = 10;
console.log(a);   // 10
```

What the engine actually does:
```js
// Creation phase
var a;           // initialized as undefined

// Execution phase
console.log(a);  // undefined
a = 10;
console.log(a);  // 10
```

**Key facts**
- `var` is hoisted
- Initialized to `undefined`
- No error → this hides bugs
- Function-scoped, not block-scoped
 
 
 `let` and `const` hoisting (but with a trap)

Yes, they **are hoisted**, but **not initialized**.
```js
console.log(b);   // ❌ ReferenceError
let b = 20;
```

Why?
Because of the **Temporal Dead Zone (TDZ)**  
The time between the start of the scope and the declaration.
```js
// Creation phase
// b exists but is uninitialized (TDZ)

// Execution phase
console.log(b); // ❌ cannot access before initialization
let b = 20;
```

Same for `const`:
```js
console.log(c);  // ❌ ReferenceError
const c = 30;
```

Key facts
- Hoisted ✔️
- Accessible before declaration ❌
- Forces safer coding

---

**Function Declaration hoisting (fully hoisted)**
```js
sayHello();   // works

function sayHello() {
  console.log("Hello");
}
```

What happens:
```js
// Creation phase
function sayHello() { ... }

// Execution phase
sayHello();
```

Key facts
- Entire function is hoisted
- Can be called before definition
- Safest form of function

---

**Function Expression hoisting (depends on variable type)**

Using `var`
```js
sayHi();   // ❌ TypeError

var sayHi = function () {
  console.log("Hi");
};
```

Why?
```js
var sayHi;     // hoisted as undefined
sayHi();       // undefined is not a function ❌
```
Since sayHi is undefined at the time of the call, you get: TypeError: sayHello is not a function


Using `let`
```js
sayHey();   // ❌ ReferenceError

let sayHey = function () {
  console.log("Hey");
};
```
Key facts
- Variable hoisting rules apply
- Function body is NOT hoisted



**Arrow functions (same rule as function expressions)**
Arrow functions are **never hoisted as functions**.
```js
greet();   // ❌ ReferenceError

const greet = () => {
  console.log("Hello");
};
```



**Interview-level summary (write this in notes)**
```
Hoisting = JS behavior where declarations are moved to the top of their scope
during the memory creation phase.

var     → hoisted, initialized to undefined
let     → hoisted, in Temporal Dead Zone
const   → hoisted, in Temporal Dead Zone

Function Declaration → fully hoisted
Function Expression  → hoisted like variables
Arrow Function       → hoisted like variables
```

**Q:** “Are `let` and `const` hoisted?”  
**A:** “Yes, but they are not initialized and stay in the Temporal Dead Zone until execution reaches their declaration.”



`undefined` vs `not defined` (this matters in debugging)

`undefined`
Memory exists, value doesn’t (yet).
```js
var x;
console.log(x); // undefined
```

`not defined`
No memory, no binding, nothing.
```js
console.log(y); // ReferenceError
```

Rule:
- `undefined` → declared, not assigned
- `ReferenceError` → never existed in scope chain


---

###### **Call stack**
Call Stack = execution order, not memory
The call stack only tracks which execution context is running.

The **Call Stack** is a **LIFO (Last In, First Out) data structure** that keeps track of **which function is currently running** and **where the program should return after a function finishes**.

JavaScript is **single-threaded**.  
That means **one call stack, one thing at a time**. No parallel execution on the main thread.
```js
function a() {
  b();
}

function b() {
  console.log("Inside b");
}

a();
```

Call stack flow
When `b` finishes, its context is destroyed.  
When `a` finishes, its context is destroyed.  
Global stays until script ends.

Basic rule
- Function call → **push** onto stack
- Function return → **pop** from stack


Example: Nested calls
```js
function a() {
  b();
  console.log("a");
}

function b() {
  c();
  console.log("b");
}

function c() {
  console.log("c");
}

a();
```

Execution order (via call stack)
1. `a()` pushed
2. `b()` pushed
3. `c()` pushed
4. `c()` finishes → pop
5. `b()` finishes → pop
6. `a()` finishes → pop

Output
c
b
a

Example: async web api (setTimeout)
```js
console.log("start");

setTimeout(() => {
  console.log("timeout");
}, 0);

console.log("end");
```

Output
start
end
timeout

Why?
- `setTimeout` does **NOT** go on call stack
- Callback waits in **task queue**
- Stack must be empty first

---

###### 06: https://youtu.be/QCRpVw2KXf8?si=lTAnImyVK0Ur20X2

**Shortest js code**: empty js program with no lines of code
still causes the engine to create:
- Global Execution Context (GEC)
- Global object
- `this`

You can verify indirectly because this works **without writing anything else**:
`console.log(this);`
Something exists, so something was created.


###### Global Execution Context (what it really is)
The GEC is created **once per script** and contains:
- Global memory (variables + functions)
- Execution thread
- A reference to the global object
- A binding for `this`
No GEC → no program.


**`this` at global level (browser)**
At global scope: `console.log(this === window); // true`
Because during GEC creation: `this → global object`

This is **not true everywhere** (Node behaves differently), but in browsers this rule holds.


**what “global space” actually means**

Global space = **not inside any function**.
```js
var a = 10;
function test() {}
```

Behind the scenes (browser):
```js
window.a === 10        // true
window.test === test  // true
```
Both are properties of `window`.


Only **`var` and function declarations** attach to `window`.
```js
let a = 10;
const b = 20;

console.log(window.a); // undefined
console.log(window.b); // undefined
```
But
```js
var c = 30;
console.log(window.c); // 30
```
So:
- `var` → global object property
- `let` / `const` → global lexical environment (not on `window`)

Same scope, different storage.


---

###### undefined vs not defined
https://youtu.be/B7iF6G3EyIk?si=So0qiHcPeAkBblic

`undefined`
Memory exists, value doesn’t (yet).
```js
var x;
console.log(x); // undefined
```

`not defined`
No memory, no binding, nothing.
```js
console.log(y); // ReferenceError
```

Rule:
- `undefined` → declared, not assigned
- `ReferenceError` → never existed in scope chain


JavaScript is loosely typed
A variable is just a **label**, not a box with a fixed shape.
```js
var data;

data = 10;
data = "hello";
data = true;
```
JS doesn’t care. The engine just swaps what the label points to. 


**Why assigning `undefined` yourself is a bad idea**
`var a = undefined;`

This tells future readers **nothing**:
- Is it uninitialized?
- Was it intentionally cleared?
- Is it a bug?

If you mean “no value”, be explicit:
`var a = null;`

Rule:
- `undefined` → engine’s job
- `null` → developer’s intent


**Correct way to check for uninitialized variables**
```js
var a;

if (a === undefined) {
  console.log("a is uninitialized");
}

// Never rely on truthy/falsy for this:
if (!a) { } // WRONG — fails for 0, "", false
```


---
###### Scope chain
https://youtu.be/uH-tVP8MUs8?si=2zWWbOLqbt_P6t69

Scope = where a variable is accessible.
Scope Chain = the mechanism JavaScript uses to resolve variables by searching outward through nested scopes.

JS uses Lexical Scoping.

**When JS cannot find a variable in the current scope, it looks:**
1. Current scope
2. Outer scope
3. Outer’s outer scope
4. Global scope
5. If still not found → `ReferenceError`
That search path is the **scope chain**.


**“Lexical” means written location, not call order**
```js
function a() {
  function c() {
    console.log("inside c");
  }
}
```
Here:
- `c` is lexically inside `a`
- `a` is lexically inside global

This relationship is fixed at **parse time**.  
Calling order does **not** change scope.


**Lexical Environment = local memory + parent environment**

Every execution context creates this structure:
```
Lexical Environment
├── Local Memory (variables, functions)
└── Outer Reference → parent environment
```



Example01: basic scope chain
```js
let globalVar = "I am global";

function outer() {
  let outerVar = "I am outer";

  function inner() {
    let innerVar = "I am inner";

    console.log(innerVar);   // found in inner
    console.log(outerVar);   // found in outer
    console.log(globalVar);  // found in global
  }

  inner();
}

outer();
```
How resolution works inside `inner()`
When JS sees `outerVar`:
- Not in `inner`
- Looks in `outer`
- Found ✔
When JS sees `globalVar`:
- Not in `inner`
- Not in `outer`
- Found in global ✔
That upward search is the **scope chain traversal**.


Example02: Not found
```js
function a() {
  var x = 5;
}

a();
console.log(x); // ReferenceError
```
Why:
- global scope has no access to `a`’s local memory
- scope chain only points **upward**, never down
Children know parents. Parents don’t know children.


Example03: Variable Shadowing
```js
let x = 10;

function test() {
  let x = 20;
  console.log(x);
}

test(); //20
```
Why?
Because JS finds x in the nearest scope first.
Outer x = 10 is shadowed.


Example04: Lexical Scope vs Call Location (closure)
```js
let x = 100;

function outer() {
  let x = 200;

  function inner() {
    console.log(x);
  }

  return inner;
}

let fn = outer();
fn(); //200
```
Even though fn() is called in global scope,
it remembers where it was defined.
That’s lexical scoping.
Scope is determined at definition time, not call time.


Example05: Lexical scope ≠ dynamic scope
```js
function outer() {
  var x = 1;
  inner();
}

function inner() {
  console.log(x);
}

outer(); // ReferenceError
```
Why this fails:
- `inner` is lexically inside **global**, not `outer`
- call site does not matter
- declaration site does
Scope is **lexical, not runtime-based**.


**Browser devtools prove this**
Pause inside a function and check:
- Call Stack → execution order
- Scope panel → lexical environments

If you see “Closure”:
- that environment is being preserved
- memory wasn’t deleted
- reference still exists
- Closures are just surviving lexical environments.


Example05: Block Scope (let and const)
```js
{
  let a = 10;
  const b = 20;
  var c = 30;
}

console.log(a); // ❌ ReferenceError
console.log(b); // ❌ ReferenceError
console.log(c); // 30
```
Why?
- `let` and `const` are block scoped
- `var` is function scoped
Scope chain respects those rules.

---
###### let, const, TDZ (temporal dead zone)
https://youtu.be/BNC6slYCj50?si=tgtiZddM6FGAM9Yb

`let` / `const` _are_ hoisted but not initialized
They **exist in memory** before execution, but the engine marks them as **unusable**.
```js
console.log(a); // undefined
var a = 10;
```
vs
```js
console.log(b); // ReferenceError
let b = 10;
```
Key difference: Same hoisting. Different initialization rules.
- `var` → initialized with `undefined`
- `let` / `const` → **uninitialized**


**Temporal Dead Zone (TDZ)**
TDZ is not a place. It’s a **time window**.
TDZ occurs when you try to access variable before initialisation (let and const)

The **Temporal Dead Zone** is the **time window in a scope where a `let` or `const` variable exists but cannot be accessed**.

It starts: at the **beginning of the scope**
It ends: when the **variable is declared and initialized**

Any access during this window → **ReferenceError**.


Example01:
```js
console.log(a); // ❌ ReferenceError
let a = 10;
```
What happens internally:
```js
// Creation phase
// a is hoisted but uninitialized (TDZ)

// Execution phase
console.log(a); // ❌ access before initialization
let a = 10;     // TDZ ends here
```


Example02: TDZ vs var
```js
console.log(x); // undefined
var x = 5;
```
`var`:
- hoisted
- initialized to `undefined`
- no TDZ

`let` / `const`:
- hoisted
- NOT initialized
- TDZ applies


Example03: TDZ with `let` inside function
```js
let x = 10;

function test() {
  console.log(x); // ❌ ReferenceError
  let x = 20;
}

test();
```
Why?
Because:
- `x` inside `test` **shadows** the outer `x`
- The inner `x` is in TDZ until its declaration
- JS never reaches the global `x`


Example04: TDZ with `const` inside function
```js
const y = 5;

{
  console.log(y); // ❌ ReferenceError
  const y = 10;
}
```


Example05: TDZ with default parameters
```js
function demo(a = b, b = 10) {
  console.log(a);
}

demo(); // ❌ ReferenceError
```
Why?
Default parameters are evaluated **left to right**.
- `a = b` tries to access `b`
- `b` is still in TDZ



**Error types**

`ReferenceError`
```js
console.log(a); // TDZ or not defined
let a = 10;
```

`SyntaxError`
```js
let a = 1;
let a = 2; // duplicate declaration

const x; // missing initializer
```

`TypeError`
```js
const y = 5;
y = 6; // reassignment
```


---
###### Redeclaration of variable

Redeclaration of variable is only possible with  the `var` keyword. 

| Original | Redeclare with `var` | Redeclare with `let` | Redeclare with `const` |
| -------- | -------------------- | -------------------- | ---------------------- |
| `var`    | ✅ Allowed            | ❌ SyntaxError        | ❌ SyntaxError          |
| `let`    | ❌ SyntaxError        | ❌ SyntaxError        | ❌ SyntaxError          |
| `const`  | ❌ SyntaxError        | ❌ SyntaxError        | ❌ SyntaxError          |

`var` **can be redeclared**
```js
var x = 10;
var x = 20; // ✅ allowed
```

- `var` is **function-scoped**
- Redeclaring the same variable with `var` does **not** cause an error

`let` **cannot be redeclared in the same scope**
```js
let y = 10;
let y = 20; // ❌ SyntaxError: Identifier 'y' has already been declared
```
- `let` is **block-scoped**
- Redeclaration in the same scope is not allowed

Mixing `var` and `let` causes an error
```js
let a = 10;
var a = 20; // ❌ SyntaxError
```

```js
var b = 10;
let b = 20; // ❌ SyntaxError
```

✔️ This happens because `let` creates a **lexical binding**, and JavaScript does not allow another declaration of the same identifier in the same scope, regardless of keyword.


**Rules for `const` in JavaScript**

`const` **cannot be redeclared**
```js
const x = 10;
const x = 20; // ❌ SyntaxError: Identifier 'x' has already been declared
```

`const` **cannot be redeclared with `var` or `let`**
```js
const a = 10;
var a = 20; // ❌ SyntaxError
```

```js
const b = 10;
let b = 20; // ❌ SyntaxError
```

`const` **must be initialized**
```js
const c; // ❌ SyntaxError: Missing initializer in const declaration
```

`const` **cannot be reassigned**
```js
const d = 10;
d = 20; // ❌ TypeError: Assignment to constant variable
```
⚠️ Note: This applies to the **binding**, not the value itself.

Objects and arrays declared with `const` can be mutated
```js
const obj = { name: "JS" };
obj.name = "JavaScript"; // ✅ allowed
```

```js
const arr = [1, 2, 3];
arr.push(4); // ✅ allowed
```

But reassigning is not:
```js
arr = []; // ❌ TypeError
```


---

###### Block Scope and shadowing 
https://youtu.be/lW_erSjyMeM?si=TFAYS3-9kmaWAbjU

A block is just `{}` that creates a **lexical environment** _only_ for:
- `let`
- `const`
- `class`

```js
{
  let x = 1;
  const y = 2;
}
```

This block:
- allocates memory
- has its own scope chain link
- is destroyed when execution leaves
Blocks don’t matter by themselves — **what you declare inside them does**.


**Block scope vs `var`**
- `var` is **function-scoped**, not block-scoped
- If no function exists → it leaks to global
```js
{
  var a = 10;
}
console.log(a); // 10 (leaks)
```
But
```js
function test() {
  {
    var x = 5;
  }
  console.log(x); // 5 (function scope)
}
console.log(x);  // ReferenceError
test();
```
So:
- `var` ignores blocks
- `let` / `const` respect blocks


**Block scope vs `let`**
```js
{
  let b = 20;
  const c = 30;
}
console.log(b); // ReferenceError
```
Engine view:
- new lexical environment created
- `b` and `c` live there
- environment destroyed after block ends


**Shadowing: same name, closer wins**
**Shadowing** happens when a variable declared in an inner scope has the **same name** as a variable in an outer scope.

The inner variable **hides (shadows)** the outer one.

Rule: Closest scope wins.
```js
let x = 10;

function test() {
  let x = 20;   // shadows outer x
  console.log(x);
}

test();        // 20
console.log(x); // 10
```


**Block Scope Shadowing (`let` / `const`)**
```js
let a = 5;

{
  let a = 10;
  console.log(a); // 10
}

console.log(a);   // 5
```

**Illegal Shadowing**
```js
let b = 10;

{
  var b = 20; // ❌ SyntaxError
}
```
Why?
- `var` is function-scoped
- `let` is block-scoped
- This breaks scope rules → not allowed


**Shadowing + TDZ**
```js
let x = 100;

function demo() {
  console.log(x); // ❌ ReferenceError
  let x = 50;
}

demo();
```
Inner `x` shadows outer `x` and stays in **TDZ** until declared.

Why `var` shadowing is dangerous
Example01: 
```js
var x = 100;

function demo() {
  console.log(x); // undefined
  var x = 50;
}

demo();
```

Example02: 
```js
var x = 100;

function demo() {
  console.log(x); // 100
}

demo();
```

Example03:
```js
var a = 100;

{
  var a = 10;
}

console.log(a); // 10
```
This is **not real shadowing**.  
It’s the **same variable** being reassigned.
Reason: both `var a` point to the same function/global memory

Example04: Illegal shadowing
```js
let a = 10;
{
  var a = 20;
}
```
Why:
- `var` tries to declare in the **same scope** as `let`
- `let` forbids re-declaration
- engine stops at parse time → SyntaxError

Example05: Legal
```js
var b = 10;
{
  let b = 20;
}
```
Why:
- `let b` stays inside block
- does not leak outward
- no collision

Example06: Legal
```js
let x = 10;

function test() {
  var x = 20;
  console.log(x); // 20
}

test();
console.log(x); // 10
```
Function creates a **new boundary**.  
`var` stays inside it.


Arrow functions: nothing special for scope
```js
let x = 5;

const fn = () => {
  console.log(x);
};

fn(); // 5
```
Arrow functions:
- don’t change lexical scope rules
- just don’t create their own `this`
Variables behave exactly the same.


---

###### Closures
https://youtu.be/qikxEIxsXco?si=ggorML4FveApuiGo
- A **closure** is created when a function **remembers and can access variables from its lexical (outer) scope even after that outer function has finished executing**.
- It’s a **side-effect of lexical scope + functions being first-class**.
- A closure exists because the returned function keeps a hidden reference to its lexical environment, so the garbage collector cannot free that environment until all references to the function are gone.


Lexical scope comes first
JavaScript decides scope **at write time**, not run time.
```js
function outer() {
  let x = 10;

  function inner() {
    console.log(x);
  }
  inner();
}
outer();
```
Why does `inner()` see `x`?
Because `inner` was **written inside** `outer`.  
This relationship is fixed forever. Execution order doesn’t matter.
No closure magic yet — just scope.


**Closure appears when the outer function dies**
Closure becomes obvious when the parent function finishes execution **but the child still lives**.
```js
function outer() {
  let x = 10;

  return function inner() {
    console.log(x);
  };
}

const fn = outer();
fn(); // 10
```
What actually happened:
1. `outer()` runs
2. `x` is created
3. `inner` is returned
4. `outer()` execution context is popped off the stack
5. **BUT `x` is not destroyed** because `inner` still references it
Garbage collector sees a reference → keeps memory alive
That preserved environment = **closure**

Example:
```js
function outer() {
  let count = 0;

  function inner() {
    count++;
    console.log(count);
  }

  return inner;
}

const fn = outer();
fn(); // 1
fn(); // 2
fn(); // 3
```
 Why this works
- `outer()` finishes execution
- Normally `count` should be gone
- But `inner()` still has a reference to `count`
- JS keeps `count` alive in memory
That preserved scope is the **closure**.


What is Actually Preserved?
Not a copy.  
A **reference** to the variable.
```js
function outer() {
  let x = 10;
  return function inner() {
    console.log(x);
  };
}

const f = outer();
x = 100;     // different variable
f();         // 10
```

What actually happens in your line:
`x = 100;`
JavaScript interprets it like this:
“Assign 100 to a variable named `x` in the current scope chain. If it doesn’t exist, try the global scope.”


**Non-strict mode**
In a browser:
```
x = 100;
```
becomes:
```
window.x = 100;
```

**Strict mode (modern safe code)**
If you had:
```
"use strict";x = 100;
```
Then:
```
ReferenceError: x is not defined
```


**Deep closure chain (scope chain in action)**
```js
function outest() {
  let c = 30;

  function outer(b) {
    let a = 20;

    function inner() {
      console.log(a, b, c);
    }

    return inner;
  }

  return outer;
}

outest()("hello")(); 
// 20 "hello" 30
```
Lookup order:
1. `inner` scope
2. `outer` scope
3. `outest` scope
4. global
This is **lexical scope chain**, not runtime magic.


**Reassignment proves it’s a reference**
```js
function test() {
  let x = 5;

  function print() {
    console.log(x);
  }

  x = 99;
  return print;
}

const p = test();
p(); // 99
```
If closures stored values, this would print `5`.  


**Multiple closures = separate memories**
Each function call creates a new lexical environment.
```js
function makeCounter() {
  let count = 0;

  return function () {
    count++;
    console.log(count);
  };
}

const a = makeCounter();
const b = makeCounter();

a(); // 1
a(); // 2

b(); // 1
```
Same code. Different closures. Different memory.
This is why closures are perfect for private state.


**Closures in async**
`setTimeout`
```js
function delayed() {
  let msg = "Hello after 2s";

  setTimeout(function () {
    console.log(msg);
  }, 2000);
}

delayed();
```
Even after `delayed()` finishes, `msg` survives.

Not the function.  
Not the execution context.

What survives is **memory referenced by the callback**.

The callback holds a **pointer** to `msg`.  
As long as the pointer exists, garbage collection is forbidden.

That’s the closure.

Example:
```js
for (var i = 1; i <= 5; i++) {
  setTimeout(() => console.log(i), i * 1000);
}

//output
//6
//6
//6
//6
//6
```
Why?
- `var` is function-scoped
- One shared `i` . `var i` → **one memory location**
- Closures capture the same variable
- Loop runs instantly → `i` becomes `6`
- All callbacks reference **the same `i`**
- Timers expire later → they all read `6`
This is not async weirdness.  This is **shared memory + delayed execution**.

fix with `let`
```js
for (let i = 1; i <= 5; i++) {
  setTimeout(() => console.log(i), i * 1000);
}

//output
//1
//2
//3
//4
//5
```
What changes?
- `let` is **block-scoped**
- Each iteration creates a **new binding**
- Each callback closes over a **different memory address**


Example: Solving it without `let` (pure closure control)
```js
for (var i = 1; i <= 5; i++) {
  (function(x) {
    setTimeout(() => console.log(x), x * 1000);
  })(i);
}
```
What changed?
- `x` is a **function parameter**
- Each function call creates a **new execution context**
- Each callback closes over a **different `x`**
You manually manufactured block scope before ES6 existed.


---
###### First Class Functions
https://youtu.be/SHINoHxvTso?si=iVAr1cDaTQ2cuIsJ


**First-Class Functions**
JavaScript treats functions like numbers or strings. Functions can be assigned , passed, return etc into another function

Assign
```js
var fn = function () {
  console.log("stored");
};

fn()
```


Pass
```js
function run(fn) {
  fn();
}

run(() => console.log("passed"));
```


Return
```js
function makeFn() {
  return function () {
    console.log("returned");
  };
}

const f = makeFn();
f();
```

###### first order function
A first-order function is a function that doesn’t accept another function as an argument and doesn’t return a function as its return value. i.e, It's a regular function that works with primitive or non-function values.

```js
const firstOrder = () => console.log("I am a first order function!");
```


**Function Statement (Declaration)**
```js
a(); // works

function a() {
  console.log("a called");
}
```
**Why this works**
- During **memory creation phase**
    - `a` → points directly to the function object
- Before execution even starts, the function already exists
Think: **function body is hoisted fully**, not `undefined`.


**Function Expression**
```js
b(); // ❌ TypeError: b is not a function

var b = function () {
  console.log("b called");
};
```
What actually happens
Memory phase:
`b = undefined`

Execution phase:
`b = function () { ... }`

Calling `b()` early means you’re doing:
`undefined()`

Hence: **TypeError**, not ReferenceError.


**`let` / `const` + function expressions (TDZ trap)**
```js
foo(); // ❌ ReferenceError

let foo = function () {
  console.log("hi");
};
```
Why this is worse than `var`:
- `var` → hoisted as `undefined`
- `let` / `const` → **unusable until initialized**

So calling early isn’t “undefined is not a function”  
It’s **illegal access**


**Arrow functions**
```js
sayHi(); // ❌

const sayHi = () => {
  console.log("hi");
};
```
Arrow functions are **always expressions**, never declarations.
No hoisting of the function body. Same rules as `let`.


**Anonymous functions (why they “can’t exist alone”)**
❌ Illegal:
```js
function () {
  console.log("nope");
}
```
Why?
- Function **statements require a name**
- Without a name, JS can’t attach it to memory

✅ Legal (expression context):
```js
var x = function () {
  console.log("ok");
};
```
Rule: Anonymous functions must be used as values, never as standalone statements.


**Named Function Expression**
```js
var b = function xyz() {
  console.log(xyz);
};

b();      // works
xyz();    // ❌ ReferenceError
```
What’s happening:
- `xyz` exists **only inside the function body**
- It’s created for:
    - recursion
    - debugging (stack traces)

Parameters vs Arguments
```js
function sum(a, b) {   // parameters
  return a + b;
}

sum(2, 3);             // arguments
```


---

###### Callback functions
https://youtu.be/btj35dh3_U8?si=RrtJyAIB5OUNVYzT

Callback functions just **a function passed as a value**.
```js
function x(cb) {
  console.log("x running");
  cb(); // x decides *when* to call back
}

function y() {
  console.log("y called");
}

x(y);
```


**Callbacks enable async (without blocking)**
JS is single-threaded:
one Call Stack
one thing at a time

```js
console.log("start");

setTimeout(function () {
  console.log("timer done");
}, 2000);

console.log("end");

//output
//start
//end
//timer done
```
What actually happens:
- `setTimeout` registers the callback + timer
- JS **moves on immediately**
- after 2s → callback enters Call Stack
Nothing is “paused”.


**Blocking the main thread**
```js
console.log("start");

function blockFor5Sec() {
  const end = Date.now() + 5000;
  while (Date.now() < end) {}
}

blockFor5Sec();

console.log("end");

//output
//start
//end
```
During those 5 seconds:
- no clicks
- no timers
- page feels dead


**Event listeners = callbacks waiting in the shadows**
```js
document.getElementById("btn")
  .addEventListener("click", function () {
    console.log("clicked");
  });
```
What JS does:
- stores the callback
- does **nothing** until event happens
- when click occurs → callback pushed to stack


**Closures inside event listeners (state without globals)**
Bad (global state leak):
```js
let count = 0; //global

document.getElementById("btn")
  .addEventListener("click", () => {
    console.log(++count);
  });
```
Here:
- `count` lives in **Global Execution Context**
- It becomes part of global scope
- Any script anywhere can modify it

Good (closure-based state):
```js
function attachEventListener() {
  let count = 0;

  document.getElementById("btn")
    .addEventListener("click", function () {
      console.log(++count);
    });
}

attachEventListener();

attachEventListener();
```
Here:
- `count` lives inside `attachEventListener`
- That function runs
- It finishes
- But the callback still references `count`
- JS keeps `count` alive in memory
This is controlled, private memory.

---

###### Asynchronous JavaScript & EVENT LOOP
https://youtu.be/8zKuNo4ay8E?si=zXZVHmCNq70z_z-n

**JS engine vs browser (who does what)**

JavaScript engine (V8):
- Call Stack
- Heap
- Executes JS code

Browser:
- Timers
- DOM
- Network
- Storage
- Events

Bridge between them: window

So this:
`setTimeout(() => {}, 1000);`

is actually:
`window.setTimeout(() => {}, 1000);`

The engine **delegates** work to the browser.


**The Event Loop (its only job)**
The Event Loop keeps asking:
- Is Call Stack empty?
- Is something waiting?

If yes → move task to stack.

It does **not execute code**.  
It only **moves** code.


**Callback Queue (aka Task Queue)**
Goes here:
- `setTimeout`
- `setInterval`
- DOM events (click, scroll, keypress)


**Microtask Queue (higher priority)**
Goes here:
- `Promise.then / catch / finally`
- `fetch().then`
- `queueMicrotask`
- MutationObserver

Example:

```js
setTimeout(() => console.log("timeout"), 0);

Promise.resolve().then(() => {
  console.log("promise");
});

//output
//promise
//timeout

```
Why?
Microtask Queue is **always drained first**

Event Loop priority rule (memorize this)
> **Call Stack → Microtask Queue → Callback Queue**

The Event Loop:
1. Waits for stack to be empty
2. Runs **all microtasks**
3. Then runs **one callback task**
4. Repeats


Example:
```js
console.log("A");

setTimeout(() => console.log("B"), 0);

fetch("https://example.com")
  .then(() => console.log("C"));

Promise.resolve().then(() => console.log("D"));

console.log("E");

//output
//A
//E
//D
//C
//B
```
Why:
- sync first: A, E
- microtasks: D, C
- callback queue: B

---

###### JavaScript Runtime Environment and JS Engine
https://youtu.be/2WJL19wDH68?si=weOWiHzNWJpf1Hwu

**JavaScript Runtime Environment**
JavaScript by itself is useless. It needs a **runtime**.
Browser runtime gives:
- DOM
- timers
- fetch
- storage

Node.js runtime gives:
- file system
- OS access
- networking

But core execution is identical. Same engine, same rules.
```js
// Browser
setTimeout(() => console.log("hi"), 1000);

// Node
setTimeout(() => console.log("hi"), 1000);
```


**JavaScript Engine**
An engine is just a C++ program pretending to be a language
Rules come from: ECMAScript spec
That spec defines:
- how variables work
- how scopes behave
- how promises schedule microtasks

Not:
- DOM
- fetch
- setTimeout implementation
Those are runtime features.


**Parsing phase (code becomes structure)**
Before anything runs, code is **understood**.

Example:
```js
let x = 10 + 20;
```
Engine steps:
1. Tokenize → `let`, `x`, `=`, `10`, `+`, `20`
2. Build AST → meaning, not text

AST means the engine sees:
- declaration
- assignment
- binary operation

That’s why formatting doesn’t matter:
```js
let x=10+20;
```
Same AST. Same execution.


**Interpreter vs Compiler (why JS is fast _and_ flexible)**

Old-school:
- interpreter → fast start, slow execution
- compiler → slow start, fast execution
JS uses **both**.


**JIT compilation**

V8 pipeline:
```
AST → Ignition → Bytecode → TurboFan → Optimized machine code
```

Example:
```js
function add(a, b) {
  return a + b;
}

add(1, 2);
add(3, 4);
add(5, 6);
```
What happens:
- Ignition runs it immediately
- Engine notices `add` is called often
- TurboFan optimizes it assuming numbers
- Machine code replaces bytecode


**Optimization can backfire (important)**
```js
function add(a, b) {
  return a + b;
}

add(1, 2);
add("1", "2"); // 💥 different types
```
Engine thought: “This function always adds numbers”

Now types change → **de-optimization**
- optimized code thrown away
- back to slow path
This is why **stable types matter**.


**Call Stack + Heap (execution & memory)**
```js
function foo() {
  let x = { value: 42 };
  bar(x);
}

function bar(obj) {
  obj.value++;
}

foo();
```
- `foo`, `bar` → Call Stack
- `{ value: 42 }` → Heap
- stack stores references, not objects
When stack unwinds and nothing references the object → garbage collectible.


**Garbage Collection**
V8 mostly uses **Mark & Sweep**.
Simplified:
1. Start from global objects
2. Mark everything reachable
3. Sweep the rest

Example leak:
```js
let cache = [];

function store() {
  cache.push({ data: "big" });
}
```
Nothing ever gets freed because references remain.
GC is automatic, but **not magical**.


**Why optimizations exist**
```js
for (let i = 0; i < 1_000_000; i++) {
  obj.x;
}
```
Inline caching:
- first lookup: slow
- engine remembers where `x` lives
- next lookups: fast
That’s how JS competes with C++ in hot paths.

---

###### `setTimeout` Lies About Time
https://youtu.be/nqsPmuicJJc?si=iTJPgCGt0AbQYB5u

`setTimeout(delay)` does **not** mean “run after _delay_ ms”.  
It means:  Run no earlier than delay ms, _if_ the call stack is empty.

Time is not the deciding factor.  
The call stack is.


**Single Thread = One Call Stack = One Bottleneck**
JavaScript has:
- **One call stack**
- **One main thread**
If the stack is busy, **everything waits**. Timers don’t interrupt. Promises don’t interrupt. Nothing interrupts.

Blocking example (the truth demo)
```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 2000);

// Block for ~5 seconds
const start = Date.now();
while (Date.now() - start < 5000) {}

console.log("End");

//output
//Start
//End
//Timeout   // after ~5 seconds, NOT 2
```
Timer expired at 2s.  
Callback waited **3 more seconds** because the stack was blocked.


**Web APIs, Callback Queue, Event Loop (Actual Flow)**
When `setTimeout` runs:
1. JS engine registers timer in **Web API**
2. Timer counts down **outside JS engine**
3. Callback moves to **Callback Queue**
4. **Event Loop checks**:
    - Is Call Stack empty?
    - If NO → wait
    - If YES → push callback
No empty stack = no execution.


---
###### **Higher-Order Functions**
https://youtu.be/HkWxvB1RJq0?si=WHdPHYpFnQn8tXDq
A **Higher-Order Function (HOF)** does **one of two things**:
- takes a function as input
- returns a function as output

```js
function greet() {
  console.log("Namaste");
}

function execute(fn) {
  fn();
}

execute(greet);
```
Why? bcz functions are first class citizen in JS


**Why Functional Programming Exists**
```js
function calculateArea(arr) {
  const result = [];
  for (let r of arr) {
    result.push(Math.PI * r * r);
  }
  return result;
}

function calculateCircumference(arr) {
  const result = [];
  for (let r of arr) {
    result.push(2 * Math.PI * r);
  }
  return result;
}

const radii = [1, 2, 3, 4];

console.log(calculateArea(radii));
console.log(calculateCircumference(radii));
```
Problem:
- Loop logic duplicated
- Only formula changes
- Maintenance nightmare


**Writing a Proper Higher-Order Function**
```js
function calculate(arr, logic) {
  const result = [];
  for (let r of arr) {
    result.push(logic(r));
  }
  return result;
}

const radii = [1, 2, 3, 4];

const area = calculate(radii, r => Math.PI * r * r);
const circumference = calculate(radii, r => 2 * Math.PI * r);
const diameter = calculate(radii, r => 2 * r);

console.log(area);
console.log(circumference);
console.log(diameter);
```
This is **real functional programming**:
- One loop
- Infinite behaviors


**You Already Know This — It’s `map`**
Your `calculate` **is literally** `map`.
```js
radius.map(area);
radius.map(circumference);
radius.map(diameter);
```
Interview truth:  
If you write your own `calculate`, interviewer expects you to say:
“This is basically how `map` works internally.”
If you don’t say that, you missed the point.

---
###### map filter and reduce
https://youtu.be/zdp0zrpKzIE?si=fL7T1Xe65fj6hgcl




---

pending
week 6| topic 4 |
+ lec 38

Strict mode
Closure


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

Prototype chain is the mechanism in JavaScript where objects inherit properties from other objects through a linked chain of prototypes.

When you access a property on an object, JS:
1. Looks on the object itself
2. If not found, checks its prototype (`__proto__`)
3. Continues up the chain until `Object.prototype`
4. If still not found → `undefined`


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

why?
JavaScript is single-threaded. It executes one thing at a time. Many operations (network requests, file reading, timers, user clicks) take time. If JavaScript waited for each one to finish, the entire application would freeze.

**Simple callback**
```js
function greet(name, callback) {
    console.log(`Hello ${name}`);
    callback();
}
function sayBye() {
    console.log("Goodbye");
}
greet("Alice", sayBye);
// Output:
// Hello Alice
// Goodbye
```


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

###### CallBack hell (Pyramid of Doom)
The **callback hell** occurs at the **call site**, where callbacks are nested multiple levels deep.
Problems:
- Deep indentation
- Hard to read
- Difficult error handling
- Difficult maintenance
- Sequential dependencies become messy

Callback Hell is a situation where multiple asynchronous callbacks are nested inside each other, creating deeply indented code, often called the 'Pyramid of Doom.' 
It makes code difficult to read, debug, maintain, and handle errors. 
Modern JavaScript avoids callback hell by using Promises and async/await, which provide a cleaner and more maintainable way to write asynchronous code.

```js
function getData(dataId, getNextData) {
    setTimeout(() => {
        console.log("Data:", dataId);

        if (getNextData) {
            getNextData();
        }
    }, 2000);
}

getData(1, () => {
    getData(2, () => {
        getData(3, () => {
            console.log("All data fetched");
        });
    });
});
```


---
### Promises
https://youtu.be/NJwRQgsu1Q8
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
https://www.w3schools.com/js/js_promise.asp
+ A Promise is basically an object representing a future value.
+ The **`Promise`** object represents the eventual completion (or failure) of an asynchronous operation and its resulting value.
+ A **Promise** is like a _placeholder_ for a value that you’ll get **later** (either success or failure).

A Promise can be in one of **three states**:
- `pending`: Initial state, neither fulfilled nor rejected.
- `fulfilled`: The operation completed successfully.
- `rejected`: The operation failed (e.g., due to a network error).

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

###### Promise Chaining
Promise chaining means **connecting multiple `.then()` methods so that each asynchronous task runs only after the previous one is completed.**

```js
Promise.resolve(1)
  .then((result) => {
    console.log(result); // 1
    return result * 2;
  })
  .then((result) => {
    console.log(result); // 2
    return result * 3;
  })
  .then((result) => {
    console.log(result); // 6
  });
```

```js
new Promise(function (resolve, reject) {
  setTimeout(() => resolve(1), 1000);
})
  .then(function (result) {
    console.log(result); // 1
    return result * 2;
  })
  .then(function (result) {
    console.log(result); // 2
    return result * 3;
  })
  .then(function (result) {
    console.log(result); // 6
    return result * 4;
  });
```



`Promise.all()` is a static method of the `Promise` object that takes an **iterable** (usually an array) of promises and returns **a new promise**.

The returned promise:
- ✅ **Resolves** only when **all** input promises resolve.
- ❌ **Rejects immediately** if **any one** of the input promises rejects (this is called **fail-fast** behavior).

```js
Promise.all([Promise1, Promise2, Promise3]) .then(result) => {   console.log(result) }) .catch(error => console.log(`Error in promises ${error}`))
```

**Note:** Remember that the order of the promises(output the result) is maintained as per input order.

i.e. All promises resolve
```js
const p1 = Promise.resolve(10);

const p2 = new Promise(resolve => {
    setTimeout(() => resolve(20), 1000);
});

const p3 = Promise.resolve(30);

Promise.all([p1, p2, p3])
    .then(results => {
        console.log(results);
    })
    .catch(error => {
        console.log(error);
    });
// Output: [10, 20, 30]
```
Notice that although p2 finishes last, the results are returned in the same order as the input array.

i.e. One promise rejects
```js
const p1 = Promise.resolve("A");

const p2 = Promise.reject("Something went wrong");

const p3 = Promise.resolve("C");

Promise.all([p1, p2, p3])
    .then(results => {
        console.log(results);
    })
    .catch(error => {
        console.log(error);
    });
// Output: Something went wrong
```
The .then() is never executed because one promise rejected.




---
### async/await

```js
function getData(dataId) {
    return new Promise((resolve) => {
        setTimeout(() => {
            console.log(dataId);
            resolve();
        }, 2000);
    });
}

async function fetchData() {
    await getData(1);
    await getData(2);
    await getData(3);
    console.log("All data fetched");
}

fetchData();
```


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


