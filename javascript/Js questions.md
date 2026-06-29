
### Arrays

Traversal
```js
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
```

`for of` gives the item in array
```js
for (const item of arr) {
    console.log(item);
}
```
where as `for in` gives the index in array

---
###### Q. Tell Output
```js
if([]){
    console.log("asf");
}else{
    console.log("asfsdfg");
}
```
asf as empty array is truthy value 
In JS:
- **Falsy values only:**  
    `false, 0, -0, 0n, "", null, undefined, NaN`
- Everything else is **truthy**, including:
    - `[]` (empty array)
    - `{}` (empty object)
    - `"0"` (string with zero)

---
###### Q. Tell Output
```js
function sayHi() {
  console.log(name);
  console.log(age);
  var name = 'Lydia';
  let age = 21;
}
sayHi();
```
undefined and ReferenceError

---
###### Q. Tell Output
```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
// Output:
// 3
// 3
// 3

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
// Output:
// 0
// 1
// 2
```
- **`var`** → Function-scoped. All `setTimeout` callbacks share the **same `i`**. By the time they run, the loop has finished, so `i = 3`.
- **`let`** → Block-scoped. A **new `i` is created for each iteration**, so each callback remembers its own value (`0`, `1`, `2`).

---
###### Q. Tell Output
```js
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius,
};

console.log(shape.diameter());  // 20
console.log(shape.perimeter()); // NaN
```
- **`diameter()`** → Regular method. `this` refers to `shape`, so `this.radius = 10`.
- **`perimeter` (arrow function)** → Arrow functions **don't have their own `this`**. They use the surrounding (lexical) `this`, which is **not `shape`**, so `this.radius` is `undefined` → result is `NaN`.
2 * Math.PI * undefined
2 * 3.14159      // 6.28318
6.28318 * undefined
When `undefined` is used in a numeric operation, JavaScript converts it to **`NaN`**.

To fix perimeter
+ we can use regular function
```js
perimeter() {
    return 2 * Math.PI * this.radius;
}
// or
perimeter: function () {
    return 2 * Math.PI * this.radius;
}
```


---
###### Q. Tell Output
```js
const person = {
    name: "John",

    greet() {
        return () => {
            console.log(this.name);
        };
    }
};

const fn = person.greet();
fn(); // John
```
Why?
- `greet()` is a **regular method**.
- It is called as `person.greet()`
- Therefore, inside `greet()`, `this === person`.
- The arrow function is **created inside `greet()`**.
- Arrow functions capture (`lexically inherit`) the `this` of their surrounding function.
- So the arrow function permanently captures `this = person`.
- Even when called later as `fn()`, it still prints `"John"`.

Key Difference
❌ Previous example:
```js
const person = {
  perimeter: () => console.log(this)
};
```
Arrow function is created in the **global scope**, so `this` is global.

✅ This example:
```js
greet() {
  return () => console.log(this.name);
}
```
Arrow function is created **inside a regular method**, so it captures `this = person`.

Arrow functions don't have their own `this`; they inherit the `this` from the scope in which they are created.


---
###### Q. Tell Output
```js
const obj = {
  name: "John",
  greet: function () {
    console.log(this.name);

    setTimeout(function () {
      console.log(this.name);
    }, 0);
  }
};
obj.greet();
```
- What is the output?
- Why does the first console.log work?
- Why does the second one not print "John"?
- Give two different ways to fix it. (This is a very common interview question.)

Output
```text
John
undefined
```

(In Node.js, the second output may also be `undefined`. In browsers, it depends on the global object, but for interviews, `undefined` is the expected answer.)_

Why?
Why does the first `console.log` print `"John"`?
- `greet()` is called as `obj.greet()`. (this binds to obj and it gets defined)
- In a regular method call, `this` refers to the object before the dot (`obj`). 
- Therefore, `this.name` is `"John"`.

Why doesn't the second `console.log` print `"John"`?
- `setTimeout` executes the callback as a **normal function**, not as an object method.
- Therefore, the callback gets its own `this`, which is **not** `obj`.
- So `this.name` is `undefined`.

Two ways to fix it
Solution 1 (Preferred): Use an arrow function
```js
setTimeout(() => {
  console.log(this.name);
}, 0);
```
Why?
- Arrow functions don't have their own `this`.
- They inherit `this` from `greet()`, which is `obj`.

Solution 2: using `bind`
```js
setTimeout(function () {
	console.log(this.name);
}.bind(this), 0);
```


---
###### Q. Tell Output
```js
+true;
!'Lydia';
```
- The unary plus tries to convert an operand to a number. `true` is `1`, and `false` is `0`.
- The string `'Lydia'` is a truthy value. What we're actually asking, is "Is this truthy value falsy?". This returns `false`.

---
###### Q. Tell Output
```js
const bird = {
  size: 'small',
};

const mouse = {
  name: 'Mickey',
  small: true,
};
console.log(mouse.bird.size); // ❌ Error  
console.log(mouse[bird.size]); // ✅ true  
console.log(mouse[bird["size"]]); // ✅ true
```
- **A:** `mouse.bird.size`
    - `mouse.bird` is `undefined` (there is no `bird` property).
    - `undefined.size` → **TypeError** ❌
- **B:** `mouse[bird.size]`
    - `bird.size` → `"small"`
    - `mouse["small"]` → `true` ✅
- **C:** `mouse[bird["size"]]`
    - `bird["size"]` → `"small"`
    - `mouse["small"]` → `true` ✅
**Note:** `obj.prop` uses the literal property name, while `obj[key]` evaluates `key` first and then looks up that property.

---
###### Q. Tell Output
```js
let c = { greeting: 'Hey!' };
let d;

d = c;
c.greeting = 'Hello';
console.log(d.greeting); // "Hello"
```
Why?
- Objects are assigned **by reference**, not copied.
- `c` and `d` point to the **same object**.
- Changing `c.greeting` also changes what `d` sees.

Rule for notes:  
Primitive values → copied by value.  
Non-Primitive (Objects/Arrays/Functions) → copied by reference.

---
###### Q. Tell Output
```js
let a = 3;
let b = new Number(3);
let c = 3;

console.log(a == b); // true  
console.log(a === b); // false  
console.log(b === c); // false
```
Why?
- `a` and `c` are **primitive numbers**.
- `b` is a **Number object** (`new Number(3)`).
- `==` → Converts `b` to primitive `3`, so `3 == 3` → `true`.
- `===` → No type conversion. `number !== object`, so `false`.
- `b === c` → `object !== number`, so `false`.

Rule for notes:
- `==` → compares **value** (with type coercion).
- `===` → compares **value + type** (no type coercion).
- Avoid `new Number()`, `new String()`, `new Boolean()` in practice. Use primitives instead.

---
###### Q. Tell Output
```js
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor;
    return this.newColor;
  }

  constructor({ newColor = 'green' } = {}) {
    this.newColor = newColor;
  }
}

const freddie = new Chameleon({ newColor: 'purple' });
console.log(freddie.colorChange("orange")); // TypeError
```
Why?
- `static` methods belong to the **class**, not its instances.
- `freddie` is an **instance**, so it **doesn't have** `colorChange()`.

Correct:
```
Chameleon.colorChange("orange");
```

Rule for notes:
- `static` → call with **ClassName.method()**
- Instance methods → call with **instance.method()**

---
###### Q. Tell Output
```js
let greeting;
greetign = {}; // Typo!
console.log(greetign);
// Output: {}
```

---
###### Q. Tell Output
```js
function bark() {
  console.log('Woof!');
}
bark.animal = 'dog';
```
This is possible in JavaScript, because functions are objects! (Everything besides primitive types are objects)
A function is a special type of object. The code you write yourself isn't the actual function. The function is an object with properties. This property is invocable.

---
###### Q. Tell Output
```js
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person('Lydia', 'Hallie');
Person.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};
console.log(member.getFullName()); // TypeError: member.getFullName is not a function
console.log(Person.getFullName()); // undefined undefined
```
Why?
- `Person.getFullName` adds a method to the **constructor function**, not its instances.
- `member` doesn't have `getFullName()`.

Correct ways
1. Add to the prototype (recommended):
```js
Person.prototype.getFullName = function () {
  return `${this.firstName} ${this.lastName}`;
};
console.log(member.getFullName()); // "Lydia Hallie"
```

2. Or add directly to the instance:
```js
member.getFullName = function () {
  return `${this.firstName} ${this.lastName}`;
};
```
Rule for notes:
- `Person.method()` → static method (constructor).
- `Person.prototype.method()` → available on all instances.
- `member.method()` → only that instance.

---
###### Q. Tell Output
```js
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const lydia = new Person("Lydia", "Hallie");
const sarah = Person("Sarah", "Smith");

console.log(lydia); // Person { firstName: "Lydia", lastName: "Hallie" }
console.log(sarah); // undefined
```
Why?
- `new Person()` → Creates a new object, binds `this` to it, and returns it.
- `Person()` (without `new`) → No object is created. Since there's no `return`, it returns `undefined`.

In non-strict mode, `this` becomes the global object (`window` in browsers), so `window.firstName` and `window.lastName` are created. In strict mode, `this` is `undefined`, causing a `TypeError`.

Rule for notes:
- `new Constructor()` → Creates and returns an instance.
- `Constructor()` → Normal function call; no instance is created.


###### Q. Tell Output
Three phases of event propagation:
1. Capturing Phase → Event travels **from `window` down to the target element**.
2. Target Phase → Event reaches the **target element**.
3. Bubbling Phase → Event travels **from the target back up to `window`**.

Flow for notes:
```text
window
  ↓
document
  ↓
html
  ↓
body
  ↓
parent
  ↓
target   ← Target Phase
  ↑
parent
  ↑
body
  ↑
html
  ↑
document
  ↑
window
```
Mnemonic: Capture ↓ → Target → Bubble ↑


 ###### Q. Tell Output
 All object have prototypes.
 False
Why?
- Most objects have a prototype.
- But objects created with **`Object.create(null)`** have **no prototype**.
```js
const obj = {};
console.log(Object.getPrototypeOf(obj)); // Object.prototype

const obj2 = Object.create(null);
console.log(Object.getPrototypeOf(obj2)); // null
```

###### Q. Tell Output
```js
function sum(a, b) {
  return a + b;
}
console.log(sum(1, "2")); // "12"
```
Why?
- `+` with a **string** performs **string concatenation**.
- Number `1` is converted to string `"1"`.
```js
1 + "2" // "12"
```
Rule for notes:
- `+` + string → **concatenation**
- `-`, `*`, `/` + string → **numeric conversion** (if possible)
```js
1 + "2" // "12"
"5" - 2 // 3
"5" * 2 // 10
"5" / 2 // 2.5
```

###### Q. Tell Output
```js
let number = 0;
console.log(number++); // 0
console.log(++number); // 2
console.log(number);   // 2
```
Why?
- `number++` (**post-increment**) → Return current value, then increment.
- `++number` (**pre-increment**) → Increment first, then return value.

Step by step:
```js
number = 0

number++  // prints 0, number becomes 1
++number  // number becomes 2, prints 2
number    // 2
```
Rule for notes:
- `x++` → **Use, then increment**
- `++x` → **Increment, then use**

###### Q. Tell Output
```js
function getPersonInfo(one, two, three) {
  console.log(one);
  console.log(two);
  console.log(three);
}
const person = "Lydia";
const age = 21;
getPersonInfo`${person} is ${age} years old`;
```

