https://github.com/sudheerj/reactjs-interview-questions#what-is-react
###### What is React?
React is a **JavaScript library for building user interfaces**, mainly for **single-page applications (SPA)**
Key points (interview-ready):
* Uses **component-based architecture** → UI is split into reusable components.
* Uses a **virtual DOM** → updates only changed parts, improving performance.
* Supports **one-way data flow** → data moves parent → child, making state easier to manage.
* Uses **JSX** → allows writing HTML-like syntax inside JavaScript.
* Maintained by **Meta (Facebook)**.

In short: React helps build **fast, scalable, and maintainable front-end applications**.
- **React Hooks**: Introduced in React 16.8, hooks allow using state and other React features in functional components without writing classes.
    
- **Context API**: Provides a way to share values between components without explicitly passing props through every level of the component tree.
    
- **Error Boundaries**: Components that catch JavaScript errors anywhere in their child component tree and display fallback UI instead of crashing.
    
- **Server-Side Rendering (SSR)**: Enables rendering React components on the server before sending HTML to the client, improving performance and SEO.
    
- **Concurrent Mode**: A set of new features (in development) that help React apps stay responsive and gracefully adjust to the user's device capabilities and network speed.
    
- **React Server Components**: A new feature that allows components to be rendered entirely on the server, reducing bundle size and improving performance.
    
- **Suspense**: A feature that lets your components "wait" for something before rendering, supporting code-splitting and data fetching with cleaner code.

---
###### What is JSX?
JSX (JavaScript XML) is a **syntax extension for JavaScript used in React**.

Key points:
- Lets you write **HTML-like code inside JavaScript**.
- Makes UI code **more readable and declarative**.
- Gets **compiled to `React.createElement()` calls** before execution.
- Allows embedding JavaScript using `{}`.

Example:
```jsx
const name = "droid";
const element = <h1>Hello {name}</h1>;
```

Important:  
Browser doesn’t understand JSX directly — it’s transformed (usually by Babel) into plain JavaScript.


---
###### What is the difference between an Element and a Component?
**Element:**
A plain JavaScript object describing what to render in the DOM. It is **immutable**.
Example: `<h1>Hello</h1>`

**Component:**
A reusable function/class that **returns elements**. It is **dynamic and can have logic/state**.
Example:

```jsx
function App() {
  return <h1>Hello</h1>;
}
```
or
```js
const App=()=>{
	return <h1>Hello</h1>;
}
```


---
###### What is state in React?
**State** is data managed by a component that can change over time. When state changes, React re-renders the component to update the UI.
When state changes, React automatically re-renders the component.

Example:
```jsx
const [count, setCount] = useState(0);
```
- `count` is the state value.
- `setCount` updates the state and triggers a re-render.

**Interview one-liner:**  
State is a component's mutable data that React tracks to update the UI when it changes.

---
###### What are props in React?
**Props** are read-only data passed from a parent component to a child component.

**Interview answer:**
Props (properties) are used to pass data from parent components to child components, making components reusable and configurable.

Example:
```jsx
<Child name="John" />
```

Inside Child:
```jsx
function Child({ name }) {
  return <h1>{name}</h1>;
}
```


---
###### What is the difference between state and props?
| State                             | Props                                  |
| --------------------------------- | -------------------------------------- |
| Managed by the component itself   | Passed from parent component           |
| Mutable (can change)              | Read-only (cannot be changed by child) |
| Used for dynamic data             | Used to pass data/configuration        |
| Updating state triggers re-render | Props change when parent re-renders    |

###### Difference between HTML and React Event Handling:
1. **Event naming**
    - HTML: `onclick`
    - React: `onClick` (camelCase)
2. **Prevent default behavior**
    - HTML: `return false`
    - React: `event.preventDefault()`
3. **Event handler**
    - HTML: `onclick="handleClick()"`
    - React: `onClick={handleClick}`

**Interview one-liner:**
React uses camelCase event names, passes function references instead of strings, and uses `preventDefault()` instead of `return false`.

---
###### What are synthetic events in React?
**Synthetic Events** are React's cross-browser wrapper around native browser events.

They provide a **consistent API across all browsers** and work like native events (`preventDefault()`, `stopPropagation()`).

