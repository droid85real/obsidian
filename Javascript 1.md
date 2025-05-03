Js is a 
+ interpreted
+ jit compiled
+ multi-paradigm
+ prototype based (allows the creation of an object without first defining its class)
+ synchronous
+ single threaded
+ dynamic language (no need to define data type)

# JavaScript Variable Declarations: `let`, `const`, `var`
## 🔹 `var`
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

## 🔹 `let`
- **Block-scoped**: Only accessible within the `{}` block where it's declared.
- **Hoisted**, but **not initialized**: Accessing before declaration causes a **ReferenceError**.
- **Can be updated, but not redeclared** in the same scope.

```js
{
  console.log(b); // ReferenceError
  let b = 20;
}
```


## 🔹 `const`

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


week6,topic2,lec11



# ( && ) AND Operator 
+ first falsy and last truthy

# ( || ) OR Operator
+ first truthy and last falsy


falsy value : { 0 , " " , null , undefined , false , NaN(not a number) }

