hitesh choudhary: https://youtu.be/KCr-UNsM3vA
https://youtu.be/IDKKB5bm4vM
https://youtu.be/m41aGndJNPU

Yes—conceptually it’s the same pattern as `setState(prev => ...)`, but don’t oversimplify it.

Correct mental model
- **React `setState`**
    ```js
    setTodos(prev => ...)
    ```
    `prev` = previous state

- **Zustand `set`**
    ```js
    set(state => ...)
    ```
    `state` = current store state

These are effectively equivalent:
- `prev` (React) ≈ `state` (Zustand)
- both are **snapshots of current state at update time**

Your examples — 100% correct

These patterns map directly:
```js
setTodos(prev => [...prev, newTodo])        // add
setTodos(prev => prev.filter(...))          // remove
setTodos(prev => prev.map(...))             // update
```

Same thing in Zustand
```ts
set((state) => ({
  todos: [...state.todos, newTodo],
}))

set((state) => ({
  todos: state.todos.filter(...),
}))

set((state) => ({
  todos: state.todos.map(...),
}))
```


Critical difference (this is where people mess up)

React:
```js
setTodos(prev => [...prev, newTodo])
```

Zustand:
```ts
set({ todos: [...] })         // direct update
set(state => ({ ... }))       // computed update
```
Zustand allows **both styles**, React doesn’t.


When to use what (industry rule)

**Use function form (`state => ...`) when:**
- depends on previous state
- multiple updates can race
- anything dynamic

**Use object form when:**
- static assignment
```ts
set({ isDark: true })
```


---
### Two update styles in Zustand

###### Direct update (object form)**

```ts
set({ todos: newTodos })
```
- You **already know the final value**
- No dependency on previous state
- Equivalent to:
```js
setState({ key: value })
```

When it’s safe
```ts
set({ isDark: true })
set({ user: fetchedUser })
```

Functional update (computed form)**
```ts
set((state) => ({
  todos: [...state.todos, newTodo],
}))
```

- You **derive next state from current state**
- Needed when:
    - appending
    - filtering
    - toggling
    - merging


Why both exist (React vs Zustand difference)

In React:
```js
setTodos([...todos, newTodo]) // ❌ can break
setTodos(prev => [...prev, newTodo]) // ✅ safe
```
Reason:
- React state updates are **async + batched**
- `todos` may be stale

In Zustand:
```ts
set({ todos: [...state.todos, newTodo] }) // ❌ impossible (no access)
set((state) => ({ todos: [...state.todos, newTodo] })) // ✅ correct
```

But also:
```ts
set({ isDark: true }) // ✅ safe
```

Zustand gives flexibility because:
- It’s **not tied to React render cycle**
- Updates are **synchronous**
- Store exists outside components


The real rule (don’t mess this up)

Use **object form** when:
- value is independent
- overwrite is intended

```ts
set({ loading: false })
```


Use **function form** when:
- depends on previous state
- multiple updates can happen close together
- arrays/objects are involved

```ts
set((state) => ({
  count: state.count + 1,
}))
```


**Subtle bug example (important)**

Bad:
```ts
const addTodo = (todo) => {
  const todos = useStore.getState().todos
  set({ todos: [...todos, todo] })
}
```
Why it's bad:
- `getState()` can become stale in async flows
- breaks under concurrency

Correct:
```ts
set((state) => ({
  todos: [...state.todos, todo],
}))
```


**Internal behavior (what actually happens)**

Zustand:
- merges state like:

```ts
nextState = { ...currentState, ...partialUpdate }
```

So this:
```ts
set({ isDark: true })
```
does NOT wipe other fields.



**Industry pattern (clean + scalable)**

```ts
const useStore = create((set) => ({
  todos: [],

  addTodo: (todo) =>
    set((state) => ({
      todos: [...state.todos, todo],
    })),

  removeTodo: (id) =>
    set((state) => ({
      todos: state.todos.filter(t => t.id !== id),
    })),
}))
```
Notice:
- Always functional updates for collections
- No direct mutation
- Logic stays inside store (not components)


- Treat **object form** as “assign”
- Treat **function form** as “derive”

If you use object form when derivation is needed → **race bugs**  
If you overuse function form → just slightly verbose, no harm


If you want next level:
- Zustand middleware (`persist`, `immer`, `devtools`)
- splitting store into slices (what real codebases do)
- avoiding unnecessary re-renders with selectors


---

