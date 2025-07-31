React app is made up of components. Its components are js functions

DOM : Document Object Model

Virtual DOM : The Virtual DOM in ReactJS is a lightweight, in-memory representation of the actual DOM. React uses it to optimize performance by updating only the parts of the DOM that need to change, instead of re-rendering the entire UI. When a component's state or props change, React creates a new Virtual DOM, compares it with the previous version (using a process called "reconciliation"), and efficiently updates only the necessary elements in the real DOM. This minimizes expensive DOM manipulations, resulting in faster rendering.

Babel in ReactJS converts modern JavaScript and JSX into browser-compatible code.

# `create-react-app`

+ go to the directory and `npx create-react-app helloworld`
+ and `npm run start` to start hosting locally.

to update `npm install -g npm@latest`
+ `npm -v` to check latest npm version
+ `node -v` to check nodejs version


### Files You Should Keep

- `package.json` and `package-lock.json` (Handles dependencies)
- `public/index.html` (Main HTML entry point)
- `src/index.js` (App entry point)
- `src/App.js` (Main component)

>Note :
`package.json` : It records all the dependencies , scripts and metadata about the project.


---
# Fragments 
+ Fragments are used to form a group
+ When returning multiple elements from a component, without fragments, you need to wrap them in a parent element like a `<div>`. This can be unnecessary and result in extra nodes in the DOM.

## `React.Fragment`
```js
import React from 'react';

const MyComponent = () => {
  return (
    <React.Fragment>
      <h1>Hello, World!</h1>
      <p>This is a simple React component using Fragments.</p>
    </React.Fragment>
  );
};

export default MyComponent;
```

## Empty Wrappers
using `<>` and `</>`
```js
import React from 'react';

const MyComponent = () => {
  return (
    <>
      <h1>Hello, World!</h1>
      <p>This is a simple React component using shorthand Fragments.</p>
    </>
  );
};

export default MyComponent;
```

**Notes :**
+ naming convention for react components (`PascalCase` or `UpperCamelCase`)

**Functional Component** 
i.e.
```js
function MyComponent() {
  return(
	  <p>JSX is Javascript XML</p>
  )
}
```
call above functional component using `<MyComponent />`

**Arrow function**
```js
const MyComponent=()=>(
	<>
		<h1 className="head">Hello JSX</h1>
		<p>This is created using JSX</p>
	</>
);
```
- **Arrow functions** with a single expression implicitly return that expression without needing the `return` keyword.

**Arrow functions with curly braces (`{}`)** require an explicit `return` statement.
```js
const MyComponent = () => {
  return (
    <>
      <h1 className="header">Welcome to JSX!</h1>
      <p>This is a paragraph inside the component.</p>
    </>
  );
};
```


# Export & Import
In React (and JavaScript in general), you can use named exports and default exports to share functions, objects, or values between different modules.

## Named Export
+ In **named exports**, you export multiple items (functions, variables, or objects) from a module using the `export` keyword. 
+ When importing, you need to use the **same name** that was exported.
+ it uses curly braces while importing.

`myComponent.js`
```js
export var a=10;

export const MyComponent = () => {
  return <div>Hello, World!</div>;
};

export const anotherComponent = () => {
  return <div>Another Component</div>;
};
```

`App.js`
```js
import { MyComponent, anotherComponent, a } from './myComponent';

const App = () => {
  return (
    <div>
	    <p>The value of a is : {a}</p>
	    <MyComponent />
	    <anotherComponent />
    </div>
  );
};
```


### Using `as` in **export**:
You can use `as` to rename exports when you're exporting them, so the names can differ from the original names.

`myComponent.js`
```js
var a = 10;

const MyComponent = () => {
  return <div>Hello, World!</div>;
};

const anotherComponent = () => {
  return <div>Another Component</div>;
};

export { a as value }; // Renaming 'a' to 'value'
export { MyComponent, anotherComponent };
```