Example:
```jsx
function handleClick(e) {
  e.preventDefault();
  console.log(e.nativeEvent); // Access native browser event
}
```
Synthetic Events are React's normalized event system that wraps native browser events to ensure consistent behavior across different browsers.

---
###### Inline Conditional Expressions
**Inline Conditional Expressions** are expressions used directly inside JSX to conditionally render UI.

Common approaches:
- Ternary operator (`condition ? A : B`)
- Logical AND (`condition && A`)

Example:
```jsx
{isLoggedIn ? <Home /> : <Login />}
```

```jsx
{messages.length > 0 && <Notification />}
```

**Interview one-liner:**
> Inline conditional expressions allow conditional rendering in JSX using operators like `? :` and `&&`.

---
###### Key
**Key** is a special React prop used to uniquely identify elements in a list.

Example:
```jsx
todos.map(todo => (
  <li key={todo.id}>{todo.text}</li>
))
```

Benefits:
- Helps React identify added, removed, or updated items.
- Improves rendering performance.
- Preserves component state correctly.

Interview one-liner:
A key is a unique identifier for list items that helps React efficiently update and re-render elements.

Note: Prefer unique IDs over array indexes as keys.

---
(imp)

**Real DOM**
- The actual DOM rendered by the browser.
- Every change updates the browser's DOM tree directly.
- DOM operations (create, update, remove elements) are relatively expensive.
- Frequent updates can hurt performance.

###### What is Virtual DOM?
**Virtual DOM** is a lightweight, in-memory copy of the real DOM maintained by React.
React creates a new Virtual DOM whenever state or props change.
When state or props change:
1. React updates the Virtual DOM.
2. Compares it with the previous Virtual DOM **(Diffing algo used in Reconciliation).**
3. Updates only the changed parts in the real DOM.

Benefits:
- Faster UI updates
- Better performance
- Fewer direct DOM manipulations

Interview one-liner:
Virtual DOM is a lightweight copy of the real DOM that React uses to efficiently update only the changed parts of the UI.
"The Virtual DOM doesn't make the DOM faster. It reduces unnecessary DOM operations by batching and minimizing updates, which improves rendering efficiency."

| Virtual DOM                      | Real DOM                           |
| -------------------------------- | ---------------------------------- |
| JavaScript object representation | Actual browser DOM                 |
| Fast to manipulate               | Expensive to manipulate            |
| Updates happen in memory first   | Updates happen directly in browser |
| Uses diffing algorithm           | No diffing                         |
| Updates only changed nodes       | May update more than necessary     |
| Improves UI performance          | Slower for frequent updates        |

---
###### How Virtual DOM works:
1. React creates a Virtual DOM from JSX.
2. State/props change → React creates a new Virtual DOM.
3. React compares old and new Virtual DOMs (**diffing**).
4. Identifies only the changed elements (**reconciliation**).
5. Updates only those parts in the Real DOM.

When state or props change, React creates a new Virtual DOM, compares it with the previous one, and updates only the changed parts of the Real DOM for better performance.

---

**Reconciliation** is the process React uses to update the UI efficiently.
When state or props change, React:
1. Creates a new Virtual DOM.
2. Compares it with the previous Virtual DOM (**diffing**).
3. Updates only the changed parts of the Real DOM.

Reconciliation is React's process of comparing the old and new Virtual DOM and updating only the changed parts of the Real DOM.

---
###### What is React Fiber?
**React Fiber** is React's reconciliation engine introduced in React 16.
It improves rendering by allowing React to:
- Prioritize updates
- Pause and resume rendering work
- Perform asynchronous rendering
React Fiber is the rendering engine that enables React to prioritize, interrupt, and efficiently process UI updates for better performance and responsiveness.

**Main goal of React Fiber:**
To make React rendering more efficient, responsive, and interruptible by breaking rendering work into smaller units and prioritizing important updates.

Key benefits:
- Incremental rendering
- Prioritized updates
- Interruptible rendering
- Better support for animations and user interactions
- Foundation for Concurrent React and Suspense

The main goal of React Fiber is to improve UI responsiveness by enabling React to prioritize, pause, and resume rendering work.


