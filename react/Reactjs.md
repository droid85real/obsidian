https://react.dev/learn
React app is made up of components. Its components are js functions

DOM : Document Object Model

Virtual DOM : The Virtual DOM in ReactJS is a lightweight, in-memory representation of the actual DOM. React uses it to optimize performance by updating only the parts of the DOM that need to change, instead of re-rendering the entire UI. When a component's state or props change, React creates a new Virtual DOM, compares it with the previous version (using a process called "reconciliation"), and efficiently updates only the necessary elements in the real DOM. This minimizes expensive DOM manipulations, resulting in faster rendering.

Babel in ReactJS converts modern JavaScript and JSX into browser-compatible code.



---
### `create-react-app` (OLD)

+ go to the directory and `npx create-react-app helloworld`
+ and `npm run start` to start hosting locally.

to update `npm install -g npm@latest`
+ `npm -v` to check latest npm version
+ `node -v` to check nodejs version

 **Files You Should Keep**
- `package.json` and `package-lock.json` (Handles dependencies)
- `public/index.html` (Main HTML entry point)
- `src/index.js` (App entry point)
- `src/App.js` (Main component)

>Note :
`package.json` : It records all the dependencies , scripts and metadata about the project.

---
### New

+ `npm create vite@latest` To create React app 

When Vite asks:
Project name: ./ (that means "this folder")
Framework: React
Variant: JavaScript 

then `npm install` To install
and then `npm run dev` To run 


Files You Should Keep
- `package.json` and `package-lock.json` (Handles dependencies)
```
index.html
vite.config.js
eslint.config.js
src/
  App.jsx
  main.jsx
```

**Delete**:
```
src/App.css
src/index.css 
src/assets/    # whole folder
```


---
#### For Tailwind Config https://v3.tailwindcss.com/docs/guides/vite

#### For react-icons
https://www.npmjs.com/package/react-icons
`npm i react-icons` To install react icon

or 

Flaticons for icons

---
#### Fragments 
+ Fragments are used to form a group
+ When returning multiple elements from a component, without fragments, you need to wrap them in a parent element like a `<div>`. This can be unnecessary and result in extra nodes in the DOM.

#### `React.Fragment`
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

#### Empty Wrappers
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



---
### Export & Import
In React (and JavaScript in general), you can use named exports and default exports to share functions, objects, or values between different modules.

#### Named Export
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


#### Using `as` in **export**:
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

#### Using `as` in **Imports**:
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


#### Default export

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



---
#### preventdefault (synthetic event)
+ synthetic events are wrapper around the event object of the real DOM
+ we have to call preventDefault to stop the default behaviour of a synthetic event

```js
// App.jsx
function PreventExample(){
  const handleSubmit=(e)=>{
    e.preventDefault(); // prevent page reload on submit
    alert("Form submitted without reload");
  }


  return(
    <form onSubmit={handleSubmit}>
      <input type="text" placeholder="Enter value"></input>
      <button type="submit">Submit</button>
    </form>
  )
}

export default PreventExample;
```


---

**array destructuring**
```js
const[,,animal]=["Horse","cat","cow"];
console.log(animal); //output: cow
```

>Note :
>+ Events in react are named using camelCase rather than lower case.


---
#### Template literals (backticks)

```js
const name = "Alice";
const age = 30;

const greeting = `Hello, my name is ${name} and I am ${age} years old.`;

console.log(greeting);
// Output: Hello, my name is Alice and I am 30 years old.
```


---
### Props
https://youtu.be/uvEAvxWvwOs
- **Props = properties (read-only inputs)** passed **from parent → child**.
- Think of them like **function arguments**.
- They make components **reusable** and **dynamic**.
- Props are immutable

##### Basic props
```js
// src/App.jsx (Parent)
import Welcome from "./Welcome";

export default function App() {
  return (
    <div>
      <Welcome name="Droid85" />
      <Welcome name="John" />
      <Welcome name="Alice" />
    </div>
  );
}
```

```js
// src/Welcome.jsx  (Child)
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

export default Welcome;
```



##### Props with destructuring
```js
// App.jsx
import Profile from "./Profile";

export default function App(){
  return(
    <>
      <Profile name="Alexa" age={13} />
      <Profile name="Person 2" age={46} />
    </>
  );
}
```