Output:
```js
["", " is ", " years old"] // one
"Lydia"                    // two
21                         // three
```
Why?
This is a **tagged template literal**.
A tagged template calls the function like this:
```js
getPersonInfo(
  ["", " is ", " years old"], // array of string parts
  "Lydia",                    // first interpolation
  21                          // second interpolation
);
```
Rule for notes:
- Tagged template: `fn\`...``
- 1st argument → array of literal string parts.
- Remaining arguments → values inside `${}`.

###### Q. Tell Output
```js
function checkAge(data) {
  if (data === { age: 18 }) {
    console.log("You are an adult!");
  } else if (data == { age: 18 }) {
    console.log("You are still an adult.");
  } else {
    console.log("Hmm.. You don't have an age I guess");
  }
}
checkAge({ age: 18 });
// "Hmm.. You don't have an age I guess"
```
Why?
- Objects are compared by **reference**, not by value.
- `{ age: 18 }` creates a **new object** every time.

```js
{ age: 18 } === { age: 18 } // false
{ age: 18 } ==  { age: 18 } // false
```
Both objects have the same content but are stored at **different memory locations**.
Rule for notes:
- Primitives → compared by **value**.
- Objects/Arrays/Functions → compared by **reference (memory address)**.


###### Q. Tell Output
```js
function getAge(...args) {
  console.log(args); // [ 21 ]
  Array.isArray(args) // true
  console.log(typeof args); // object
}
getAge(21); 
```
Why?
- `...args` (rest parameter) collects all arguments into an **array**.
- In JavaScript, **arrays are objects**.

Rule for notes:
- `...args` → **Array**
- `typeof array` → `"object"`
- To check for an array, use `Array.isArray()`, **not** `typeof`.

###### Q. Tell Output
```js
function getAge() {
  "use strict";
  age = 21;
  console.log(age); // ReferenceError
}
getAge(); 
```
Why?
- In **strict mode**, you **cannot assign to an undeclared variable**.
- `age` was never declared with `let`, `const`, or `var`.

```js
age = 21; // ❌ ReferenceError
```

Rule for notes:
- Normal mode → undeclared variable becomes **global** (bad practice).
- Strict mode → undeclared variable → **ReferenceError**.

###### Q. Tell Output
```js
const sum = eval("10 * 10 + 5");
console.log(sum); // 105
```
Why?
- `eval()` executes the string as JavaScript code.
- It evaluates `"10 * 10 + 5"` and returns the result.
```js
eval("10 * 10 + 5"); // 105
```

Rule for notes:
- `eval(string)` → Executes the string as JavaScript code.
- **Avoid `eval()`** in production: it's slow and can introduce security vulnerabilities.

.i.e.
```js
const fn = eval('()=>console.log("x")');
fn();
```


######  How long is cool_secret accessible?
```js
sessionStorage.setItem('cool_secret', 123);
```
- A: Forever, the data doesn't get lost.
- B: When the user closes the tab.
- C: When the user closes the entire browser, not only the tab.
- D: When the user shuts off their computer.

**Answer: B — When the user closes the tab. ✅**
```js
sessionStorage.setItem("cool_secret", 123);
```

- **`sessionStorage`** lasts for the **current browser tab/session**.
- Closing the **tab** (or window) clears it.
- Refreshing the page **does not** clear it.

| Storage          | Lifetime                            |
| ---------------- | ----------------------------------- |
| `sessionStorage` | Until the **tab/window is closed**  |
| `localStorage`   | **Persists** until manually cleared |

###### Q. Tell Output
```js
var num = 8;
var num = 10;
console.log(num); // 10
```
Why?
- `var` allows redeclaration in the same scope.
- The second declaration overwrites the first value.

Rule for notes:
- `var` → ✅ Redeclare + Reassign
- `let` → ❌ Redeclare, ✅ Reassign
- `const` → ❌ Redeclare, ❌ Reassign

###### Q. Tell Output
```js
const obj = { 1: "a", 2: "b", 3: "c" };
const set = new Set([1, 2, 3, 4, 5]);

console.log(obj.hasOwnProperty("1")); // true
console.log(obj.hasOwnProperty(1));   // true