---
###### Q. setCount, React.memo
```jsx
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>

      <Child />
    </>
  );
}

function Child() {
  console.log("Child rendered");
  return <h1>Hello</h1>;
}
```
Every time you click Increment:
- Does Child re-render?
- Why?
- How would you prevent unnecessary re-renders?
- Would useMemo or React.memo be the correct solution here? Explain why.

Every time you click **Increment**, does `Child` re-render?
**Yes.**

Why?
- `setCount` updates the state in `Parent`.
- State update causes `Parent` to re-render.
- By default, **all children of a re-rendered parent also re-render**, so `Child` renders again even though it has no props or state.

How to prevent unnecessary re-renders?
Wrap `Child` with `React.memo`.
```jsx
const Child = React.memo(function Child() {
  console.log("Child rendered");
  return <h1>Hello</h1>;
});
```

- `React.memo` skips re-rendering if the component's **(only) props have not changed**.
- Since `Child` receives no props, it renders only once.

`useMemo` or `React.memo`?
**Correct answer: `React.memo`**
- **`React.memo`** → Memoizes a **component** and prevents unnecessary re-renders.
- **`useMemo`** → Memoizes a **computed value**, not a component.


---

###### React.memo, useCallback
Child is wrapped in React.memo, yet it still re-renders every time Parent renders.
Why?
How would you fix it?
```jsx
const Child = React.memo(function Child({ onClick }) {
  console.log("Child rendered");
  return <button onClick={onClick}>Child</button>;
});

function Parent() {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>

      <Child onClick={() => console.log("Hi")} />
    </>
  );
}
```

```
// Output
Parent rendered
Child rendered

// Click Increment
Parent rendered
Child rendered

// Click Increment again
Parent rendered
Child rendered
```


using `usecallBack`
```jsx
import React, { useState, useCallback } from "react";

const Child = React.memo(function Child({ onClick }) {
  console.log("Child rendered");
  return <button onClick={onClick}>Child</button>;
});

export default function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Hi");
  }, []);

  console.log("Parent rendered");

  return (
    <>
      <h2>Count: {count}</h2>

      <button onClick={() => setCount((prev) => prev + 1)}>
        Increment
      </button>

      <Child onClick={handleClick} />
    </>
  );
}
```

```
// Ouput
Parent rendered
Child rendered

// Click Increment
Parent rendered

// Click Increment again
Parent rendered
```

Why does `Child` re-render even with `React.memo`?
`React.memo` only skips a re-render if **all props are shallowly equal** to the previous render.

Here, the `onClick` prop is:
```jsx
<Child onClick={() => console.log("Hi")} />
```
Every time `Parent` re-renders, this arrow function is **recreated**, producing a **new function reference**.

So React compares:
```js
prevProps.onClick === nextProps.onClick
// false
```
Since the prop reference changed, `React.memo` considers the props different and re-renders `Child`.

Fix
Memoize the function using `useCallback` so its reference remains stable.
```jsx
const handleClick = useCallback(() => {
  console.log("Hi");
}, []);

<Child onClick={handleClick} />
```

Now:
```js
prevProps.onClick === nextProps.onClick
// true
```
Since the props are unchanged, `React.memo` skips the re-render.

---
###### useEffect, useLayoutEffect
Explain the difference between:
- `useEffect`
- `useLayoutEffect`

Specifically answer:
1. When does each run?
2. Which runs before the browser paints?
3. When would you choose `useLayoutEffect` over `useEffect`?
4. Why shouldn't `useLayoutEffect` be used everywhere?
Take your time. I'm looking for an understanding of the browser rendering lifecycle, not just the API definitions.


useEffect vs useLayoutEffect

When does each run?
- **useEffect**
    - React updates the DOM.
    - Browser paints the UI.
    - Then `useEffect` executes.
- **useLayoutEffect**
    - React updates the DOM.
    - `useLayoutEffect` executes.
    - Browser paints afterward.

Which runs before the browser paints?
**useLayoutEffect**
It executes **before paint**, allowing you to measure or modify the DOM without the user seeing intermediate changes.

When would you choose `useLayoutEffect`?
Use it when you need **synchronous DOM work** before the screen is displayed.