`App.js`
```js
import React from 'react';
import { MyComponent, anotherComponent, value } from './myComponent';

const App = () => {
  return (
    <div>
      <p>The value of 'a' (now renamed to 'value') is: {value}</p>
      <MyComponent />
      <anotherComponent />
    </div>
  );
};
```

### Using `as` in **Imports**:
`myComponent.js`
```js
export var a=10;

export const MyComponent = () => {
  return <div>Hello, World!</div>;
};

export const anotherComponent = () => {
  return <div>Another Component</div>;
};
```

`App.js`
```js
import { MyComponent as comp, anotherComponent as ano, a } from './myComponent';

const App = () => {
  return (
    <div>
      <p>The value of a is : {a}</p>
      <comp />
      <ano />
    </div>
  );
};
```

# Default export

In React, you can use `export default` to export a single component from a file.

#### In-line export

`MyComponent.js`
```js
import React from 'react';

export default function MyComponent() {
  return <h1>Hello from Default Export!</h1>;
}
```

`App.js`
```js
import React from 'react';
import MyComponent from './MyComponent'; // No curly braces needed

function App() {
  return (
    <div>
      <MyComponent />
    </div>
  );
}

export default App;
```

#### At the bottom

`MyComponent.js`
```js
import React from "react";

const MyComponent = () => {
  return <h1>Hello, I am a default exported component!</h1>;
};

export default MyComponent;
```

`App.js`
```js
import React from "react";
import CustomName from "./MyComponent"; // Importing the default export, you can use anyname in place of MyComponent

const App = () => {
  return (
    <div>
      <CustomName />
    </div>
  );
};

export default App;
```


Note :
You **must initialize** a variable, function, or class **before exporting it**.
```js
export x; // ❌ Error: 'export' declarations must be initialized
let x = 10;
```



**call function in jsx**

`App.js`
```js
import React from 'react';

function App() {
  // Define the function you want to call
  const handleClick = () => {
    alert('Button clicked!');
  };

  return (
    <div>
      {/* Use the function with onClick */}
      <button onClick={handleClick}>Click Me</button>  {/* here we called handleClick without ()*/}
    </div>
  );
}

export default App;
```



**expressions in jsx**

`index.js`
```js
import React from 'react';
import ReactDOM from 'react-dom/client';

function App(){
  var name="Rishi"
  var age=10;
  let demo=null;
  let undef;
  const bool=true;

  return(
    <>
      <h1>Javascript inside JSX</h1> {/* Javascript inside JSX */}
      <p>String: {name}</p>          {/* String: Rishi */}
      <p>Number: {age}</p>           {/* Number: 10 */}
      <p>Null value: {demo}</p>      {/* Null value:  */}  // null renders as empty
      <p>Undefined value: {undef}</p> {/* Undefined value:  */} // undefined renders as empty
      <p>Boolean value: {bool}</p>   {/* Boolean value:  */} // true/false are not rendered in JSX directly
    </>
  )
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```


**printing array and object**

`index.js`
```js
import React from 'react';
import ReactDOM from 'react-dom/client';

function App() {
  let arr = [1, 2, 3, 4];

  let obj = {
    name: "Rishu",
    age: 10
  };

  return (
    <>
      <p>{arr}</p> {/* output: 1234 */}
      <br />
      {arr.map((element, index) => <p key={index}>{element}</p>)}
      {/* output: 
      1
      2
      3
      4
      */}
      <br />
      <p>{obj.name}</p> {/* output: Rishu */}
      <p>{obj.age}</p> {/* output: 10 */}
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```


**we need to re-render to show changes in score and to pass argument we need to create inline function**