console.log(set.has("1")); // false
console.log(set.has(1));   // true
```
Why?
- **Object keys are always strings** (or symbols), so `1` is converted to `"1"`.
```js
obj[1] === obj["1"] // true
```
- **Set preserves types**. String `"1"` and number `1` are different values.

Rule for notes:
- **Object** → Numeric keys become **strings**.
- **Set** → No type conversion; `"1"!== 1`.


###### Global Execution Context creates
The JavaScript global execution context creates two things for you: the global object, and the "this" keyword.

1. **Global Object**
    - Browser → `window`
    - Node.js → `global`

2. **`this`**
    - In the global scope:
        - Browser (non-module) → `this === window`
        - Node.js/CommonJS → `this !== global` (module-specific)
        - ES Modules → `this === undefined`

Rule for notes:
```text
Global Execution Context creates:
1. Global Object (window/global)
2. Global this
```

During the creation phase, it also sets up the memory for variables/functions (hoisting), but the two built-in values are the **global object** and **`this`**.


###### Q. Tell Output
```js
for (let i = 1; i < 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
//Output:
// 1
// 2
// 4
```


###### Q. Tell Output
```js
String.prototype.giveLydiaPizza = () => {
  return "Just give Lydia pizza already!";
};

const name = "Lydia";

console.log(name.giveLydiaPizza());
// "Just give Lydia pizza already!"
```
Why?
- Methods added to `String.prototype` are available to **all strings**.
- JavaScript temporarily wraps the primitive string in a `String` object (**autoboxing**) so it can access prototype methods.

```js
"Lydia".giveLydiaPizza(); // Works
```

Rule for notes:
- Primitive strings can call methods because of **autoboxing**.
- Adding a method to `String.prototype` makes it available to **every string**.

**Industry note:** Avoid modifying built-in prototypes (`String.prototype`, `Array.prototype`, etc.) in production code—it can cause conflicts with other libraries or future JavaScript features.


###### Q. Tell Output
```js
const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"));
const baz = () => console.log("Third");
bar();
foo();
baz();
// Output:
// First
// Third
// Second
```
Why?
- `setTimeout()` is **asynchronous**. It registers the callback and continues.
- `foo()` and `baz()` run immediately.
- After the call stack is empty, the event loop executes the `setTimeout` callback.

Rule for notes:
- **Synchronous code** runs first.
- **`setTimeout` callbacks** run later via the **Web APIs → Callback Queue → Event Loop**.


###### Q. What is the event.target when clicking the button?
```html
<div onclick="console.log('first div')">
  <div onclick="console.log('second div')">
    <button onclick="console.log('button')">
      Click!
    </button>
  </div>
</div>
```

When you click the **button**, the output is:
```text
button
second div
first div
```
Why?
- `onclick` handlers listen during the **bubbling phase** by default.
- Event starts at the **target** (`button`) and bubbles up to its parents.

Flow:
```text
button
   ↑
second div
   ↑
first div
```

Rule for notes:
- Default event listeners (`onclick`, `addEventListener("click")`) → **Bubbling**.
- To listen during **capturing**, use:
```js
element.addEventListener("click", handler, true);
```
or
```js
element.addEventListener("click", handler, { capture: true });
```



###### Q. When you click the paragraph, what's the logged output?
```html
<div onclick="console.log('div')">
  <p onclick="console.log('p')">
    Click here!
  </p>
</div>
```
When you click the **`<p>`**, the output is:
```text
p
div
```
Why?
- Event occurs on the **target** (`p`).
- Then it **bubbles** up to the parent (`div`).

Flow:
```text
p
↑
div
```

Rule for notes:
- Default `onclick` → **Bubbling**.
- Child handler runs first, then parent handler (unless propagation is stopped with `event.stopPropagation()`).


###### Q. Tell Output
```js
const person = { name: "Lydia" };

function sayHi(age) {
  return `${this.name} is ${age}`;
}
console.log(sayHi.call(person, 21)); // "Lydia is 21"
console.log(sayHi.bind(person, 21)); // [Function]
```

Why?
- `call()` → **Invokes immediately** with `this` and arguments.
- `bind()` → **Returns a new function** with `this` and arguments bound. It does **not** execute it.

To execute the bound function:
```js
const boundFn = sayHi.bind(person, 21);
console.log(boundFn()); // "Lydia is 21"
```

Rule for notes:
- `call()` → **Call now**.
- `apply()` → **Call now** (arguments as an array).
- `bind()` → **Call later** (returns a new function).


###### Q. Tell Output
```js
function sayHi() {
  return (() => 0)();
}

console.log(typeof sayHi()); // "number"
```
Why?
- `(() => 0)()` is an **immediately invoked arrow function (IIFE)**.
- It returns `0`.
- `typeof 0` is `"number"`.

Rule for notes:
- `typeof` returns the **type of the returned value**, not the function.
- `(() => value)()` → executes immediately and returns `value`.


###### Q. Tell Output
```js
console.log(Boolean(0));                  // false
console.log(Boolean(new Number(0)));      // true
console.log(Boolean(''));                 // false
console.log(Boolean(' '));                // true
console.log(Boolean(new Boolean(false))); // true
console.log(Boolean(undefined));          // false
```
Rule for notes
- **Falsy:** `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`
- **Everything else is truthy**, including **all objects**.


###### Q. Tell Output
```js
console.log(typeof typeof 1); // "string"
```

Why?
Evaluation happens left to right:
```js
typeof 1          // "number"
typeof "number"   // "string"
```

Rule for notes:
- `typeof` **always returns a string**.
- Therefore, `typeof typeof x` is **always `"string"`**.

---
###### Q. Tell Output
```js
const numbers = [1, 2, 3];
numbers[10] = 11;
console.log(numbers); // [1, 2, 3, <7 empty items>, 11]
console.log(numbers[4]); // undefined
```

Why?
- Arrays in JavaScript are **sparse**.
- Assigning to index `10` creates **empty slots (holes)** from index `3` to `9`.

```js
numbers.length // 11
```
Rule for notes:
- Assigning beyond the current array length creates **empty slots (holes)**.
- `length` becomes **highest index + 1**.
+ Sparse (holey) arrays are slower because JavaScript engines can't optimize them as efficiently as dense (packed) arrays, so element access and iteration may be slower.

---
###### Q. Tell Output
```js
(() => {
  let x, y;
  try {
    throw new Error();
  } catch (x) {
    (x = 1), (y = 2);
    console.log(x);
  }
  console.log(x);
  console.log(y);
})();
// Output:
// 1
// undefined
// 2
```

Why?
- `catch (x)` creates a **new block-scoped variable `x`** that shadows the outer `x`.
- Inside `catch`, `x = 1` changes only the **catch variable**.
- `y = 2` modifies the **outer `y`** because there is no local `y` in `catch`.

Rule for notes:
- `catch (x)` → creates a **new block-scoped variable**.
- Variables declared in `catch` **shadow** outer variables.
- Changes to the catch variable **do not affect** the outer variable.


######  Everything in JavaScript is either a...
A: primitive or object

JavaScript values fall into **two categories**:
1. **Primitive** `string`, `number`,`bigint`,`boolean`,`undefined`,`symbol`,`null`
2. **Object** Objects, Arrays, Functions, Dates, Maps, Sets

Why not B?
Functions are actually **objects**.

```js
typeof function() {} // "function"
typeof []            // "object"
typeof {}            // "object"
function() {} instanceof Object // true
```

Rule for notes:
- JavaScript values = **Primitive** or **Object**.
- **Functions are objects** (with a special `typeof` result of `"function"`).


###### Q. Tell Output
```js
console.log([[0, 1], [2, 3]].reduce(
  (acc, cur) => {
    return acc.concat(cur);
  },
  [1, 2],
)); // [ 1, 2, 0, 1, 2, 3 ]
```

Step by step:
```js
Initial acc = [1, 2]

1st iteration:
acc.concat([0, 1])
→ [1, 2, 0, 1]

2nd iteration:
[1, 2, 0, 1].concat([2, 3])
→ [1, 2, 0, 1, 2, 3]
```

Rule for notes:
- `reduce()` accumulates a single value.
- `concat()` returns a **new array** (does not modify the original).


###### Q. Tell Output
```js
console.log(!!null); // false
console.log(!!"");   // false
console.log(!!1);    // true
```

Why?
- `!!` converts any value to its **boolean equivalent**.
- First `!` negates the truthiness.
- Second `!` negates it again, giving the boolean value.

Rule for notes:
- `!!value` → Convert `value` to `true` or `false`.
- Falsy values (`null`, `undefined`, `0`, `""`, `NaN`, `false`) → `false`.
- Everything else → `true`.


###### Q.  What does the setInterval method return in the browser?
Answer: a unique ID

```js
const id = setInterval(() => console.log("Hi"), 1000);
console.log(id); // e.g. 1
```

Why?
- `setInterval()` returns a **timer ID**.
- Use this ID to stop the interval.

```js
const id = setInterval(() => console.log("Hi"), 1000);
clearInterval(id);
```

Rule for notes:
- `setInterval()` → returns a **timer ID**.
- `clearInterval(id)` → stops that interval.


###### Q. Tell Output
```js
console.log([..."Lydia"]); // ["L", "y", "d", "i", "a"]
```

Why?
- The **spread operator (`...`)** expands an **iterable** into individual elements.
- Strings are iterable, so each character is spread into the array.

```js
[..."abc"] // ["a", "b", "c"]
```

Rule for notes:
- `...` on a string → spreads it into individual characters.
- Strings are iterable.


###### Q. Tell Output
```js
function* generator(i) {
  yield i;
  yield i * 2;
}
const gen = generator(10);
console.log(gen.next().value); // 10
console.log(gen.next().value); // 20
```
Why?
- `function*` creates a **generator**.
- `yield` **pauses** execution and returns a value.
- Each `next()` resumes from the previous `yield`.

Step by step:
```js
gen.next() // { value: 10, done: false }
gen.next() // { value: 20, done: false }
gen.next() // { value: undefined, done: true }
```

Rule for notes:
- `function*` → Generator function.
- `yield` → Pause and return a value.
- `next()` → Resume execution until the next `yield`.


###### Q. Tell Output
```js
const firstPromise = new Promise((res) => {
  setTimeout(res, 500, "one");
});
const secondPromise = new Promise((res) => {
  setTimeout(res, 100, "two");
});
Promise.race([firstPromise, secondPromise]).then((res) =>
  console.log(res)
);
// "two"
```

Why?
- `Promise.race()` settles with the **first promise that settles** (resolve or reject).
- `secondPromise` resolves in **100ms**, so it wins.

Timeline:
```text
100ms → secondPromise ✅ ("two")
500ms → firstPromise  (ignored)
```

Rule for notes:
- `Promise.race()` → First **resolved or rejected** promise wins.
- `Promise.all()` → Waits for **all** to resolve.
- `Promise.any()` → First **resolved** promise wins.
- `Promise.allSettled()` → Waits for **all** to settle (resolve/reject).


###### Q. Tell Output
```js
let person = { name: "Lydia" };
const members = [person];
person = null;
console.log(members); // [{ name: "Lydia" }]
```

Why?
- `members` stores a **reference** to the object.
- `person = null` only changes the `person` variable, **not the object**.

Memory:
```text
person ─────► { name: "Lydia" }
members[0] ──┘

person = null

person      null
members[0] ─► { name: "Lydia" }
```
The object is still alive because `members[0]` references it.

Rule for notes:
- Variables hold **references** to objects.
- Setting one variable to `null` **doesn't delete the object** if another reference still exists.


###### Q. Tell Output
```js
const person = {
  name: "Lydia",
  age: 21,
};

for (const item in person) {
  console.log(item);
}
// Output:
// name
// age
```

Why?
- `for...in` iterates over an object's **keys (property names)**.
```js
item // "name", then "age"
```

To get the values:
```js
for (const key in person) {
  console.log(person[key]);
}
// Lydia
// 21
```

Rule for notes:
- `for...in` → iterates **keys** of an object.
- `for...of` → iterates **values** of an iterable (Array, String, Map, Set, etc.).

---
###### Q. Tell Output
```js
console.log(3 + 4 + "5"); // "75"
```

Why?
- `+` is evaluated **left to right**.
- `3 + 4` → `7`
- `7 + "5"` → `"75"` (string concatenation)

Rule for notes:
- `+` with a string converts the result to a **string**.
- Evaluation is **left to right**.

```js
3 + 4 + "5"   // "75"
"3" + 4 + 5   // "345"
3 + "4" + 5   // "345"
```

---
###### Q. Tell Output
```js
const num = parseInt("7*6", 10);
console.log(num); // 7
```
Why?
- `parseInt()` reads the string **from left to right**.
- It stops parsing when it encounters a non-digit (`*`).

```js
parseInt("7*6", 10); // 7
parseInt("123abc");  // 123
parseInt("abc123");  // NaN
```

Rule for notes:
- `parseInt(str, radix)` → Parses until the **first invalid character**.
- If the string doesn't start with a valid number → `NaN`.

---
###### Q. Tell Output
```js
const result = [1, 2, 3].map((num) => {
  if (typeof num === "number") return;
  return num * 2;
});
console.log(result); // [undefined, undefined, undefined]
```

Why?
- Every element (`1`, `2`, `3`) is a **number**.
- The `if` condition is always `true`, so `return;` executes.
- `return;` without a value returns `undefined`.

Rule for notes:
- `map()` returns a **new array**.
- If the callback returns nothing (`return;`), that element becomes `undefined`.

---
###### Q. Tell Output
```js
function getInfo(member, year) {
  member.name = "Lydia";
  year = "1998";
}
const person = { name: "Sarah" };
const birthYear = "1997";
getInfo(person, birthYear);
console.log(person, birthYear); // { name: "Lydia" } "1997"
```

Why?
- `member` references the **same object**, so changing `member.name` changes `person.name`.
- `year` is a **primitive (string)**. Reassigning it only changes the local parameter, not `birthYear`.

Rule for notes:
- **Objects** → Passed by **sharing/reference** (object properties can be modified).
- **Primitives** → Passed by **value** (reassigning doesn't affect the original variable).


###### Q. Tell Output
```js
function greeting() {
  throw "Hello world!";
}
function sayHi() {
  try {
    const data = greeting();
    console.log("It worked!", data);
  } catch (e) {
    console.log("Oh no an error:", e);
  }
}
sayHi(); // Oh no an error: Hello world!
```

Why?
- `throw` immediately stops execution of `greeting()`.
- Control jumps to the `catch` block.
- `e` contains the thrown value (`"Hello world!"`).

Rule for notes:
- `throw` → Raises an exception immediately.
- `try...catch` → Catches the thrown error/value and prevents the program from crashing.


###### Q. Tell Output
```js
function Car() {
  this.make = 'Lamborghini';
  return { make: 'Maserati' };
}
const myCar = new Car();
console.log(myCar.make);
```

Why?
- With `new`, JavaScript normally returns `this`.
- **But if the constructor explicitly returns an object, that object replaces `this`.**

```js
this.make = "Lamborghini";   // ignored
return { make: "Maserati" }; // returned instead
```

Rule for notes:
- Constructor returns **object** → returned object is used.
- Constructor returns **primitive** (`1`, `"hi"`, `true`, `null`, etc.) → ignored; `this` is returned.


###### Q. Tell Output
```js
(() => {
  let x = (y = 10);
})();

console.log(typeof x); // "undefined"
console.log(typeof y); // "number"
```

Why?
- `x` is declared with `let` inside the IIFE → **block-scoped**, inaccessible outside.
- `y = 10` has **no declaration** (`let`, `const`, `var`), so in **non-strict mode** it becomes a **global variable**.

Equivalent to:
```js
(() => {
  y = 10;     // global (non-strict mode)
  let x = y;  // local
})();
```

Rule for notes:
- `let`/`const` → Block-scoped.
- Assigning to an undeclared variable (`y = 10`) creates a **global variable** in **non-strict mode**.
- In **strict mode**, `y = 10` throws a `ReferenceError`.


###### Q. Tell Output
```js
class Dog {
  constructor(name) {
    this.name = name;
  }
}

Dog.prototype.bark = function () {
  console.log(`Woof I am ${this.name}`);
};

const pet = new Dog("Mara");

pet.bark(); // "Woof I am Mara"

delete Dog.prototype.bark;

pet.bark(); // TypeError: pet.bark is not a function
```

Why?
- `pet` doesn't have its own `bark` method.
- It finds `bark` through `Dog.prototype`.
- After `delete Dog.prototype.bark`, the method is removed from the prototype.
- Prototype lookup fails → `pet.bark` is `undefined`, so calling it throws a `TypeError`.

Rule for notes:
- Instances inherit methods from the **prototype**.
- Deleting a prototype method removes it for **all existing and future instances** (unless they have their own method).


###### Q. Tell Output
```js
const set = new Set([1, 1, 2, 3, 4]);
console.log(set); // Set(4) {1, 2, 3, 4}
```

Why?
- A `Set` stores **only unique values**.
- Duplicate `1` is ignored.

Rule for notes:
- `Set` → Stores **unique values only**.
- Duplicate values are automatically removed.


###### Q. Tell Output
```js
// counter.js
let counter = 10;
export default counter;
```

```js
// index.js
import myCounter from "./counter";
myCounter += 1; // ❌ TypeError
console.log(myCounter);
```

Why?
- Imported bindings are **read-only**.
- You **cannot reassign** an imported value.

Rule for notes:
- `import` → **Read-only binding**.
- You can **read** imported values, but **cannot reassign** them.

**Output:** `TypeError: Assignment to constant variable` (or equivalent read-only import error, depending on the environment).


###### Q. Tell Output
```js
const name = "Lydia";
age = 21;
console.log(delete name); // false
console.log(delete age);  // true (non-strict mode)
```

Why?
- `name` is declared with `const` → cannot be deleted.
- `age` is an undeclared assignment, so in **non-strict mode** it becomes a global property that **can** be deleted.

Rule for notes:
- `delete` removes **object properties**, not variables declared with `var`, `let`, or `const`.
- Undeclared globals (non-strict mode) → can be deleted.
- In **strict mode**, `age = 21` throws a `ReferenceError`.


###### Q. Tell Output
```js
const numbers = [1, 2, 3, 4, 5];
const [y] = numbers;
console.log(y); // 1
```

Why?
- Array destructuring assigns elements by **position**.
- `y` gets the **first** element.

Equivalent to:
```js
const y = numbers[0];
```

Rule for notes:
- `[a, b] = arr` → `a = arr[0]`, `b = arr[1]`.
- Array destructuring is **position-based**.


###### Q. Tell Output
```js
const user = { name: 'Lydia', age: 21 };
const admin = { admin: true, ...user };
console.log(admin); // { admin: true, name: "Lydia", age: 21 }
```

Why?
- `...user` copies all **own enumerable properties** from `user` into `admin`.
- `admin: true` is added as another property.

Rule for notes:
- Object spread (`...obj`) → creates a **shallow copy** of an object's properties.
- If duplicate keys exist, **later properties overwrite earlier ones**.

```js
const obj = { a: 1 };
const copy = { a: 2, ...obj }; // { a: 1 }
const copy2 = { ...obj, a: 2 }; // { a: 2 }
```


###### Q. Tell Output
```js
const person = { name: "Lydia" };
Object.defineProperty(person, "age", { value: 21 });
console.log(person); // { name: "Lydia", age: 21 }
console.log(Object.keys(person)); // ["name"]
```

Why?
- `Object.defineProperty()` creates properties that are **non-enumerable by default**.
- `Object.keys()` returns **only enumerable** properties.

Equivalent to:
```js
Object.defineProperty(person, "age", {
  value: 21,
  enumerable: false, // default
});
```

To make it appear in `Object.keys()`:
```js
Object.defineProperty(person, "age", {
  value: 21,
  enumerable: true,
});
```

Rule for notes:
- `Object.keys()` → returns **enumerable** own properties only.
- `Object.defineProperty()` defaults:
    - `enumerable: false`
    - `writable: false`
    - `configurable: false`

Think of **enumerable** as **"visible during property iteration."**
**Non-enumerable Property**
- Exists on the object.
- You can access it normally.
- It is hidden from iteration.

Object
├── name (enumerable)      ✅ visible
└── age  (non-enumerable)  👻 hidden from loops

| Operation         | Enumerable | Non-enumerable |
| ----------------- | ---------- | -------------- |
| `obj.prop`        | ✅          | ✅              |
| `Object.keys()`   | ✅          | ❌              |
| `for...in`        | ✅          | ❌              |
| `{ ...obj }`      | ✅          | ❌              |
| `Object.assign()` | ✅          | ❌              |


###### Q. Tell Output
```js
let num = 10;
const increaseNumber = () => num++;
const increasePassedNumber = number => number++;
const num1 = increaseNumber();
const num2 = increasePassedNumber(num1);
console.log(num1); // 10
console.log(num2); // 10
```

Why?
- `num++` is **post-increment**: returns the current value, then increments.
- `increaseNumber()` returns `10`, but `num` becomes `11`.
- `increasePassedNumber(10)` returns `10`; `number` becomes `11` locally only.

Step by step:
```js
num = 10
num1 = num++;      // returns 10, num = 11
num2 = number++;   // returns 10, local number = 11
```

Rule for notes:
- `x++` → return first, increment later.
- Function parameters are local variables; incrementing a primitive parameter does not affect the original value.


###### Q. Tell Output
```js
const value = { number: 10 };
const multiply = (x = { ...value }) => {
  console.log((x.number *= 2));
};
multiply();       // 20
multiply();       // 20
multiply(value);  // 20
multiply(value);  // 40
```
Why?
- Default parameter `{ ...value }` creates a **new copy** each call.
- Passing `value` uses the **same object**, so it gets modified.

Step by step:
```js
multiply();       // copy {10} → {20}
multiply();       // new copy {10} → {20}
multiply(value);  // value {10} → {20}
multiply(value);  // same value {20} → {40}
```

Rule for notes:
- Default object parameter with `...` → **new shallow copy every call**.
- Passing an object directly → **same reference**, changes persist.


###### Q. Tell Output
```js
[1, 2, 3, 4].reduce((x, y) => console.log(x, y));
```
Output:
```text
1 2
undefined 3
undefined 4
```

Why?
- No initial accumulator is provided, so:
    - `x = 1`, `y = 2` on the first iteration.
- `console.log()` returns `undefined`.
- That `undefined` becomes the accumulator for the next iteration.

Step by step:
```text
x = 1,         y = 2  → console.log() → returns undefined
x = undefined, y = 3
x = undefined, y = 4
```

Rule for notes:
- `reduce()` uses the callback's **return value** as the next accumulator.
- If no initial value is provided, the **first array element** is the initial accumulator.


###### Q.  With which constructor can we successfully extend the Dog class?
```js
class Dog {
  constructor(name) {
    this.name = name;
  }
};
class Labrador extends Dog {
  // 1
  constructor(name, size) {
    this.size = size;
  }
  // 2
  constructor(name, size) {
    super(name);
    this.size = size;
  }
  // 3
  constructor(size) {
    super(name);
    this.size = size;
  }
  // 4
  constructor(name, size) {
    this.name = name;
    this.size = size;
  }
};
```


```js
class Dog {
  constructor(name) {
    this.name = name;
  }
}

class Labrador extends Dog {
  constructor(name, size) {
    super(name);      // ✅ must be called first
    this.size = size;
  }
}
```

Why?
- In a derived class (`extends`), you **must call `super()` before using `this`**.

Why others are wrong?
❌ **1**

```js
constructor(name, size) {
  this.size = size;
}
```

Uses `this` before `super()`.
❌ **3**

```js
constructor(size) {
  super(name);
}
```
`name` is not defined.

❌ **4**

```js
constructor(name, size) {
  this.name = name;
  this.size = size;
}
```
Uses `this` before `super()`.

Rule for notes:
- In a subclass (`extends`), **`super()` must be the first statement in the constructor before accessing `this`**.


###### Q. Tell Output
```js
// index.js
console.log('running index.js');
import { sum } from './sum.js';
console.log(sum(1, 2));

// sum.js
console.log('running sum.js');
export const sum = (a, b) => a + b;
```

Output:
```text
running sum.js
running index.js
3
```

Why?
- ES Modules load and execute **imports first**, before running the rest of the importing file.
- So `sum.js` executes before `index.js`.

Execution order:
```text
1. Load index.js
2. Execute sum.js
   → "running sum.js"
3. Continue index.js
   → "running index.js"
4. sum(1, 2)
   → 3
```

Rule for notes:
- **ES Modules are hoisted**: imported modules execute **before** the rest of the importing module's code.


###### Q. Tell Output
```js
console.log(Number(2) === Number(2));         // true
console.log(Boolean(false) === Boolean(false)); // true
console.log(Symbol("foo") === Symbol("foo"));   // false
```

Why?
- `Number(2)` → returns primitive `2`.
- `Boolean(false)` → returns primitive `false`.
- `Symbol("foo")` → creates a **new unique symbol every time**.

Rule for notes:
- `Number()` and `Boolean()` return **primitive values**.
- Every call to `Symbol()` returns a **unique value**, even with the same description.


###### Q. Tell Output
```js
const name = "Lydia Hallie";
console.log(name.padStart(13)); // " Lydia Hallie"
console.log(name.padStart(2));  // "Lydia Hallie"
```

Why?
- `"Lydia Hallie"` has **12 characters**.
- `padStart(targetLength)` only pads if `targetLength` is **greater than** the string length.
- `13` and `2` are **not greater than 12** in the way needed to add padding? Actually:
    - Length = **12**
    - `padStart(13)` **is greater**, so it adds **1 leading space**.
    - `padStart(2)` is smaller, so it returns the original string.

Correct output:
```text
" Lydia Hallie"  // one leading space
"Lydia Hallie"
```

Rule for notes:
- `padStart(n, padString = " ")` → Pads the **start** until the string reaches length `n`.
- If `n <= string.length`, the original string is returned unchanged.


###### Q. Tell Output
```js
console.log("🥑" + "💻"); // "🥑💻"
```
Why?
- `+` between strings performs **string concatenation**.
- Emojis are just Unicode characters in strings.

Rule for notes:
- `+` with two strings → concatenates them.

```js
"Hello" + " World"; // "Hello World"
"🥑" + "💻";         // "🥑💻"
```


###### How can we log the values that are commented out after the console.log statement?
```js
function* startGame() {
  const answer = yield "Do you love JavaScript?";

  if (answer !== "Yes") {
    return "Oh wow... Guess we're done here";
  }

  return "JavaScript loves you back ❤️";
}

const game = startGame();

console.log(game.next().value);       // Do you love JavaScript?
console.log(game.next("Yes").value);  // JavaScript loves you back ❤️
```

Why?
- `game.next()` starts the generator and returns the first `yield`.
- `game.next("Yes")` sends `"Yes"` back to `answer`, so the generator returns the final message.

Rule for notes:
- First `next()` → starts the generator and runs until the first `yield`.
- Next `next(value)` → sends `value` to the paused `yield` expression and resumes execution.


###### Q. Tell Output
```js
console.log(String.raw`Hello\nworld`);
// Hello\nworld
```

Why?
- `String.raw` is a **tagged template literal**.
- It returns the **raw string**, without interpreting escape sequences like `\n`.

Compare:
```js
console.log(`Hello\nworld`);
// Hello
// world

console.log(String.raw`Hello\nworld`);
// Hello\nworld
```

Rule for notes:
- `` `...` `` → escape sequences are interpreted.
- `String.raw\`...``→ returns the **raw string**, keeping escapes like`\n`,` \t`, etc. literally.


###### Q. Tell Output
```js
async function getData() {
  return await Promise.resolve("I made it!");
}
const data = getData();
console.log(data);
// Promise { <pending> }
```

Why?
- An `async` function **always returns a Promise**.
- `await` resolves the promise **inside** the function, but the function itself still returns a Promise.

To get the value:
```js
getData().then(console.log);// I made it!

// or
const data = await getData();
console.log(data); // I made it!
```

Rule for notes:
- `async` → always returns a **Promise**.
- `await` unwraps a Promise **only inside an async function**.


###### Q. Tell Output
```js
function addToList(item, list) {
  return list.push(item);
}

const result = addToList("apple", ["banana"]);
console.log(result); // 2
```

Why?
- `push()` **modifies the array** and returns the **new length**, **not** the array.

```js
["banana"].push("apple"); // returns 2
```

The array becomes:
```js
["banana", "apple"]
```
…but `result` stores the return value of `push()`, which is `2`.

Rule for notes:
- `array.push(item)` → Adds item to the end and returns the **new array length**.


###### Q. Tell Output
```js
const box = { x: 10, y: 20 };
Object.freeze(box);
const shape = box;
shape.x = 100;
console.log(shape); // { x: 10, y: 20 }
```

**Why?
- `shape` and `box` reference the **same object**.
- `Object.freeze()` makes the object **immutable** (cannot add, delete, or modify properties).
- `shape.x = 100` fails silently in non-strict mode (throws `TypeError` in strict mode).

Rule for notes:
- `Object.freeze(obj)` → Prevents **adding, deleting, or modifying** properties.
- Freeze is **shallow** (nested objects can still be modified).


###### Q. Tell Output
```js
const { firstName: myName } = { firstName: "Lydia" };
console.log(firstName); // ReferenceError
```

Why?
- `firstName: myName` means:
    - Read the property `firstName`.
    - Store it in a variable named `myName`.
- No variable named `firstName` is created.

```js
console.log(myName);    // "Lydia"
console.log(firstName); // ReferenceError
```



###### Q. Is this a pure function?
```js
function sum(a, b) {
  return a + b;
}
```
**Answer:** ✅ **Yes**
- Same inputs → always same output.
- No side effects (doesn't modify anything outside the function).

- A **pure function**:
    1. Returns the **same output** for the same inputs.
    2. Has **no side effects** (no mutation, no I/O, no global state changes).



###### Q. Tell Output
```js
const myLifeSummedUp = ["☕", "💻", "🍷", "🍫"];

for (let item in myLifeSummedUp) {
  console.log(item);
}
// 0
// 1
// 2
// 3

for (let item of myLifeSummedUp) {
  console.log(item);
}
// ☕
// 💻
// 🍷
// 🍫
```

Why?
- `for...in` iterates over **keys (indexes)**.
- `for...of` iterates over **values**.

Rule for notes:
- `for...in` → Object keys / Array indexes.
- `for...of` → Iterable values (arrays, strings, sets, maps).

```js
for (const i in arr)  // i = 0, 1, 2...
for (const v of arr)  // v = actual values
```



###### Q. Tell Output
```js
const list = [1 + 2, 1 * 2, 1 / 2];
console.log(list); // [3, 2, 0.5]
```


###### Q. Tell Output
```js
function sayHi(name) {
  return `Hi there, ${name}`;
}
console.log(sayHi()); // "Hi there, undefined"
```

Why?
- No argument is passed.
- Missing parameters are `undefined`.
- Template literals convert `undefined` to the string `"undefined"`.

Rule for notes:
- Missing function arguments → parameter value is `undefined`.
- Template literals convert values to strings automatically.

```js
sayHi();      // "Hi there, undefined"
sayHi("Tom"); // "Hi there, Tom"
```


###### Q. Tell Output
```js
function sayHi(name) {
  return `Hi there, ${name}`;
}
console.log(sayHi());// "Hi there, undefined"
```


###### Q. Tell Output
```js
var status = "😎";

setTimeout(() => {
  const status = "😍";

  const data = {
    status: "🥑",
    getStatus() {
      return this.status;
    },
  };

  console.log(data.getStatus());          // 🥑
  console.log(data.getStatus.call(this)); // 😎 (browser)
}, 0);
```

Why?
- `data.getStatus()` → `this` is `data` → returns `"🥑"`.
- `call(this)` sets `this` to the callback's `this`.
- In a **browser (non-module script)**, the arrow function inherits the global `this` (`window`), and `var status` becomes `window.status = "😎"`.

If this code runs as an **ES module** or in **Node.js**, the second output is different because `this` is **not** the global object.

Rule for notes:
- `obj.method()` → `this = obj`.
- `method.call(obj)` → `this = obj` explicitly.
- Arrow functions **don't have their own `this`**; they inherit it from the surrounding scope.


###### Q. Tell Output
```js
const person = {
  name: "Lydia",
  age: 21,
};

let city = person.city; // undefined
city = "Amsterdam";

console.log(person); // { name: "Lydia", age: 21 }
```


###### Q. Tell Output
```js
function checkAge(age) {
  if (age < 18) {
    const message = "Sorry, you're too young.";
  } else {
    const message = "Yay! You're old enough!";
  }
  return message;
}
console.log(checkAge(21)); // ReferenceError
```
`const` is **block-scoped**.


###### What kind of information would get logged?
```js
fetch('https://www.website.com/api/user/1')
  .then(res => res.json())
  .then(res => console.log(res));
```
The value of `res` in the second `.then` is equal to the returned value of the previous `.then`. You can keep chaining `.then`s like this, where the value is passed to the next handler.



###### Which option is a way to set hasName equal to true, provided you cannot pass true as an argument?
```js
function getName(name) {
  const hasName = //
}
```

The expected answer is:
```js
function getName(name) {
  const hasName = !!name;
}
```

or equivalently:
```js
const hasName = Boolean(name);
```

Why?
- `!!` converts any value to a boolean.
- Since you **cannot pass `true` directly**, pass a truthy value (e.g. `"Lydia"`, `1`, `{}`, `[]`) and `!!` converts it to `true`

Examples:
```js
!!"Lydia"   // true
!!1         // true
!!{}        // true
!![]        // true

!!""        // false
!!0         // false
!!null      // false
!!undefined // false
```

Rule for notes:
- `!!value` → converts any value to a boolean.
- Truthy → `true`, Falsy → `false`.


###### Q. Tell Output
```js
console.log("I want pizza"[0]); // "I"
```

Why?
- Strings are **array-like**.
- You can access characters using their **index**.
- Indexing starts at `0`.

```js
"I want pizza"
 0123456789...
 ^
 index 0 = "I"
```

Rule for notes:
- `str[index]` → returns the character at that index.
- Strings are **immutable**, but individual characters can be read using indexing.


###### Q. Tell Output
```js
function sum(num1, num2 = num1) {
  console.log(num1 + num2);
}
sum(10); // 20
```


###### Q. Tell Output
```js
function sum(num2 = num1, num1) {
  console.log(num1 + num2);
}
sum(10); // NaN
```

Why?
- `sum(10)` passes `10` as the **first parameter** (`num2`).
- Since `num2` is provided, its default value (`num1`) is **never evaluated**.
- `num1` is not passed, so it is `undefined`.

So:
```js
num2 = 10;
num1 = undefined;

undefined + 10 // NaN
```


###### Q. Tell Output
```js
function sum(num2 = num1, num1) {
  console.log(num1 + num2);
}
sum(undefined, 10);
```
ReferenceError: Cannot access 'num1' before initialization

A default parameter is evaluated whenever the argument is `undefined`.


###### Q. Tell Output
```js
// module.js
export default () => 'Hello world';
export const name = 'Lydia';

// index.js
import * as data from './module';

console.log(data);
```

Output:
```js
{
  default: () => "Hello world",
  name: "Lydia"
}
```

Why?
- `import * as data` imports **all exports** into a **module namespace object**.
- The **default export** is available as `data.default`.
- Named exports are available by their names.

```js
data.default(); // "Hello world"
data.name;      // "Lydia"
```

Rule for notes:
- `import * as obj from "./module"` →
    - `obj.default` → default export.
    - `obj.namedExport` → named exports.


###### Q. Tell Output
```js
class Person {
  constructor(name) {
    this.name = name;
  }
}
const member = new Person("John");
console.log(typeof member); // "object"
```

Why?
- `new Person()` creates an **object instance** of `Person`.
- `typeof` returns `"object"` for all object instances.

```js
typeof {}              // "object"
typeof []              // "object"
typeof new Person()    // "object"
```

Rule for notes:
- `typeof` an instance created with `new` → `"object"`.
- `typeof ClassName` (the class itself) → `"function"`.


###### Q. Tell Output
```js
let newList = [1, 2, 3].push(4);
console.log(newList.push(5));
```

Output:
```text
TypeError: newList.push is not a function
```

Why?
- `push()` returns the **new array length**, not the array.
- So:

```js
let newList = [1, 2, 3].push(4);
// newList = 4
```

Then:
```js
4.push(5); // ❌ Numbers don't have a push() method
```

Rule for notes:
- `array.push(item)` → modifies the array and returns the **new length**.
- If you need the updated array:

```js
const arr = [1, 2, 3];
arr.push(4);
console.log(arr); // [1, 2, 3, 4]
```



###### Q. Tell Output
```js
function giveLydiaPizza() {
  return "Here is pizza!";
}

const giveLydiaChocolate = () =>
  "Here's chocolate... now go hit the gym already.";

console.log(giveLydiaPizza.prototype);      // {}
console.log(giveLydiaChocolate.prototype);  // undefined
```

Why?
- Regular functions have a `prototype` property because they can be used with `new`.
- Arrow functions **cannot** be used as constructors, so they **don't have a `prototype` property**.

```js
new giveLydiaPizza();      // ✅
new giveLydiaChocolate();  // ❌ TypeError
```

Rule for notes:
- Regular function → has `.prototype`.
- Arrow function → `.prototype` is `undefined` (not a constructor).



When you use `new`, JavaScript treats the function as a **constructor**. It creates a new object and sets up the prototype chain.

Example
```js
function Person(name) {
  this.name = name;
}

const p = new Person("Lydia");

console.log(p); // Person { name: "Lydia" }
```

What `new Person("Lydia")` does behind the scenes:

```js
// Roughly equivalent to:
const obj = {};                     // 1. Create a new empty object
obj.__proto__ = Person.prototype;   // 2. Link prototype
Person.call(obj, "Lydia");          // 3. Execute function with this = obj
return obj;                         // 4. Return the object
```

So:
```js
function giveLydiaPizza() {
  return "Here is pizza!";
}
const pizza = new giveLydiaPizza();
console.log(pizza); // giveLydiaPizza {}
```

**Why not `"Here is pizza!"`?**
Because when a constructor returns a **primitive** (`string`, `number`, `boolean`, etc.), JavaScript **ignores it** and returns the newly created object instead.

If it returns an **object**, that object replaces the newly created one:
```js
function Person() {
  this.name = "John";
  return { age: 25 };
}
const p = new Person();
console.log(p); // { age: 25 }
```



###### Q. Tell Output
```js
const person = {
  name: "Lydia",
  age: 21,
};
for (const [x, y] of Object.entries(person)) {
  console.log(x, y);
}
// Output:
// name Lydia
// age 21
```

Why?
- `Object.entries(person)` returns an array of `[key, value]` pairs.

```js
Object.entries(person);
// [
//   ["name", "Lydia"],
//   ["age", 21]
// ]
```

- Destructuring:
```js
const [x, y] = ["name", "Lydia"];
// x = "name"
// y = "Lydia"
```

Rule for notes:
- `Object.entries(obj)` → `[[key1, value1], [key2, value2], ...]`
- `for (const [key, value] of Object.entries(obj))` → iterate over **keys and values** simultaneously.



###### Q. Tell Output
```js
function getItems(fruitList, ...args, favoriteFruit) {
  return [...fruitList, ...args, favoriteFruit];
}
getItems(["banana", "apple"], "pear", "orange");
```
**Answer:** ❌ **SyntaxError**

**Why?**
- The **rest parameter (`...args`) must be the last parameter** in the function.
- You cannot have `favoriteFruit` after `...args`.

❌ Invalid:
```js
function fn(a, ...rest, b) {}
```

✅ Valid:
```js
function fn(a, b, ...rest) {}
```
or
```js
function fn(a, ...rest) {}
```

Rule for notes:
- `...rest` **must always be the last parameter** in a function definition. Otherwise, JavaScript throws a **SyntaxError**.


###### Q. Tell Output
```js
function nums(a, b) {
  if (a > b) console.log("a is bigger");
  else console.log("b is bigger");
  return
  a + b;
}
console.log(nums(4, 2));
console.log(nums(1, 2));
//Output:
// a is bigger
// undefined
// b is bigger
// undefined
```
Why?
* JavaScript automatically inserts a semicolon after `return` (**ASI - Automatic Semicolon Insertion**).

It becomes:
```js
return;
a + b; // Never executes
```
So the function always returns `undefined`.

Correct way:
```js
return a + b;
```
or
```js
return (
  a + b
);
```

Rule for notes:
* Never put the return value on the next line after `return`.
* `return` followed by a newline → JavaScript inserts `;`, so the function returns `undefined`.


###### Q. Tell Output
```js
class Person {
  constructor() {
    this.name = 'Lydia';
  }
}
Person = class AnotherPerson {
  constructor() {
    this.name = 'Sarah';
  }
};
const member = new Person();
console.log(member.name); // "Sarah"
```

Why?
- `Person` is a variable that initially refers to the first class.
- It is then **reassigned** to `AnotherPerson`.
- `new Person()` now creates an instance of `AnotherPerson`.

Rule for notes:
- A class declaration creates a variable.
- If the variable is reassigned, `new ClassName()` uses the **new class**, not the original one.

```js
Person = AnotherPerson;
new Person(); // creates AnotherPerson instance
```


###### Q. Tell Output
```js
const info = {
  [Symbol("a")]: "b",
};
console.log(info); // { [Symbol(a)]: "b" }
console.log(Object.keys(info)); // []
```

Why?
- The property key is a **Symbol**, not a string.
- `Object.keys()` returns **only enumerable string keys**, so it ignores Symbol keys.

To get Symbol keys:
```js
Object.getOwnPropertySymbols(info); // [Symbol(a)]
```

Rule for notes:
- `Object.keys(obj)` → returns **string keys only**.
- `Object.getOwnPropertySymbols(obj)` → returns **Symbol keys**.


###### Q. Tell Output
```js
const getList = ([x, ...y]) => [x, y]
const getUser = user => { name: user.name, age: user.age }

const list = [1, 2, 3, 4]
const user = { name: "Lydia", age: 21 }

console.log(getList(list))
console.log(getUser(user))
// Output:
// [1, [2, 3, 4]]
// undefined
```

Why?
`getList(list)`
```js
[x, ...y] = [1, 2, 3, 4];
```
- `x = 1`
- `y = [2, 3, 4]`

Returns: `[1, [2, 3, 4]]`


`getUser(user)`
```js
const getUser = user => { name: user.name, age: user.age };
```
This is **not** returning an object.
JavaScript treats `{}` as the **function body**, not an object literal. ```

There is no `return`, so it returns `undefined`.

Correct way
```js
const getUser = user => ({
  name: user.name,
  age: user.age,
});
```

Rule for notes
- Arrow function:
    - `() => ({})` → returns an object.
    - `() => {}` → function body; requires `return`.


###### Q. Tell Output
```js
const name = 'Lydia';
console.log(name()); // TypeError: name is not a function
```


###### Q. Tell Output
```js
const output = `${[] && 'Im'}possible!
You should${'' && `n't`} see a therapist after so much JavaScript lol`;
```

Output:
```text
Impossible!
You should see a therapist after so much JavaScript lol
```

Why?
1.`[] && 'Im'`
- `[]` is **truthy**.
- `&&` returns the **second operand** if the first is truthy.

 2.`'' && "n't"`
- `""` is **falsy**.
- `&&` returns the **first falsy operand**.

Rule for notes
- `a && b`
    - If `a` is **truthy** → returns `b`.
    - If `a` is **falsy** → returns `a`.

Examples:
```js
[] && "Im";     // "Im"
"" && "n't";    // ""
0 && "hello";   // 0
true && 123;    // 123
```


###### Q. Tell Output
```js
const one = false || {} || null;
const two = null || false || '';
const three = [] || 0 || true;
console.log(one, two, three);
```

Output
```text
{} "" []
```

 Why?
1. `false || {} || null`
- `||` returns the **first truthy value**
- `false` → falsy → skip
- `{}` → truthy → returned

So:
```js
one = {}
```


2. `null || false || ''`
All are falsy except empty string is also falsy:
- `null` → falsy
- `false` → falsy
- `''` → falsy → last value returned

So: `two = ""`

3. `[] || 0 || true`
- `[]` is **truthy in JS** (important trap)
- So evaluation stops immediately

So: `three = []`

Rule (important)
- `||` returns **first truthy value**
- If none → returns **last value**
- Arrays and objects are **always truthy**, even if empty

```js
[]  // truthy
{}  // truthy
""  // falsy
0   // falsy
null // falsy
```



###### Q. Tell Output
```js
const myPromise = () => Promise.resolve("I have resolved!");

function firstFunction() {
  myPromise().then(res => console.log(res));
  console.log("second");
}

async function secondFunction() {
  console.log(await myPromise());
  console.log("second");
}

firstFunction();
secondFunction();
```

Output (order matters)
```text
second
I have resolved!
I have resolved!
second
```
Why?
1. `firstFunction()`
```js
myPromise().then(...)
console.log("second")
```
- `then()` is async → goes to **microtask queue**
- `console.log("second")` runs immediately
So: second
Later microtask runs: I have resolved!

2. `secondFunction()`
```js
console.log(await myPromise());
console.log("second");
```
- `await` pauses function execution
- resumes in **microtask queue**

So it prints:

I have resolved!
second

Key rule (important)
- `console.log()` → synchronous
- `.then()` → microtask (async)
- `await` → pauses function, resumes in microtask


###### Q. Tell Output
```js
const set = new Set();
set.add(1);
set.add("Lydia");
set.add({ name: "Lydia" });

for (let item of set) {
  console.log(item + 2);
}
```
Output:
```text
3
Lydia2
[object Object]2
```

Why?
1. **Number** `1 + 2 // 3`
2. **String** `"Lydia" + 2 // "Lydia2"`
`+` with a string performs **string concatenation**.

3. **Object** `{ name: "Lydia" } + 2`
The object is converted to a string first: `String({ name: "Lydia" }) // "[object Object]"`

So:
`"[object Object]" + 2`
`// "[object Object]2"`

Rule for notes
- `+` operator:
    - Number + Number → addition.
    - If **either operand is a string** (or becomes one), it performs **string concatenation**.
    - Objects are coerced to strings (`"[object Object]"`) unless they define custom conversion methods.



###### Q. Tell Output
```js
Promise.resolve(5);
```
What it does:
- Creates a **fulfilled Promise** with the value `5`.

Equivalent to:
```js
new Promise(resolve => resolve(5));
```

Examples: `Promise.resolve(5).then(console.log); // 5`

```js
const p = Promise.resolve(5);
console.log(p);
// Promise {<fulfilled>: 5}
```

With `await`:
```js
const value = await Promise.resolve(5);
console.log(value); // 5
```

Rule for notes:
- `Promise.resolve(value)` → returns an **already fulfilled Promise** containing `value`.
- If `value` is already a Promise, it simply returns that Promise.


###### Q. Tell Output
```js
function compareMembers(person1, person2 = person) {
  if (person1 !== person2) {
    console.log('Not the same!');
  } else {
    console.log('They are the same!');
  }
}
const person = { name: 'Lydia' };
compareMembers(person);
```

Output:
```text
They are the same!
```

Why?
When you call:

```js
compareMembers(person);
```
- `person1` receives the `person` object.
- `person2` is not provided, so its default value is `person`.

So it's effectively:
```js
person1 = person;
person2 = person;
```
Both variables reference the **same object in memory**.
```js
person1 === person2 // true
```
Therefore:
```js
person1 !== person2 // false
```
and the `else` block runs.

Rule for notes
- Objects are compared by **reference**, not by content.
- Two variables referencing the **same object** are equal with `===`.


###### Q. Tell Output
```js
const colorConfig = {
  red: true,
  blue: false,
  green: true,
  black: true,
  yellow: false,
};
const colors = ["pink", "red", "blue"];
console.log(colorConfig.colors[1]); // TypeError: Cannot read properties of undefined (reading '1')

console.log(colorConfig[colors[0]]); // undefined
console.log(colorConfig[colors[1]]); // true
console.log(colorConfig[colors[1]]); // false
```

Why?
`colorConfig` is:

```js
{
  red: true,
  blue: false,
  green: true,
  black: true,
  yellow: false
}
```
It **does not have** a property named `colors`.

So:
```js
colorConfig.colors
// undefined
```
Then JavaScript tries to do:
```js
undefined[1]
```
which throws a **TypeError**.

If the intention was:
```js
console.log(colorConfig[colors[1]]);
```
Then:
```js
colors[1] // "red"
colorConfig["red"] // true
```

Output:
```text
true
```

Rule for notes
- `obj.prop` → accesses a property literally named `"prop"`.
- `obj[key]` → accesses the property whose name is stored in `key`.
```js
const key = "red";
obj.key;    // looks for "key"
obj[key];   // looks for "red"
```


###### Q. Tell Output
```js
console.log('❤️' === '❤️'); // true
```


###### Q. Which of these methods modifies the original array?
```js
const emojis = ["✨", "🥑", "😍"];

emojis.map(x => x + "✨");              // ❌ New array
emojis.filter(x => x !== "🥑");         // ❌ New array
emojis.find(x => x !== "🥑");           // ❌ Returns one element
emojis.reduce((acc, cur) => acc + "✨");// ❌ Returns a value
emojis.slice(1, 2, "✨");               // ❌ New array
emojis.splice(1, 2, "✨");              // ✅ Modifies original array
```

Output after `splice`
```js
const emojis = ["✨", "🥑", "😍"];
emojis.splice(1, 2, "✨");
console.log(emojis);
// ["✨", "✨"]
```

Why?
- Starts at index `1`.
- Removes `2` elements (`🥑`, `😍`).
- Inserts `"✨"`.


###### Q. Tell Output
```js
const food = ['🍕', '🍫', '🥑', '🍔'];
const info = { favoriteFood: food[0] };
info.favoriteFood = '🍝';
console.log(food);
```

Output:
```js
['🍕', '🍫', '🥑', '🍔']
```

Why?
```js
const info = {
  favoriteFood: food[0]
};
```
`food[0]` is the **string** `"🍕"`.
So:
```js
info.favoriteFood = "🍕";
```

`favoriteFood` gets a **copy of the string value**, not a reference to the array element.

When you do:
```js
info.favoriteFood = "🍝";
```
you're only changing the property in `info`, **not** `food[0]`.



###### Q. Tell Output
```js
let name = 'Lydia';
function getName() {
  console.log(name);
  let name = 'Sarah';
}
getName();
```

Output
```text
ReferenceError: Cannot access 'name' before initialization
```

Why?
When `getName()` starts executing, JavaScript creates a **local** variable `name` because of:

```js
let name = 'Sarah';
```
This local `name` **shadows** the global `name`.
Before this line executes, the local `name` is in the **Temporal Dead Zone (TDZ)**.

Execution order:
```js
function getName() {
  // local `name` exists but is uninitialized (TDZ)
  console.log(name); // ❌ ReferenceError
  let name = 'Sarah'; // initialized here
}
```
JavaScript **does not** look at the global `name` because a local `name` already exists in the current scope.

Rule for notes
- `let` and `const` are **hoisted** but remain in the **Temporal Dead Zone** until their declaration is reached.
- A local variable **shadows** an outer variable, even before it is initialized.
- Accessing a `let`/`const` variable during its TDZ throws a **ReferenceError**.


###### Q. Tell Output
```js
function* generatorOne() {
  yield ['a', 'b', 'c'];
}
function* generatorTwo() {
  yield* ['a', 'b', 'c'];
}
const one = generatorOne();
const two = generatorTwo();
console.log(one.next().value);
console.log(two.next().value);
```

Output
```js
['a', 'b', 'c']
'a'
```

Why?
`yield`
```js
function* generatorOne() {
  yield ['a', 'b', 'c'];
}
```

`yield` returns the **entire array as one value**.
```js
one.next(); // { value: ['a', 'b', 'c'], done: false }
```

`yield*`
```js
function* generatorTwo() {
  yield* ['a', 'b', 'c'];
}
```
`yield*` delegates to another **iterable**.
The array is iterable, so it yields each element one by one.
```js
two.next(); // { value: 'a', done: false }
two.next(); // { value: 'b', done: false }
two.next(); // { value: 'c', done: false }
```

Rule for notes
- `yield value` → yields **one value**.
- `yield* iterable` → yields **every value from the iterable** one by one.
```js
yield [1, 2];   // → [1, 2]
yield* [1, 2];  // → 1, then 2
```



###### Q. Tell Output
```js
console.log(`${(x => x)('I love')} to program`); // I love to program
```

Why?
Inside the template literal:
```js
(x => x)("I love")
```
This is an **immediately invoked arrow function**.

Equivalent to:
```js
const fn = x => x;
fn("I love"); // "I love"
```
The arrow function simply returns its argument.
So the template literal becomes:
```js
`${"I love"} to program`
```
Result:
```text
I love to program
```
Rule for notes
- Arrow functions can be **immediately invoked** by wrapping them in parentheses:

```js
(x => x * 2)(5); // 10
```
This is the arrow-function equivalent of an IIFE.


###### Q. Tell Output
```js
let config = {
  alert: setInterval(() => {
    console.log("Alert!");
  }, 1000),
};
config = null;
```

What happens?
The program prints:
```text
Alert!
Alert!
Alert!
...
```
every second, **even after**:
```js
config = null;
```

Why?
`setInterval()` creates a timer managed by the browser (or Node.js). It returns an **interval ID**.
```js
const id = setInterval(...);
```
In your code:
```js
config.alert = id;
```
Later:
```js
config = null;
```
This only removes your reference to the object. The interval itself is **still registered with the event loop**, so it continues executing.
To stop it
You must call:
```js
clearInterval(id);
```
or
```js
clearInterval(config.alert);
```
before losing the reference.

Rule for notes
- `setInterval()` keeps running until `clearInterval(intervalId)` is called.
- Setting an object containing the interval ID to `null` **does not stop the timer**. The timer is independent of your variable.


###### Q. Tell Output
```js
const myMap = new Map();
const myFunc = () => 'greeting';

myMap.set(myFunc, 'Hello world!');

// 1
myMap.get('greeting');
// 2
myMap.get(myFunc);
// 3
myMap.get(() => 'greeting');
```

Output
```js
// 1
undefined
// 2
"Hello world!"
// 3
undefined
```

Why?
A `Map` compares keys using **reference equality** for objects and functions.

You stored the key:
```js
myMap.set(myFunc, "Hello world!");
```
The key is **the function object itself**, **not** its return value.

1.
```js
myMap.get("greeting");
```
You're looking up a **string**, but the key is a **function**.
```js
undefined
```

 2.
```js
myMap.get(myFunc);
```
This is the **exact same function reference** used in `set()`.
```js
"Hello world!"
```

3.
```js
myMap.get(() => "greeting");
```
Although this arrow function has the same code, it is a **new function object**.
```js
myFunc === (() => "greeting"); // false
```
So:
```js
undefined
```

Visualization
```js
const f1 = () => "greeting";
const f2 = () => "greeting";

f1 === f2; // false
```

```
Map
┌──────────────────────────────┐
│ key: myFunc ───────────────┐ │
│ value: "Hello world!"      │ │
└────────────────────────────┼─┘
                             │
myMap.get(myFunc) ───────────┘ ✅

myMap.get("greeting")         ❌
myMap.get(() => "greeting")   ❌ (different function reference)
```

Rule for notes
- `Map` stores object/function keys **by reference**, not by value.
- Two functions with identical code are **different keys** unless they are the same function object.

```js
const f = () => {};
map.set(f, 1);
map.get(f);        // 1
map.get(() => {}); // undefined
```



###### Q. Tell Output
```js
const person = {
  name: 'Lydia',
  age: 21,
};
const changeAge = (x = { ...person }) => (x.age += 1);
const changeAgeAndName = (x = { ...person }) => {
  x.age += 1;
  x.name = 'Sarah';
};
changeAge(person);
changeAgeAndName();
console.log(person); // { name: "Lydia", age: 22 }
```

Why?
Initial object `person // { name: "Lydia", age: 21 }`

First call
```js
changeAge(person);
```
You **pass `person` explicitly**, so the default value is **not used**.
```js
x === person // true
```
The function does:
```js
x.age += 1;
```
Since `x` and `person` reference the **same object**:
```js
person // { name: "Lydia", age: 22 }
```


Second call
```js
changeAgeAndName();
```
No argument is passed, so the default parameter is used:
```js
x = { ...person };
```
The spread operator creates a **new shallow copy**.
```js
x // { name: "Lydia", age: 22 }
```
Then:
```js
x.age += 1;
x.name = "Sarah";
```
Now `x` becomes:
```js
{ name: "Sarah", age: 23 }
```
But **only the copy changes**.

The original `person` remains:
```js
{ name: "Lydia", age: 22 }
```

Rule for notes
- Passing an object as an argument → function receives the **same object reference**.
- Default parameter `{ ...obj }` creates a **new shallow copy** only when **no argument** is provided.
- Mutating the copy does **not** affect the original object.


###### Q. Which of the following options will return 6?
```js
function sumValues(x, y, z) {
  return x + y + z;
}
```
- A: `sumValues([...1, 2, 3])`
- B: `sumValues([...[1, 2, 3]])`
- C: `sumValues(...[1, 2, 3])`
- D: `sumValues([1, 2, 3])`

The correct answer is:
> ✅ **C: `sumValues(...[1, 2, 3])`**

Let's examine each option.
```js
function sumValues(x, y, z) {
  return x + y + z;
}
```

The function expects **three separate arguments**.

A
```js
sumValues([...1, 2, 3])
```

❌ **TypeError**
You cannot spread a number.
```js
...[1,2,3]   // ✅
...1         // ❌ Number is not iterable
```

Error:
```text
TypeError: 1 is not iterable
```

B
```js
sumValues([...[1, 2, 3]])
```
The spread works inside the array:
```js
[...[1,2,3]] // [1,2,3]
```
So the call becomes:
```js
sumValues([1,2,3])
```
Equivalent to:
```js
x = [1,2,3]
y = undefined
z = undefined
```
Then:
```js
[1,2,3] + undefined + undefined
```
Results in string coercion:
```text
"1,2,3undefinedundefined"
```
❌ Not `6`.

C ✅
```js
sumValues(...[1, 2, 3])
```
The spread operator expands the array into separate arguments:
```js
sumValues(1, 2, 3)
```
So:
```js
1 + 2 + 3
// 6
```
✅ Returns `6`.

D
```js
sumValues([1, 2, 3])
```
Equivalent to:
```js
x = [1,2,3]
y = undefined
z = undefined
```
Again:
```js
[1,2,3] + undefined + undefined
```
Output:
```text
"1,2,3undefinedundefined"
```
❌ Not `6`.

Rule for notes
- **Spread in function calls** expands an iterable into individual arguments.
```js
fn(...[1, 2, 3]); // fn(1, 2, 3)
```

- Passing an array without `...` passes it as **one argument**.
```js
fn([1, 2, 3]); // x = [1,2,3], y = undefined, z = undefined
```

- Only **iterables** (arrays, strings, sets, etc.) can be spread. Primitive numbers cannot.
```js
...[1, 2] // ✅
..."abc"  // ✅
...1      // ❌ TypeError
```


###### Q. Tell Output
```js
let num = 1;
const list = ['🥳', '🤠', '🥰', '🤪'];
console.log(list[(num += 1)]); // 🥰
```

Why?
```js
num += 1; // num becomes 2
list[2];  // 🥰
```

Rule:
- `x += y` → `x = x + y`
- The expression evaluates to the new value (`2` here).


###### Q. Tell Output
```js
const person = {
  firstName: 'Lydia',
  lastName: 'Hallie',
  pet: {
    name: 'Mara',
    breed: 'Dutch Tulip Hound',
  },
  getFullName() {
    return `${this.firstName} ${this.lastName}`;
  },
};
console.log(person.pet?.name);
console.log(person.pet?.family?.name);
console.log(person.getFullName?.());
console.log(member.getLastName?.());
```

**Output:**
```text
Mara
undefined
Lydia Hallie
ReferenceError: member is not defined
```

**Why?**
- `person.pet?.name` → `"Mara"`
- `person.pet?.family?.name` → `undefined` (`family` doesn't exist)
- `person.getFullName?.()` → calls the method → `"Lydia Hallie"`
- `member.getLastName?.()` → ❌ `member` itself is not defined, so optional chaining cannot prevent the `ReferenceError`.

**Rule:**
- `obj?.prop` protects against `obj` being `null` or `undefined`.
- It **does not** protect against an **undeclared variable**.
```js
obj?.prop;      // ✅
undefinedVar?.x; // ❌ ReferenceError
```


###### Q. Tell Output
```js
const groceries = ['banana', 'apple', 'peanuts'];

if (groceries.indexOf('banana')) {
  console.log('We have to buy bananas!');
} else {
  console.log(`We don't have to buy bananas!`);
}
```

Output:
```text
We don't have to buy bananas!
```

Why?
```js
groceries.indexOf('banana'); // 0
```
`0` is **falsy**, so the `else` block executes.

**Rule:**
- `indexOf()` returns:
    - `0, 1, 2, ...` → found
    - `-1` → not found

⚠️ Don't use it directly in `if`.
```js
// ❌
if (arr.indexOf('banana'))

// ✅
if (arr.indexOf('banana') !== -1)

// or
if (arr.includes('banana'))
```


###### Q. Tell Output
```js
const config = {
  languages: [],
  set language(lang) {
    return this.languages.push(lang);
  },
};
console.log(config.language); // undefined
```

Why?
`language` is a **setter**, not a getter.
```js
config.language = "JavaScript"; // ✅ Calls the setter
config.language; // ❌ No getter → undefined
```

Rule:
- `set prop(value) {}` → handles assignment only.
- `get prop() {}` → returns a value when accessed.


###### Q. Tell Output
```js
const name = 'Lydia Hallie';
console.log(!typeof name === 'object');
console.log(!typeof name === 'string');
```
Output:
```text
false
false
```

**Why?**
`typeof` has **higher precedence** than `!`.

So:
```js
!typeof name
```
is evaluated as:
```js
!(typeof name)
```

```js
typeof name      // "string"
!("string")      // false
```

Then:
```js
false === "object" // false
false === "string" // false
```

**Rule:**
If you want to negate the comparison, use parentheses:
```js
!(typeof name === 'object')
!(typeof name === 'string')
```
The second expression above evaluates to `false` because `typeof name === 'string'` is `true`, and `!true` is `false`.


###### Q. Tell Output
```js
const add = x => y => z => {
  console.log(x, y, z);
  return x + y + z;
};
add(4)(5)(6); // 4 5 6
```
(Returns `15`, but it's not logged.)

**Why?**
Each arrow function returns another function until the last one.
```js
add(4)      // returns y => ...
     (5)    // returns z => ...
        (6) // logs 4 5 6, returns 15
```

Rule:
- This is **currying**: one function takes one argument and returns another function until all arguments are received.


###### Q. Tell Output
```js
async function* range(start, end) {
  for (let i = start; i <= end; i++) {
    yield Promise.resolve(i);
  }
}

(async () => {
  const gen = range(1, 3);
  for await (const item of gen) {
    console.log(item);
  }
})();
```

Output:
```text
1
2
3
```

Why?
- `yield Promise.resolve(i)` yields a promise.
- `for await...of` automatically **awaits** each yielded promise before assigning it to `item`.

Rule:
- `for...of` → iterates values.
- `for await...of` → iterates **async values/promises**, awaiting each one automatically.


###### Q. Tell Output
```js
const myFunc = ({ x, y, z }) => {
  console.log(x, y, z);
};
myFunc(1, 2, 3);
```

**Output:**
```text
undefined undefined undefined
```

**Why?**
The parameter uses **object destructuring**:
```js
({ x, y, z })
```

But you passed:
```js
1
```
A number has no properties `x`, `y`, or `z`, so each becomes `undefined`.

**Correct call:**
```js
myFunc({ x: 1, y: 2, z: 3 });
// 1 2 3
```

**Rule:**
- `{ x, y }` → expects an **object**.
- `[x, y]` → expects an **array**.


###### Q. Tell Output
```js
function getFine(speed, amount) {
  const formattedSpeed = new Intl.NumberFormat('en-US', {
    style: 'unit',
    unit: 'mile-per-hour'
  }).format(speed);

  const formattedAmount = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD'
  }).format(amount);

  return `The driver drove ${formattedSpeed} and has to pay ${formattedAmount}`;
}