Examples:
- Measuring element size or position (`getBoundingClientRect()`).
- Setting scroll position.
- Preventing layout flicker.
- Positioning tooltips, modals, or popovers before paint.
For everything else (API calls, timers, event listeners), use **`useEffect`**.


Why shouldn't `useLayoutEffect` be used everywhere?
Because it **blocks the browser from painting**.

If it performs expensive work:
- UI rendering is delayed.
- The page feels less responsive.
- Performance suffers.
`useEffect` is preferred because it lets the browser paint first, resulting in smoother rendering.


Browser Rendering Lifecycle
```text
React Render
      ↓
DOM Updated
      ↓
useLayoutEffect
      ↓
Browser Paint 🎨
      ↓
useEffect
```


---
###### useState Functional update
```jsx
const [count, setCount] = useState(0);

function handleClick() {
  setCount(count + 1);
  setCount(count + 1);
  setCount(count + 1);
}
```

When the button is clicked:
- What will count become?
- Why?
- How would you make it increment by 3 instead of 1?
- Explain how React batches state updates.

What will `count` become?
✅ **`count` becomes `1`**, not `3`.

Why?
Each `setCount(count + 1)` uses the **same snapshot** of `count` from the current render.

If `count` is `0`, React receives:
```jsx
setCount(1);
setCount(1);
setCount(1);
```
Since all updates set the same value, the final state is **1**.

How would you increment by 3?
Use the **functional update** form.
```jsx
setCount(prev => prev + 1);
setCount(prev => prev + 1);
setCount(prev => prev + 1);
```

Result:
```text
0 → 1 → 2 → 3
```
Each update receives the **latest state**, not the stale value from the render.

How does React batch state updates?
React **batches multiple state updates** occurring in the same event into a **single re-render** for better performance.

During batching:
- State updates are **queued**.
- React processes them together.
- The component re-renders **once** with the final state.


---

###### Rendering list of 10k users
Assume you're rendering a list of **10,000 users**:

```jsx
users.map(user => (
  <UserCard key={user.id} user={user} />
))
```
The page becomes slow.

As a React developer, how would you optimize this?
I'm **not** looking for just "`React.memo`".
Think like you're building a production application.
Mention every optimization you know, explain why you'd use it, and in what situations.

Optimizing a List of 10,000 Users
```jsx
users.map(user => (
  <UserCard key={user.id} user={user} />
))
```

**Virtualization (Most Important)** 
Render **only visible items** instead of all 10,000.

Why?
- Reduces DOM nodes drastically.
- Best solution for very large lists.

Libraries
- `react-window`
- `react-virtualized`
- `@tanstack/react-virtual`

**React.memo**
```jsx
const UserCard = React.memo(UserCard);
```

Why?
- Prevents unnecessary re-renders when props haven't changed.

Use when
- Component is expensive to render.
- Props are stable.


**Stable Props (`useMemo` / `useCallback`)**
```jsx
const handleClick = useCallback(() => {}, []);
```

Why?
- Prevents new object/function references.
- Makes `React.memo` effective.

**Pagination / Infinite Scrolling**
Load data in chunks instead of all at once.

Why?
- Faster initial load.
- Lower memory usage.

**Stable Keys**
```jsx
key={user.id}
```
Avoid:
```jsx
key={index}
```

Why?
- Helps React reconcile efficiently.
- Prevents unnecessary remounting.


**Minimize Parent Re-renders**
- Keep state close to where it's used.    
- Split large components.
- Avoid updating the whole list for one item.

**Debounce / Throttle Search**
For filtering/search:
```text
User types → Wait 300ms → Filter once
```

Why?
- Avoids re-rendering thousands of items on every keystroke.

**Concurrent Features (React 18+)**
- `useDeferredValue`
- `useTransition`

Why?
- Keeps UI responsive during expensive updates like filtering large lists.


**Lazy Load Heavy Components**
```jsx
const UserCard = React.lazy(() => import("./UserCard"));
```

Why?
- Reduces initial bundle size.

**Profile Before Optimizing**
Use:
- React DevTools Profiler
- Browser Performance tab

Why?
- Optimize the actual bottleneck, not assumptions.