```js
// Profile.jsx
export default function Profile({name,age}){
    return(
        <>
            <h2>Name: {name}</h2>
            <p>Age: {age}</p>
        </>
    )
}
```



##### Props as array/objects
```js
// App.jsx
import List from "./list";

export default function App(){
  const fruits=["Apple","Banana","Mango"];
  return <List items={fruits} />
}
```

```js
// list.jsx
export default function List({items}){
    return(
        <ul>
            {items.map((item,index)=><li key={index}>{item}</li>)}
        </ul>
    );
}
```



##### Props as function (event handler)
```js
// App.jsx
import Button from "./button";

export default function App(){
  const handleClick=()=>{
    alert("Button Clicked");
  }
  return <Button onClick={handleClick} label="Click me" />
}
```

```js
// button.jsx
export default function Button({onClick,label}){
    return <button onClick={onClick}>{label}</button>
}
```


##### Props with Children
- In React, **anything you put between a component’s opening and closing tags** is automatically passed to that component as a special prop called `children`.

```js
// App.jsx
import Card from "./card";

export default function App() {
  return (
    <Card>
      <h2>Inside Card</h2>
      <p>This content is passed as children.</p>
    </Card>
  );
}
```


```js
// card.jsx
export default function Card({ children }) {
  return (
    <div style={{ border: "1px solid gray", padding: "10px" }}>{children}</div>
  );
}
```



##### Default props
```js
// App.jsx
import Greeting from "./greeting";

export default function App(){
  return(
    <>
      <Greeting name="Person 1" />
      <Greeting/>
    </>
  )
}
```


```js
// greeting.jsx
export default function Greeting({ name = "Guest" }) {
  return <p>Hello, {name}</p>;
}
```


##### Props vs State
- **Props**: External inputs, controlled by parent. Immutable.
- **State**: Internal to the component. Mutable.

```js
function Counter({ initial }) {
  const [count, setCount] = React.useState(initial);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```
Here `initial` comes as **props** (from parent), but `count` is **state** (local).



#### Props drilling Example

```js
// App.jsx
import ParentComponent from "./components/ParentComponent";

const App = () => {
  return (
    <>
      <ParentComponent />
    </>
  );
};

export default App;
```


```js
// ParentComponent.jsx
import { useState } from "react";
import ChildComponent from "./ChildComponent";

const ParentComponent = () => {
  const [color, setColor] = useState("#000000");

  return (
    <>
      <h1>Pick a color</h1>
      <input
        type="color"
        onChange={(e) => setColor(e.target.value)}
        value={color}
      />
      <ChildComponent color={color} />
    </>
  );
};
export default ParentComponent;
```


```js
// ChildComponent.jsx
import GrandChildrenComponent from "./GrandChildrenComponent";

const ChildComponent = (props) => {
  return (
    <div
      style={{
        border: `10px solid #000000`,
        marginLeft: "50px",
        padding: "30px",
        fontSize: "30px",
        width: "300px",
      }}
    >
      <GrandChildrenComponent color={props.color} />
    </div>
  );
};
export default ChildComponent;
```


```js
// GrandChildrenComponent.jsx
const GrandChildrenComponent = (props) => {
  return (
    <>
      <p style={{ color: props.color }}>Color: {props.color}</p>
    </>
  );
};

export default GrandChildrenComponent;
```

---
### `useRefs()`
- **Purpose:** Mutable container, survives re-renders, does NOT cause re-render when changed.
+ Refs are used to directly access DOM elements

**Signature:**
```js
const ref = useRef(initialValue);
ref.current; // mutable value
```
 
 **Details:**
 + Can be used to focus on input field and scroll to specific element
- Also used as “instance variables” in function components.

**Pitfalls:**
- Don’t use for state that drives UI. UI won’t update.

**Example**
+ Refs are created using **`React.createRef()`** (in classes)
+ import `useRef` from react and use it to create reference and attached to the element via the ref attribute
+ we can use **`ref.current.value`** to access or modify the value of the input element associated with that ref

```js
// App.jsx
import {useRef} from "react";
function RefExample() {
  const inputRef=useRef(null); // create a ref

  function handleClick(){
    inputRef.current.focus();
  }

  return (
    <div>
    <input ref={inputRef} placeholder="Enter value" />
    <button onClick={handleClick}>Focus Input</button>
    </div>
  )
}