console.log(getFine(130, 300));
```

**Output:**
```text
The driver drove 130 mph and has to pay $300.00
```

**Why?**
- `Intl.NumberFormat` formats numbers according to locale.
- `style: 'unit'` + `unit: 'mile-per-hour'` → `130 mph`
- `style: 'currency'` + `currency: 'USD'` → `$300.00`

**Rule:**
- `Intl.NumberFormat` is used for locale-aware formatting.
    - `style: 'currency'` → currencies (`$300.00`)
    - `style: 'unit'` → units (`130 mph`)
    - `style: 'percent'` → percentages (`25%`)


###### Q. Tell Output
```js
const spookyItems = ['👻', '🎃', '🕸'];
({ item: spookyItems[3] } = { item: '💀' });

console.log(spookyItems);
```

**Output:**
```js
['👻', '🎃', '🕸', '💀']
```

**Why?**
The destructuring assignment:
```js
({ item: spookyItems[3] } = { item: '💀' });
```
assigns the value of `item` (`'💀'`) to `spookyItems[3]`.

Equivalent to:
```js
spookyItems[3] = '💀';
```

**Rule:**
- In object destructuring, you can assign directly to array elements or object properties.
```js
({ a: arr[0] } = { a: 10 });
// arr[0] = 10
```



###### Q. Tell Output
```js
const name = 'Lydia Hallie';
const age = 21;