|Priority|Optimization|Impact|
|---|---|---|
|⭐⭐⭐⭐⭐|Virtualization|Highest|
|⭐⭐⭐⭐|Pagination / Infinite Scroll|Very High|
|⭐⭐⭐⭐|React.memo|High|
|⭐⭐⭐|Stable props (`useMemo`, `useCallback`)|High|
|⭐⭐⭐|Stable keys|High|
|⭐⭐|Minimize parent re-renders|Medium|
|⭐⭐|`useDeferredValue` / `useTransition`|Medium|
|⭐|Lazy loading|Situational|
|⭐⭐⭐⭐⭐|Profiling|Essential|

---

TODO: Context api







---

**Controlled Components** are form elements whose values are controlled by React state.
Example:
```jsx
const [name, setName] = useState("");

<input
  value={name}
  onChange={(e) => setName(e.target.value)}
/>
```
A controlled component is a form element whose value is managed by React state, making React the single source of truth.


**Uncontrolled Components** are form elements whose data is managed by the DOM instead of React state.
React accesses the value using a **ref**.

Example:
```jsx
const inputRef = useRef();

<input ref={inputRef} />
```
An uncontrolled component stores form data in the DOM and React accesses it using refs when needed.

---

| createElement                                | cloneElement                                    |
| -------------------------------------------- | ----------------------------------------------- |
| Creates a new React element from scratch     | Clones an existing React element                |
| Used internally by JSX                       | Used to modify/add props to an existing element |
| `React.createElement(type, props, children)` | `React.cloneElement(element, props)`            |

---

**Lifting State Up** is the process of moving shared state from child components to their closest common parent component.
This allows multiple child components to access and update the same data through props.

---

**Higher-Order Component (HOC)** is a function that takes a component and returns a new enhanced component.
```jsx
const EnhancedComponent = withAuth(Component);
```
Common uses:
- Authentication
- Data fetching
- Logging
- Permission checks

A Higher-Order Component (HOC) is a function that wraps a component and adds extra functionality or behavior without modifying the original component.

---

**`children`** is a special React prop used to pass content between a component's opening and closing tags.

Example:
```jsx
<Card>
  <h1>Hello</h1>
</Card>
```

Inside `Card`:
```jsx
function Card({ children }) {
  return <div>{children}</div>;
}
```

The `children` prop allows a component to receive and render nested content, making wrapper and layout components reusable.

---
###### `className` vs `class`
**React uses `className` instead of `class`** because `class` is a reserved keyword in JavaScript.

`className` also matches the DOM API (`element.className`), and React converts it to the HTML `class` attribute when rendering.

---
###### Fragments
**Fragments** let you group multiple elements without adding an extra DOM node.
 Fragments allow a component to return multiple elements without creating unnecessary wrapper elements in the DOM.
 
Syntax:
```jsx
<>
  <h1>Hello</h1>
  <p>World</p>
</>
```
Or:
```jsx
<React.Fragment>...</React.Fragment>
```

---

**Why use Fragments instead of `<div>`?**
- Avoids creating unnecessary DOM elements.
- Improves performance (slightly).
- Prevents layout issues with Flexbox/Grid.
- Keeps the DOM cleaner and easier to debug.

Fragments group multiple elements without adding extra DOM nodes, resulting in cleaner DOM and avoiding layout issues.

---
###### Portals
**Portals** allow React to render a component into a DOM node outside its parent DOM hierarchy.
Portals let React render components outside the parent DOM tree while preserving the React component hierarchy, making them ideal for modals and overlays.

They are commonly used for:
- Modals
- Tooltips
- Popups
- Dropdowns

Example:
```jsx
ReactDOM.createPortal(<Modal />, document.body);
```

---

**Styles in React** are applied using the `style` prop, which accepts a **JavaScript object** with **camelCase** CSS properties.

Example:
```jsx
const style = {
  color: "blue",
  backgroundColor: "black",
};

<div style={style}>Hello</div>
```

---

**React events differ from HTML events in two ways:**
- Event names use **camelCase** (`onClick` instead of `onclick`).
- Event handlers are passed as **function references**, not strings.    

Example:
```jsx
<button onClick={handleClick}>Click</button>
```

---

Using **array indexes as keys** can cause incorrect UI updates and loss of component state when items are added, removed, or reordered.