export default RefExample;
```


---
### `useState()`
Functional components can have stateful logic using react hooks
- **Stores dynamic data** (e.g., form inputs, counters).
- **Triggers re-renders** when updated.
- **Component-specific memory** — each component manages its own state.
- Makes UI **interactive** and responsive.
- Without state = static UI.
- Async nature: You can’t immediately read updated value after `setValue`.

```js
import { useState } from "react";

function Counter(){

  const [count,setCount]=useState(0);

  return(
    <>
    <p>You clicked {count} times</p>
    <button onClick={()=>setCount(count+1)}>Click me</button>
    </>
  )
}

export default Counter;
```


**Why functional updates matter (batching!)**
```js
// count starts at 0, in one click handler:
setCount(count + 1);
setCount(count + 1);
// => ends up 1 (because both read the same old count)

setCount(c => c + 1);
setCount(c => c + 1);
// => ends up 2 (each sees the latest)
```


**Why can’t we just change state directly?**

React checks if state **changed** by comparing the old value with the new value:
- If it’s **the same object in memory**, React thinks “nothing changed” → **no re-render**.
- If it’s a **new object/array**, React sees it’s different → **triggers re-render**.

**Example with an object**
```js
const [user, setUser] = useState({ name: "Alex", age: 20 });
```

❌ WRONG: Mutating
```js
user.age = 21;     // directly changing the object
setUser(user);     // React sees: "same object reference"
```

React won’t re-render, because `user` is still the same object in memory, just with a changed property.

✅ RIGHT: Copy + replace
```js
setUser(prev => ({ ...prev, age: prev.age + 1 }));
```

Here:
- `...prev` copies the old object.
- Then we change `age`.
- React sees: “new object!” → re-render.


**Example with an array**
```js
const [todos, setTodos] = useState([{ id: 1, text: "Learn" }]);
```

❌ WRONG: Mutating
```js
todos.push({ id: 2, text: "Build" }); // modifies same array
setTodos(todos);  // same reference, no update
```

✅ RIGHT: Create a new array
```js
setTodos(prev => [...prev, { id: 2, text: "Build" }]);  // add
setTodos(prev => prev.filter(t => t.id !== 1));         // remove
setTodos(prev => prev.map(t => t.id === 1 
  ? { ...t, text: "Learn React deeply" } 
  : t
)); // edit
```

Think of it like this:
- **Mutation** = scribbling on the same paper → React doesn’t notice.
- **Immutability** = giving React a _new sheet of paper_ → React says “oh, this is new, let me redraw.”



#### `useState()` Example

```js
// App.jsx
import { useState } from "react";
import Blog from "./components/Blog";

const App = () => {
  const [formData, setFormData] = useState({title:"",content:""});
  const [blog, setBlog] = useState([]);

  return (
    <Blog
      formData={formData}
      setFormData={setFormData}
      blog={blog}
      setBlog={setBlog}
    />
  );
};