`index.js`
```js
import React from 'react';
import ReactDOM from 'react-dom/client';

let score = 0;

function addSum(num) {
  score += num;
  root.render(<App />);  //root re-render
}

const App = () => {
  return (
    <>
      <h1>Score: {score}</h1>
      <div>
        <button onClick={() => addSum(1)}>Add 1</button>  {/* ()=>addSum(1) is inline function*/}
        <button onClick={() => addSum(2)}>Add 2</button>
        <button onClick={() => addSum(3)}>Add 3</button>
      </div>
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```


**using filter and we have to assign a unique to every html element**

`index.js`
```js
import React from 'react';
import ReactDOM from 'react-dom/client';

function App() {
	let arr2 = [0, 1, 2, 3, 4, 5, 6];
	
 return (
    <>
      {arr2.filter((ele) => (ele % 2 === 0)).map((element, index) => <p key={index}>{element}</p>)}
      {/* output:
      0
      2
      4
      6
      */}
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```


**Displaying students information on table**

`index.js`
```js
import React from "react";
import ReactDOM from "react-dom/client";

const App = () => {
  let students = [
    { name: "Alexa", age: 10, marks: 35 },
    { name: "droid85", age: 25, marks: 100 },
    { name: "somya", age: 25, marks: 100 },
  ];

  return (
    <>
      <table style={{ borderCollapse: "collapse", margin: "20px auto" }} border="1">
        <thead>
          <tr>
            <th>Name</th>
            <th>Age</th>
            <th>Marks</th>
          </tr>
        </thead>
        <tbody>
          {students.map((student, index) => (
            <tr key={index}>
              <td>{student.name}</td>
              <td>{student.age}</td>
              <td>{student.marks}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </>
  );
};

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```


# TODO: Pending work

**Rendering components based on condition**

**preventdefault (synthetic event)**
+ synthetic events are wrapper around the event object of the real DOM
+ we have to call preventDefault to stop the default behaviour of a synthetic event

**Refs**
+ Refs are used to directly access DOM elements
+ Refs are created using **`React.createRef()`** and attached to the element via the ref attribute
+ we can use **`ref.current.value`** to access or modify the value of the input element associated with that ref

Flaticons for icons

**array destructuring**
```js
const[,,animal]=["Horse","cat","cow"];
console.log(animal); //output: cow
```

Note :
+ Events in react are named using camelCase rather than lower case.


## **Why Use State in React**

- **Stores dynamic data** (e.g., form inputs, counters).
- **Triggers re-renders** when updated.
- **Component-specific memory** — each component manages its own state.
- Makes UI **interactive** and responsive.
- Without state = static UI.

Class Based Components

#### week 2 | Topic 1 |
Lec 13
+ pendingDefault
Lec 16
+ input value atribute
+ extract value from input using createref , react.createref
+ then assign createref to input
+ then access it using inputref.currentvalue
Lec 19
+ template literals (backticks)
+ ${ } blabla ${ }

problem 25, 26, 27 can be used to show reactcreateref 

#### week 3 | Topic 1 |

Problem 6
Problem 8

Lec 9
+ states
+ destructuring

Lec 11
+ Bind
+ `this` get lost so we bind
+ two ways to bind
+ use arrow function it binds this automatically

Lec 13
+ Setstate
+ using this.state to set data and then doing destructure in render and in addstar using setstate to update state and re-render
+ two ways to write setstate

Lec 16
+ restricting increment and decrement of addstar
+ setState is asyn in nature so if u need current value of state , then call it inside the call back of setstate
+ batching: consecutive calling multiple times this.setstate , then react create batch and process only the last this.setstate
+ but if we use second form of this.setstate , and in this update of state depends on prev state so each call is considered but rendering only happen once
+ skipped test


#### week 3 | Topic 2 |

Lec 1
+ favourite button
Lec 2
+ add to cart
+ movielist
Lec 3
 + props (from parent to child only)
Lec 6
+ default value props
+ props can't be modified (states can be)
Lec 8
+ passing data through props
Lec 9 
+ displaying movielist with props
Lec11
+ handling increase star




#### week 4 | Topic 1 | Styling in react