**Avoid using array indexes as keys** because when items are added, removed, or reordered, React may associate the wrong component with the wrong data, causing incorrect rendering and state bugs. Instead, use a **stable, unique ID** (e.g., `todo.id`).

Example:
```jsx
// ✅ Preferred
todos.map(todo => <Todo key={todo.id} {...todo} />)

// ❌ Avoid (if list can change)
todos.map((todo, index) => <Todo key={index} {...todo} />)
```
The important point is not that `id` exists as a property, but that the key must be **stable and unique**. `todo.id` is just the most common example. If your data has another unique field (e.g., `email`, `uuid`, `slug`), that works just as well.

---

**Components can be conditionally rendered** using JavaScript conditions inside JSX.
Common ways:
- `&&` for rendering only if a condition is true.
- Ternary operator (`? :`) for if-else rendering.

Example:
```jsx
{isLoggedIn && <Dashboard />}

{isLoggedIn ? <Dashboard /> : <Login />}
```

React conditionally renders components using JavaScript expressions such as `&&` and the ternary (`? :`) operator inside JSX.

---

**React component names must start with a capital letter** so React can distinguish them from HTML elements.
- **Uppercase** → Treated as a React component.
- **Lowercase** → Treated as an HTML tag.

Example:
```jsx
<MyComponent />   // ✅ React component
<div />           // ✅ HTML element
```

---

**Looping in JSX** is typically done using the `map()` method.

Example:
```jsx
{items.map(item => (
  <Component key={item.id} />
))}
```

`for` loops cannot be used directly inside JSX because JSX only allows **expressions**, not **statements**.

In React, lists are rendered using `Array.map()`, which returns an array of JSX elements.

---

You **cannot** interpolate variables inside quoted JSX attributes.

❌ Incorrect:
```jsx
<img src="images/{image}" />
```

✅ Correct:
```jsx
<img src={"images/" + image} />
```
or
```jsx
<img src={`images/${image}`} />
```

In JSX, JavaScript expressions must be placed inside `{}` as the entire attribute value, not inside quoted strings.

---

Apply classes conditionally by using JavaScript expressions (e.g., ternary operator or template literals) inside the `className` prop.

Use a **ternary operator** or **template literals** inside `className`.

Example:
```jsx
<div className={isVisible ? "show" : "hidden"} />
```
or
```jsx
<div className={`btn-panel ${isVisible ? "show" : "hidden"}`} />
```

---

In React, use **`htmlFor`** instead of `for` in a `<label>` because `for` is a reserved JavaScript keyword.

Example:
```jsx
<label htmlFor="user">User</label>
<input id="user" type="text" />
```

React uses `htmlFor` instead of `for` to associate a label with an input, since `for` is a reserved keyword in JavaScript.

---

###### How to focus an input element on page load ?
To focus an input on page load, use `useRef` to access the input element and call `focus()` inside `useEffect`.
Use **`useRef`** to reference the input and **`useEffect`** to focus it after the component mounts.

Example:
```jsx
const inputRef = useRef();

useEffect(() => {
  inputRef.current.focus();
}, []);

<input ref={inputRef} />
```


---
### React Router
###### What is React Router?
React Router is a routing library for React that enables client-side navigation between pages without reloading the browser.

###### What is the difference between client-side routing and server-side routing?
- **Client-side routing:** React updates the UI without refreshing the page.
- **Server-side routing:** Every navigation sends a new request to the server.

###### What is BrowserRouter?
`BrowserRouter` uses the HTML5 History API to manage navigation and clean URLs. It is the most commonly used router for React web applications.

###### What are Routes and Route?
- `Routes` is a container for route definitions.    
- `Route` maps a URL path to a React component.

Example:
```jsx
<Routes>
  <Route path="/" element={<Home />} />
</Routes>
```

###### How do you navigate programmatically in React Router v6?
Use the `useNavigate()` hook.
```jsx
const navigate = useNavigate();
navigate("/dashboard");
```

###### What is the difference between `Link` and `NavLink`?
- `Link` is used for navigation.
- `NavLink` also provides styling for the active route.

###### What is `useNavigate`?
`useNavigate` is a hook used for programmatic navigation between routes.