console.log(Number.isNaN(name));
console.log(Number.isNaN(age));

console.log(isNaN(name));
console.log(isNaN(age));
```

**Output:**
```text
false
false
true
false
```

**Why?**
- `Number.isNaN()` checks **only if the value is actually `NaN`**.
- `isNaN()` **first converts** the value to a number, then checks.
```js
Number.isNaN('Lydia'); // false
isNaN('Lydia');        // true (Number('Lydia') => NaN)

Number.isNaN(21);      // false
isNaN(21);             // false
```

**Rule:**
- `Number.isNaN(x)` → strict check (recommended).
- `isNaN(x)` → converts `x` to a number before checking.


###### Q. Tell Output
```js
const randomValue = 21;

function getInfo() {
  console.log(typeof randomValue);
  const randomValue = 'Lydia Hallie';
}
getInfo();
```

Output:
```text
ReferenceError: Cannot access 'randomValue' before initialization
```

Why?
The local `const randomValue` shadows the global one and is in the **Temporal Dead Zone (TDZ)** until it's initialized.
```js
function getInfo() {
  // randomValue is in TDZ here
  console.log(typeof randomValue); // ❌ ReferenceError
  const randomValue = 'Lydia Hallie';
}
```

`typeof` does **not** avoid a `ReferenceError` for variables in the TDZ.

**Rule:**
- `typeof undeclaredVariable` → `"undefined"` ✅
- `typeof let/constVariableInTDZ` → `ReferenceError` ❌


###### Q. Tell Output
```js
const myPromise = Promise.resolve('Woah some cool data');