export default App;
```


```js
// Blog.jsx
const Blog = ({ formData, setFormData, blog, setBlog }) => {

  const handleSubmit = (event) => {
    event.preventDefault();
    setBlog((prev) => [...prev, formData]);
    setFormData({ title: "", content: "" }); // clear form data after submit
  };

  const handleDelete=(deleteIndex)=>{
    setBlog(blog.filter((_,index)=>index!==deleteIndex));
  }


  return (
    <div
      style={{
        display: "flex",
        flexDirection: "column",
        justifyContent: "center",
        alignItems: "center",
      }}
    >
      <form
        style={{
          textAlign: "center",
          padding: "5px",
          width: "400px",
          border: "1px solid black",
          borderRadius: "8px",
          display: "flex",
          flexDirection: "column",
          backgroundColor: "#f9f9f9",
          boxShadow: "0px 2px 8px rgba(0,0,0,0.1)",
          gap: "10px"
        }}
        onSubmit={handleSubmit}
      >
        <label htmlFor="title">Title</label>
        <input
          onChange={(e) =>
            setFormData({ title: e.target.value, content: formData.content })
          }
          value={formData.title}
          name="Title"
          placeholder="Enter Title name"
        />
        <label htmlFor="content">Content</label>
        <textarea
          onChange={(e) =>
            setFormData({ title: formData.title, content: e.target.value })
          }
          value={formData.content}
          name="content"
          placeholder="Enter the content"
        />
        <button>Submit</button>
      </form>
      <hr />
      <h2>Blogs</h2>
      {blog.map((post, index) => (
        <div
          key={index}
          style={{
            border: "1px solid #000000",
            borderRadius: "8px",
            backgroundColor: "skyblue",
            margin: "8px",
            padding: "5px",
            maxWidth: "700px",
            width: "100%",
            boxShadow: "0px 2px 8px rgba(0,0,0,0.1)",
          }}
        >
          <h3>{post.title}</h3>
          <p>{post.content}</p>
          <button onClick={()=>handleDelete(index)}>Delete</button>
        </div>
      ))}
    </div>
  );
};
export default Blog;
```




---
### `useReducer()`
https://react.dev/reference/react/useReducer
- **Purpose:** Complex state logic, alternative to `useState`

**Signature:**
```js
const [state, dispatch] = useReducer(reducer, initialState);
```
- **Details:**
    - Keeps state transitions predictable.
    - Useful for forms, big UI state.
    - Its a pure function does not cause any side effect
    
- **Pitfalls:**
    - Avoid huge reducers; sometimes multiple `useState` is cleaner.


---

### `useEffect()`
https://youtu.be/L-1sP3Ljhsg
+ **Purpose:** Side effects (API calls, subscriptions (real time updates), manual DOM manipulation , event listeners).

**Signature:**
`useEffect(function,[dependencies])`

```js
useEffect(() => {
  // effect
  return () => { /* cleanup */ };
}, [dependencies]);
```
- **Details:**
    - Runs **after render**.
    - `useEffect(()=>{},[])` If dependencies are empty `[]`, runs once (componentDidMount).
    - `useEffect(()=>{})` Without dependencies, runs after every re-render.
    - `useEffect(()=>{},[value])`  Runs on mount + when value changes
    - Cleanup runs before unmount, or before next effect run.
    
- **Pitfalls:**
    - Missing dependencies → stale closures.
    - Over-fetching: If you don’t memoize functions, effect may trigger too often.


TODO: Copy notes

week 6 | topic 1 | 

---
### `localStorage`

```js
// App.jsx
import { useEffect, useState } from "react";

const App = () => {
  const [formData, setFormData] = useState({ username: "", email: "" });
  const [users, setUsers] = useState(()=>{
    // load from localStorage on first render
    return JSON.parse(localStorage.getItem("users")) || [];
  });

  useEffect(()=>{
    // save to localStorage whenever users change
    localStorage.setItem("users",JSON.stringify(users));
  },[users]);

  const handleSubmit = (event) => {
    event.preventDefault();
    if (!formData.username || !formData.email) return;
    setUsers((prev)=>[...prev,formData]);
    setFormData({ username: "", email: "" });
  };

  return (
    <>
      <form onSubmit={handleSubmit}>
        <label htmlFor="username">Username:</label><br />
        <input
          name="username"
          placeholder="Enter your username"
          value={formData.username}
          onChange={(e) =>
            setFormData({ username: e.target.value, email: formData.email })
          }
        /><br />
        <label htmlFor="email">Email:</label><br />
        <input
          name="email"
          placeholder="Enter your email"
          value={formData.email}
          onChange={(e) =>
            setFormData({ username: formData.username, email: e.target.value })
          }
        /><br />
        <button>Submit</button>
      </form>
      <hr />
      <h2>Users</h2>
      {users.map((user, index) => (
        <div key={index}>
          <h4>{user.username}</h4>
          <p>{user.email}</p>
        </div>
      ))}
    </>
  );
};

export default App;
```


---
#### `useContext()`
- **Purpose:** Access context values without prop drilling.

**Signature:**
```js
const value = useContext(MyContext);
```

- **Details:**
    - Triggers re-render whenever context value changes.
    - Useful for global-ish state (theme, auth).

- **Pitfalls:**
    - Overuse → unnecessary re-renders of large component trees.
    - Solution: split contexts or memoize.


#### Context API Direct Example
+ Create context
+ Provide context
+ Consume Context

Step 1: Create a context object
```js
// context.jsx
import { createContext } from "react";

const ColorContext=createContext();