###### What is `useParams`?
`useParams` retrieves dynamic URL parameters.

Example:
```jsx
<Route path="/user/:id" element={<User />} />
```

```jsx
const { id } = useParams();
```

###### What is `useLocation`? 
`useLocation` returns information about the current URL, such as pathname, search query, and state.

###### What is `useSearchParams`?
It is used to read and update query parameters.

```jsx
const [searchParams] = useSearchParams();
searchParams.get("page");
```

###### What is a Dynamic Route?
A route that contains URL parameters.

Example:
```jsx
/user/:id
```

###### What is Nested Routing?
Nested routing allows rendering child routes inside parent routes using `<Outlet />`.

###### What is `<Outlet>`?
`<Outlet>` is a placeholder where nested route components are rendered.

###### What is Protected Routing?
Protected routes restrict access to authenticated users by checking authentication before rendering a page.

###### What is Lazy Loading in React Router?
Lazy loading loads route components only when needed, reducing the initial bundle size.

Usually implemented with:
- `React.lazy()`
- `Suspense`

###### What is the difference between `navigate()` and `navigate(..., { replace: true })`?
- `navigate()` adds a new entry to browser history.
- `replace: true` replaces the current history entry.

###### What are URL Parameters and Query Parameters?
- URL Parameter: `/users/25`
- Query Parameter: `/users?page=2`

###### How do you pass data between routes?
Using:
- URL parameters
- Query parameters
- Navigation state
- Global state (Context/Redux)

---
### React testing

###### What is Jest?
Jest is a JavaScript testing framework used to write and run unit and integration tests.

###### What is React Testing Library (RTL)?
React Testing Library is used to test React components by focusing on user behavior rather than implementation details.

###### Why is RTL preferred over Enzyme?
RTL encourages testing the application the way users interact with it, making tests more reliable and less coupled to implementation.

###### Difference between Jest and RTL?

|Jest|RTL|
|---|---|
|Test runner & assertion library|Library for testing React components|
|Runs tests|Renders components and simulates user interactions|

**One-liner:** Jest runs the tests, while React Testing Library helps test React components.

###### How do you test a button click?
Use `render`, `screen`, and `userEvent`.

###### What is `render()`?
`render()` mounts a React component into a virtual DOM for testing.

###### What is `screen`?
`screen` provides methods to query rendered elements.
Example:
```js
screen.getByText("Login");
```

###### What is `userEvent`?  
`userEvent` simulates real user interactions such as clicking, typing, and selecting.

###### Difference between `fireEvent` and `userEvent`?
- `fireEvent` triggers DOM events directly.
- `userEvent` simulates actual user behavior and is preferred.

###### What are unit, integration, and E2E tests?
- **Unit:** Tests a single function/component.
- **Integration:** Tests multiple components working together.
- **E2E:** Tests the entire application flow.

---
### Redux
###### What is Redux?
Redux is a state management library that stores the application's global state in a centralized store.

###### Why use Redux?
Redux is used to manage shared application state across multiple components, making state predictable and easier to debug.

###### What is Redux Toolkit (RTK)?
Redux Toolkit is the official, recommended way to write Redux. It reduces boilerplate and simplifies Redux development.

###### What is a Store?
The store is the central place where the application's global state is stored.

###### What is an Action?
An action is a plain JavaScript object that describes what happened.

Example:
```js
{ type: "cart/addItem", payload: item }
```

###### What is a Reducer?
A reducer is a pure function that takes the current state and an action, then returns the updated state.

###### What is dispatch()?
`dispatch()` sends an action to the Redux store, triggering the reducer to update the state.

###### What is useSelector()?
`useSelector()` reads data from the Redux store.

###### What is useDispatch()?
`useDispatch()` returns the dispatch function used to send actions.

###### Redux vs Context API?

|Context API|Redux|
|---|---|
|Simple global state|Complex global state|
|Small apps|Large apps|
|No DevTools|Redux DevTools|
|Minimal setup|Better scalability|

Context is suitable for simple shared state, while Redux is better for complex application state.

###### When should you use Redux?
Use Redux when multiple components need shared global state, such as authentication, cart, user profile, or notifications.