(async () => {
  try {
    console.log(await myPromise);
  } catch {
    throw new Error(`Oops didn't work`);
  } finally {
    console.log('Oh finally!');
  }
})();
```

Output
```text
Woah some cool data
Oh finally!
```

Why?
- `await myPromise` resolves immediately → logs:
    ```
    Woah some cool data
    ```
- No error occurs → `catch` block is skipped.
- `finally` **always runs**, regardless of success/failure:
    ```
    Oh finally!
    ```

Rule (important)
- `try` → runs normal logic
- `catch` → runs only on error
- `finally` → always runs (even after return / throw)


###### Q. Tell Output
```js
const emojis = ['🥑', ['✨', '✨', ['🍕', '🍕']]];
console.log(emojis.flat(1));
```

**Output:**
```text
['🥑', '✨', '✨', ['🍕', '🍕']]
```

**Why?**
- `.flat(1)` flattens **only 1 level** of nesting.
- So only this part is unwrapped:
    ```js
    ['✨', '✨', ['🍕', '🍕']]
    ```

Becomes:
```js
'✨', '✨', ['🍕', '🍕']
```
- The inner array `['🍕', '🍕']` is still nested because it is **2 levels deep**.
    
**Rule:**
- `flat(1)` → removes one layer
- deeper arrays stay untouched
- `flat(Infinity)` → fully flattens everything


###### Q. Tell Output
```js
class Counter {
  constructor() {
    this.count = 0;
  }