export default ColorContext;
```


```js
// App.jsx
import ParentComponent from "./components/ParentComponent";

const App = () => {
  return (
    <>
	    {/* Step 2: Render ParentComponent which will provide context */}
      <ParentComponent />
    </>
  );
};

export default App;
```


```js
// ParentComponent.jsx
import { useState,useRef } from "react";
import ChildComponent from "./ChildComponent";
import ColorContext from "../context";

const ParentComponent = () => {
  const [color, setColor] = useState("#000000");
  const inputRef=useRef(null);

  // Function to trigger input click from anywhere
  const openColorPicker=()=>{
    inputRef.current.click();
  }

  return (
    <>
      <h1>Pick a color</h1>
      <input
        ref={inputRef}
        type="color"
        onChange={(e) => setColor(e.target.value)}
        value={color}
      />
	    {/* Step 3: Provide context values (color + helpers) to children */}
      <ColorContext.Provider value={{color,setColor,openColorPicker}}>
        <ChildComponent  />
      </ColorContext.Provider>
    </>
  );
};
export default ParentComponent;
```


```js
// ChildComponent.jsx
import GrandChildrenComponent from "./GrandChildrenComponent";

const ChildComponent = () => {
  // Note: ChildComponent is NOT directly using context here,
  // but it still has access because GrandChildrenComponent consumes it.
  return (
    <div
      style={{
        border: `10px solid #000000`,
        marginLeft: "50px",
        padding: "30px",
        fontSize: "30px",
        width: "300px",
      }}
    >
      <GrandChildrenComponent/>
    </div>
  );
};
export default ChildComponent;
```


```js
// GrandChildrenComponent.jsx
import { useContext } from "react";
import ColorContext from "../context";

const GrandChildrenComponent = () => {
  const {color,openColorPicker}=useContext(ColorContext);

  return (
    <>
      <p style={{ color: color }}>Color: {color}</p>
      <button onClick={openColorPicker}>Pick color</button>
    </>
  );
};

export default GrandChildrenComponent;
```


But there is another way to consume context values using consumer
```js
// GrandChildrenComponent.jsx
import ColorContext from "../context";

const GrandChildrenComponent = () => {
  return (
    <ColorContext.Consumer>
      {({ color, setColor ,openColorPicker }) => (
        <>
          <p style={{ color: color }}>Color: {color}</p>
          <button onClick={openColorPicker}>Pick color</button>
          <button onClick={() => setColor("#000000")} style={{ marginLeft: "10px" }}>
           Reset Color
          </button>
        </>
      )}
    </ColorContext.Consumer>
  );
};

export default GrandChildrenComponent;
```


#### Encapsulated Provider Pattern (with custom hook)

```js
// App.jsx
import ParentComponent from "./ParentComponent";

const App=()=>{
  return(
    <ParentComponent />
  )
}

export default App;
```


```js
// ColorContent.jsx
import { createContext, useState, useRef, useContext } from "react";

const ColorContext = createContext();

export const ColorProvider = ({ children }) => {
  const [color, setColor] = useState("#000000");
  const inputRef = useRef(null);

  const openColorPicker = () => {
    inputRef.current.click();
  };

  return (
    <ColorContext.Provider value={{ color, setColor, openColorPicker }}>
      <input
        style={{ display: "none" }}
        ref={inputRef}
        type="color"
        value={color}
        onChange={(e) => setColor(e.target.value)}
      />
      {children}
    </ColorContext.Provider>
  );
};

// Optional: custom hook (cleaner than importing useContext every time)
export const useColor=()=>useContext(ColorContext);
```


```js
// ParentComponent.jsx
import { ColorProvider } from "./context/ColorContent";
import ChildrenComponent from "./ChildrenComponent";

const ParentComponent=()=>{
    return(
        <ColorProvider>
            <ChildrenComponent />
        </ColorProvider>
    )
}

export default ParentComponent;
```


```js
// ChildrenComponent.jsx
import GrandChildrenComponent from "./GrandChildrenComponent";

const ChildrenComponent = () => {
  return (
    <div
      style={{ border: "8px solid black", marginLeft: "5px", padding: "5px" }}
    >
      <GrandChildrenComponent />
    </div>
  );
};

export default ChildrenComponent;
```


```js
// GrandChildrenComponent.jsx
import { useColor } from "./context/ColorContent";