  increment() {
    this.count++;
  }
}

const counterOne = new Counter();
counterOne.increment();
counterOne.increment();

const counterTwo = counterOne;
counterTwo.increment();

console.log(counterOne.count);
```

**Output:**
```text
3
```

**Why?**
- `counterTwo = counterOne` does **not create a new object**
- Both variables point to the **same reference**

So all increments affect the same instance:
```js
counterOne.count = 0 → 1 → 2 → 3
```

**Rule:**
- Objects are assigned **by reference**
- No copy is made unless explicitly cloned


###### Q. Tell Output
```js
const myPromise = Promise.resolve(Promise.resolve('Promise'));

function funcOne() {
  setTimeout(() => console.log('Timeout 1!'), 0);
  myPromise.then(res => res).then(res => console.log(`${res} 1!`));
  console.log('Last line 1!');
}

async function funcTwo() {
  const res = await myPromise;
  console.log(`${res} 2!`)
  setTimeout(() => console.log('Timeout 2!'), 0);
  console.log('Last line 2!');
}

funcOne();
funcTwo();
```

TODO


###### Q. How can we invoke sum in sum.js from index.js?
```js
// sum.js
export default function sum(x) {
  return x + x;
}

// index.js
import * as sum from './sum';
```


```js
import * as sum from './sum';
```
Output behavior

`sum` becomes a **module namespace object**, not the function.
So:
```js
console.log(sum);
```

Outputs something like:
```text
{
  default: [Function: sum]
}
```

Why?
You did:
```js
export default function sum(x) {
  return x + x;
}
```
But imported as:
```js
import * as sum from './sum';
```
So ES modules wrap exports like:
```js
sum = {
  default: sumFunction
}
```

Correct usage options
```js
// Option 1 (recommended)
import sum from './sum';
sum(2);
```

```js
// Option 2
import * as sum from './sum';
sum.default(2);
```

Rule
- `default export` + `import * as` → function is inside `.default`
- `import default` → direct function access


###### Q. Tell Output
```js
const handler = {
  set: () => console.log('Added a new property!'),
  get: () => console.log('Accessed a property!'),
};

const person = new Proxy({}, handler);