const GrandChildrenComponent=()=>{

    const { color, setColor, openColorPicker }=useColor();

    return(
        <>
            <p style={{color: color}}>Color: {color}</p>
            <button onClick={openColorPicker}>Pick Color</button><br/>
            <button onClick={()=>setColor("#000000")}>Reset Color</button>
        </>
    )
}

export default GrandChildrenComponent;
```



---
### `useMemo`
- **Purpose:** Memoize expensive computations.

 **Signature:**
```js
 const memoized = useMemo(() => computeSomething(a, b), [a, b]);
```

- **Details:**
    - Avoids re-running expensive functions if deps don’t change.
    
- **Pitfalls:**
    - Misuse: Don’t wrap everything. It has overhead itself.
    - Use for **expensive calculations** or referential equality (e.g. when passing objects as props).


---
### `useCallback`
- **Purpose:** Memoize functions (so child components don’t re-render unnecessarily).

**Signature:**
```js
const fn = useCallback(() => { doSomething(a); }, [a]);
```

- **Details:**
    - `useCallback(fn, deps)` ≈ `useMemo(() => fn, deps)`.
    
- **Pitfalls:**
    - If you forget dependencies, you freeze stale values.
    - If you add everything in deps blindly, you lose optimization.


---
### `useLayoutEffect`

- **Like useEffect**, but fires **synchronously after DOM mutations, before paint**.
- **When:** Measure DOM size/position before browser paints.
- **Pitfall:** Can block paint → avoid heavy work.


---
### `useImperativeHandle`
- **Purpose:** Customize what a parent gets when using `ref` on a child.

**Signature:**
```js
useImperativeHandle(ref, () => ({ focus: () => inputRef.current.focus() }));
```
+ **Pitfall:** Breaks declarative style → use sparingly.

---
### `useDebugValue`
- **Purpose:** Debugging in React DevTools, mostly for custom hooks.
```js
useDebugValue(isOnline ? 'Online' : 'Offline');
```


TODO:
# 🧩 2. Advanced Built-in Hooks (React 18+)

### **2.1 useId**

- **Purpose:** Generate unique IDs that are consistent across server/client rendering.
    
- Example:
    
    `const id = useId(); <label htmlFor={id}>Name</label> <input id={id} />`
    

---

### **2.2 useTransition**

- **Purpose:** Mark state updates as “non-urgent”.
    
- **Example:**
    
    `const [isPending, startTransition] = useTransition(); startTransition(() => setPage(newPage));`
    
- **Benefit:** Keeps UI responsive while deferring heavy updates.
    

---

### **2.3 useDeferredValue**

- **Purpose:** Defer a changing value until the browser is free.
    
- Example:
    
    `const deferredValue = useDeferredValue(searchQuery);`
    
- Useful for typing search inputs without lag.
    

---

### **2.4 useSyncExternalStore**

- **Purpose:** For subscribing to external stores (Redux, Zustand).
    
- Ensures correctness with concurrent rendering.
    

---

### **2.5 useInsertionEffect**

- **Purpose:** For injecting styles into DOM **before rendering**.
    
- Rare, mostly for CSS-in-JS libraries.
    

---

week6 | topic 1 | lec24 customhook
### Custom Hooks
https://youtu.be/I2Bgi0Qcdvc
A function that starts with `use`, calls other hooks, and returns reusable state/logic.
+ It does not return jsx

- Rules:
    1. Must start with `use`.
    2. Call hooks only at top level (not inside loops, conditions/ifs)).
    3. Treat dependencies seriously (same as `useEffect` etc).
























---

TODO: Rendering components based on condition
TODO: Class Based Components

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






---
# leafletjs
https://leafletjs.com


**leaflet**
https://www.npmjs.com/package/leaflet
+ `npm i leaflet` To install leaflet https://www.npmjs.com/package/leaflet
- `npm i react-leaflet` → React-friendly components that use Leaflet https://www.npmjs.com/package/react-leaflet
- `npm i react-leaftlet-markercluster`  (old) To install markercluster https://www.npmjs.com/package/react-leaflet-markercluster

- check getting started and more documents in https://www.npmjs.com/package/react-leaflet-markercluster






GeoJSON

---



week6 | topic 2 | firebase pending

week 8 | topic 1 |
+ lec 7