person.name = 'Lydia';
person.name;
```

Output
```text
Added a new property!
Accessed a property!
```

Why?
- `person.name = 'Lydia'` → triggers **set trap**
- `person.name` → triggers **get trap**
But note: your traps **don’t return values**

So:
- `set` still logs message
- `get` logs message but returns `undefined`

Important detail (real behavior)
Proper proxy traps usually look like:
```js
set(target, prop, value) { ... }
get(target, prop) { ... }
```
In your case, since parameters are ignored, it still runs but **only side-effects (console.log)** happen.

Rule
- Proxy intercepts operations (`get`, `set`, etc.)
- If trap exists → it runs instead of default behavior
- If no `return` in `get` → value becomes `undefined`

---
###### Q. Tell Output
```js
const person = { name: 'Lydia Hallie' };
Object.seal(person);
```

What it does
`Object.seal()` makes the object:
- ❌ No new properties can be added
- ❌ Existing properties cannot be deleted
- ✅ Existing properties can still be modified

Example behavior
```js
person.name = 'Sarah'; // allowed
person.age = 21;       // ignored / fails silently (or throws in strict mode)
delete person.name;    // false
```

Check status
```js
Object.isSealed(person); // true
```

Rule
- `freeze` → no changes allowed at all
- `seal` → can modify, but cannot add/remove properties

---
###### Q. Which of the following will modify the person object?
```js
const person = {
  name: 'Lydia Hallie',
  address: {
    street: '100 Main St',
  },
};
Object.freeze(person);
```
What happens
- `person` is **frozen shallowly**
- Top-level properties cannot be:
    - added ❌
    - removed ❌
    - modified ❌

 Important catch (common trap)
```js
person.address.street = '200 Main St';
```
This **still works**.

Why?
`Object.freeze()` is **shallow**, not deep.
So:
```js
person.address // still a normal mutable object
```
Only the outer object is frozen.

If you try:
```js
person.name = 'Sarah'; // ignored (or fails in strict mode)
```

Rule
- `freeze()` = shallow immutability
- Nested objects are still mutable unless you recursively freeze them
```js
function deepFreeze(obj) {
  Object.freeze(obj);
  Object.keys(obj).forEach(key => {
    if (typeof obj[key] === 'object' && obj[key] !== null) {
      deepFreeze(obj[key]);
    }
  });
}
```

---
###### Q. Tell Output
```js
const add = x => x + x;
function myFunc(num = 2, value = add(num)) {
  console.log(num, value);
}
myFunc(); // 2 4
myFunc(3); // 3 6
```


###### Q. Tell Output
```js
class Counter {
  #number = 10
  increment() {
    this.#number++
  }
  getNum() {
    return this.#number
  }
}
const counter = new Counter()
counter.increment()
console.log(counter.#number)
```

Output
```text
SyntaxError: Private field '#number' must be declared in an enclosing class
```

Why?
- `#number` is a **private class field**
- It is only accessible **inside the class body**
- Outside access is forbidden at compile time (not runtime)

```js
counter.getNum(); // 11 (valid way)
counter.#number;   // ❌ illegal
```

Rule
- `#field` → **true private (hard privacy)**
- Cannot be accessed, read, or modified outside class
- Must use public methods (`getNum`, etc.) to access it


###### Q. Tell Output
```js
const teams = [
  { name: 'Team 1', members: ['Paul', 'Lisa'] },
  { name: 'Team 2', members: ['Laura', 'Tim'] },
];
function* getMembers(members) {
  for (let i = 0; i < members.length; i++) {
    yield members[i];
  }
}
function* getTeams(teams) {
  for (let i = 0; i < teams.length; i++) {
    // ✨ SOMETHING IS MISSING HERE ✨
  }
}
const obj = getTeams(teams);
obj.next(); // { value: "Paul", done: false }
obj.next(); // { value: "Lisa", done: false }
```

You need to **delegate the inner generator** using `yield*`.

Correct code
```js
function* getTeams(teams) {
  for (let i = 0; i < teams.length; i++) {
    yield* getMembers(teams[i].members);
  }
}
```

Why?
- `getMembers()` yields individual members
- `yield*` **forwards all yielded values** from another generator

So flow becomes:
```js
Team 1 → Paul → Lisa
Team 2 → Laura → Tim
```

Result
```js
const obj = getTeams(teams);

obj.next(); // Paul
obj.next(); // Lisa
obj.next(); // Laura
obj.next(); // Tim
```

Rule
- `yield` → single value
- `yield*` → delegate to another iterator/generator (flatten behavior)


###### Q. Tell Output
```js
const person = {
  name: 'Lydia Hallie',
  hobbies: ['coding'],
};

function addHobby(hobby, hobbies = person.hobbies) {
  hobbies.push(hobby);
  return hobbies;
}

addHobby('running', []);
addHobby('dancing');
addHobby('baking', person.hobbies);

console.log(person.hobbies);
```

TODO 141
https://github.com/lydiahallie/javascript-questions














---
###### Q. Find the sum
```js
let arr=[1,2,3];
let sum=0;

for(let i=0;i<arr.length;i++){
    sum+=arr[i]; // sum=sum+arr[i];
}

console.log(sum);
```

or
```js
let arr=[1,2,3];

let res=arr.reduce((acc,curr)=>acc+curr,0);

console.log(res);
```

or
```js
const arr = [1, 2, 3, 4, 5];
let sum=0;
for(const num of arr){
	sum+=num
}
console.log(sum);
```


###### Q. Find max/min
```js
let arr = [-5, -2, -10];
let max=arr[0];

for(let i=0;i<arr.length;i++){
    if(arr[i]>max){
        max=arr[i];
    }
}
console.log(max);
```

or
```js
let arr=[1,2,3];
let max=Math.max(...arr);
console.log(max);
```

or
```js
let arr = [-5, -2, -10];
let res=arr.reduce((acc,curr)=>acc>curr ? acc: curr);
console.log(res);
```
if you don't provide an initial value, JavaScript automatically uses the first element of the array as the accumulator.


###### Q. Find the item count
```js
const arr = [1,2,3,4,5,1,2,1,3,1,50];

const count = arr.reduce((acc,curr)=>{acc[item]=(acc[item] || 0)+1;
	return acc;
},{});

console.log(count);
```

or
```js
const arr = [1,2,3,4,5,1,2,1,3,1,50];
const freq = new Map();

for(const item of arr){
    freq.set(item,(freq.get(item) || 0)+1);
}

console.log(freq);
```


###### Reverse array

built-in `reverse()` method
```js
const arr = [1, 2, 3, 4, 5];
arr.reverse();
console.log(arr); // [5, 4, 3, 2, 1]
```

without modifying the original array
```js
const arr = [1, 2, 3, 4, 5];
const reversed = [...arr].reverse();
console.log(reversed); // [5, 4, 3, 2, 1]
```

In-place reverse using two pointers
```js
const arr = [1, 2, 3, 4, 5];

let left = 0;
let right = arr.length - 1;

while (left < right) {
  [arr[left], arr[right]] = [arr[right], arr[left]];
  //let temp = arr[left];
  //arr[left] = arr[right];
  //arr[right] = temp;
  left++;
  right--;
}

console.log(arr); // [5, 4, 3, 2, 1]
```


###### Q. Removes duplicates

using `Set`
- `Set` is a **constructor** that creates a collection of **unique values**.
- `new Set(arr)` converts the array into a `Set` (removes duplicates).
- `...` (spread) works on **iterables** like `Set` and `Array`.
- `[...new Set(arr)]` = convert **Array → Set (unique) → Array**.

```js
const arr = [1, 2, 3, 4, 5, 1, 2, 1, 3, 1, 50];
const unique = [...new Set(arr)];
console.log(unique);
// [1, 2, 3, 4, 5, 50]
```
Time Complexity: `O(n)`  
Space Complexity: `O(n)`

using `filter()`
```js
const arr = [1, 2, 3, 4, 5, 1, 2, 1, 3, 1, 50];

const unique = arr.filter((item, index) => {
  // indexOf(item) always returns the FIRST occurrence of `item` in the array.
  // Keep the element only if its first occurrence index matches the current index.
  // Duplicates fail this check because their first occurrence is at an earlier index.
  return arr.indexOf(item) === index;
});

console.log(unique); // [1, 2, 3, 4, 5, 50]
```

`filter + indexOf` is **O(n²)** because `indexOf()` scans the array for every element.


###### Find intersection of two arrays (common element)

```js
const arr1 = [1, 2, 3, 4];
const arr2 = [3, 4, 5, 6];

const set2 = new Set(arr2);

const intersection = arr1.filter(item => set2.has(item));

console.log([...new Set(intersection)]); // [3, 4]
```

const set2 = new Set(arr2); // Convert to Set because Set provides O(1) `.has()` where as Arrays don't have `.has()` (they use slower `.includes()`).

// `new Set(arr)` creates a Set object.
// `[...new Set(arr)]` converts the Set back to an array, so you'd need `.includes()` instead of `.has()`.


###### Check palindrome array
The array reads the same from both ends.
i.e. 12321, abcba etc

using two pointers
```js
const isPalindrome = (arr) => {
    let left = 0;
    let right = arr.length - 1;

    while (left < right) {
        if (arr[left] !== arr[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
};

console.log(isPalindrome([1, 2, 3, 2, 1])); // true
console.log(isPalindrome([1, 2, 3])); // false
```

Time Complexity: O(n)
Space Complexity: O(1)

###### Check if every string in array is palindrome

using two pointer
```js
const isPalindrome = (str) => {
	let left=0;
	let right=str.length-1;
	
	while(left<right){
		if(str[left]!==str[right]) return false;
		left++;
		right--;
	}
	return true;
}

const arr = ["madam", "level", "hello"];

const result = arr.map(isPalindrome);

console.log(result); // [ true, true, false ]
```

Time Complexity: O(n)
Space Complexity: O(1)

using `reverse()`
```js
const isPalindrome = (str)=>{
    const revStr = str.split("").reverse().join("");
    
    return str===revStr;
}

const arr = ["madam", "level", "hello"];

const result = arr.map(isPalindrome);

console.log(result); // [ true, true, false ]
```
Time Complexity: O(n)
Space Complexity: O(n) (because a new array and a new string are created)





---
### String





###### Reverse string
Strings are immutable so `reverse()` won't fit 
```js
const str = "asdf";  
  
const reversed = str  
.split("") // ["a", "s", "d", "f"]  
.reverse() // ["f", "d", "s", "a"]  
.join(""); // "fdsa"  
  
console.log(reversed);
```



---
### Objects

###### Merge two objects

using spread operator
```js
const obj1={
	name: "john",
	age: 25,
};

const obj2={
	city: "Delhi",
	country: "India",
};

const merged = {
	...obj1,
	...obj2
};

console.log(merged);
// {
//   name: "John",
//   age: 25,
//   city: "Delhi",
//   country: "India"
// }
```

if both objects have the same key, then the later object overwrites the earlier one.


---
###### Deep clone object
Deep cloning means creating a completely independent copy of an object, including all nested objects and arrays. No references are shared.

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
const obj = {
    name: "John",
    address: {
        city: "Delhi"
    }
};

const clone = JSON.parse(JSON.stringify(obj));

console.log(obj);
console.log(clone);
// Output:
// { name: 'John', address: { city: 'Delhi' } }
// { name: 'John', address: { city: 'Mumbai' } }
```


In coding interviews, you may also be asked to implement a recursive deep clone manually to demonstrate understanding of object traversal.

```js
function deepClone(obj) {
  if (obj === null || typeof obj !== "object") {
    return obj;
  }

  const copy = Array.isArray(obj) ? [] : {};

  for (const key in obj) {
    copy[key] = deepClone(obj[key]);
  }

  return copy;
}
```

---
###### Serialization & Deserialization (JavaScript)
Serialization is the process of converting a JavaScript object into a JSON string using `JSON.stringify()`, typically for transmitting or storing data. 
Deserialization is the reverse process—converting a JSON string back into a JavaScript object using `JSON.parse()`

###### Serialization (`JSON.stringify()`)
Converts a **JavaScript object → JSON string**.

```js
const user = {
  name: "John",
  age: 25
};
const json = JSON.stringify(user);
console.log(json);
// '{"name":"John","age":25}'
```

**Use cases:**
- Sending data in API requests
- Storing data in `localStorage`
- Writing data to files

###### Deserialization (`JSON.parse()`)
Converts a **JSON string → JavaScript object**.
```js
const json = '{"name":"John","age":25}';

const user = JSON.parse(json);

console.log(user); // { name: 'John', age: 25 }
```

Common Interview Question

Why use `JSON.stringify()` before storing in `localStorage`? Because `localStorage` only stores **strings**.
```js
localStorage.setItem("user", JSON.stringify(user));
const storedUser = JSON.parse(localStorage.getItem("user"));
```


---
###### Deep object comparison
Deep object comparison means checking whether two objects have the same structure and values recursively, not whether they point to the same memory location.

```js
const obj1 = {
  name: "John",
  address: {
    city: "Delhi",
  },
};

const obj2 = {
  name: "John",
  address: {
    city: "Delhi",
  },
};

console.log(obj1 === obj2); // false
```
`===` compares **references**, not contents.
Even though they contain identical data, they are different objects in memory.

**Deep Comparison**
A deep comparison recursively checks every property.

It verifies:
- Same keys
- Same number of keys
- Same values
- Nested objects recursively
- Nested arrays recursively

```js
function deepEqual(a, b) {
  // Same reference or primitive
  if (a === b) return true;

  // One is null or not an object
  if (
    a === null ||
    b === null ||
    typeof a !== "object" ||
    typeof b !== "object"
  ) {
    return false;
  }

  const keysA = Object.keys(a);
  const keysB = Object.keys(b);

  if (keysA.length !== keysB.length) {
    return false;
  }

  for (const key of keysA) {
    if (!keysB.includes(key)) {
      return false;
    }

    if (!deepEqual(a[key], b[key])) {
      return false;
    }
  }

  return true;
}
```


---
###### Convert array → key-value object

```js
const arr = [["a", 1], ["b", 2], ["c", 3]];
const obj = Object.fromEntries(arr);
console.log(obj);
// { a: 1, b: 2, c: 3 }
```

using reduce
```js
const arr = [
	{ id: "a", value: 1},
	{ id: "b", value: 2}
];

const obj = arr.reduce((acc,curr)=>{
	acc[curr.id]=curr.value
	return acc;
},{});

console.log(obj); // { a: 1, b: 2 }
```


---
RoadsideCoder: https://youtu.be/XnFIX3c7xoI?t=171
###### Q. Tell Output
```js
const obj = {
	a: "one",
	b: "two",
	a: "three"
};
console.log(obj); //{ a: 'three', b: 'two' }
```
if the same key appears multiple times, the last occurrence overrides all previous ones.

###### Q. Create function `mutliplyByTwo(obj)` that multiplies all the numeric property values of nums by 2

```js
let nums = {
	a: 100,
	b: 200,
	title: "My numbs",
};

function multiplyByTwo(obj){
	for(let key in obj){
		if(typeof obj[key]==="number"){
			obj[key]*=2;
		}
	}
}
multiplyByTwo(nums)
console.log(nums); //{ a: 200, b: 400, title: 'My numbs' }
```

###### Q. Tell Output
```js
const a = {};
const b = { key: "b" };
const c = { key: "c" };
a[b] = 123;
a[c] = 456;
console.log(a[b]); // 456
```
Why?
- Object keys must be **strings or symbols**.
- When an **object is used as a key**, JavaScript converts it to a string:
```js
String(b); // "[object Object]"
String(c); // "[object Object]"
```
So:
```js
a["[object Object]"] = 123;
a["[object Object]"] = 456; // overwrites
```

Hence:
```js
a[b] // 456
```
Rule for notes:
- Plain object keys → **strings/symbols only**.
- Using an object as a key converts it to `"[object Object]"`.
- Use **`Map`** if you need objects as keys.
i.e.
```js
const map = new Map();
map.set(b, 123);
map.set(c, 456);

map.get(b); // 123
map.get(c); // 456
```


###### Q. Tell Output
```js
console.log([..."asf"]); // [ 'a', 's', 'f' ]
```

###### Q. Tell Output
```js
const user = { name: "Lydia", age: 21 };
const admin = { admin: true, ...user };
console.log(admin); // { admin: true, name: 'Lydia', age: 21 }
```

###### Q. Tell Output
```js
const settings = {
	username: "Piyush",
	level: 19,
	health: 90,
};
const data = JSON.stringify(settings, ["level", "health"]);
console.log(data); // {"level":19,"health":90}
```
`JSON.stringify(value, replacer)` accepts a **replacer array** as the second argument.
- `["level", "health"]` tells `JSON.stringify` to **include only these properties**.
- So `username` is ignored.

###### Q. Tell Output
```js
console.log({ a: 1 } == { a: 1 }); // false
console.log({ a: 1 } === { a: 1 }); // false
```
because of different memory reference 

###### Q. Tell Output
```js
let person = { name: "Lydia" }; // person → object
const members = [person];       // members[0] → same object
person = null;                  // person no longer points to the object
console.log(members); // [ { name: 'Lydia' } ]
```
`members` stores a **reference** to the object, not the variable `person`
Setting a variable to `null` removes **that variable's reference**, not the object itself. The object is garbage-collected only when **no references** to it remain.

```js
let person = { name: "Lydia" };
const members = [person];
person.name = null;
console.log(members); // [ { name: null } ]
```

###### Q. Tell Output
https://youtu.be/XnFIX3c7xoI?t=1376
```js
const value = { number: 10 };
const multiply = (x = { ...value }) => {
  console.log((x.number *= 2));
};
multiply();       // 20
multiply();       // 20
multiply(value);  // 20
multiply(value);  // 40
```
Why?
- `x = { ...value }` creates a **new copy** of `value` only when **no argument** is passed.
- Passing `value` directly means `x` and `value` refer to the **same object**.

Step by step:
1. `multiply()`
    - `x = { number: 10 }` (copy)
    - `10 * 2 = 20`
    - Original `value` is still `{ number: 10 }`
2. `multiply()`
    - Another fresh copy `{ number: 10 }`
    - Prints `20`
3. `multiply(value)`
    - `x` points to the original object.
    - `value.number` changes from `10 → 20`
    - Prints `20`
4. `multiply(value)`
    - Same object again.
    - `value.number` changes from `20 → 40`
    - Prints `40`

Key concept
- **Default parameter + spread (`{...value}`)** → creates a **shallow copy**.
- **Passing an object directly** → passes its **reference**, so mutations affect the original object.

###### Q. Tell Output
TODO: https://youtu.be/XnFIX3c7xoI?t=1477

```js
function changeAgeAndReference(person){
    person.age = 25;
    person = {
        name: "john",
        age: 50,
    }
    return person;
};
const personObj1 = {
  name: "Alex",
  age: 30,
};
const personObj2 = changeAgeAndReference(personObj1);

console.log(personObj1); // { name: 'Alex', age: 25 }
console.log(personObj2); // { name: 'john', age: 50 }
```


TODO:
```js
let user = {
  name: "Roadside code"  ,
  age: 24,
};
const objClone = Object.assign({},user);
objClone.name = "Piyush";
console.log(user,objClone);
```