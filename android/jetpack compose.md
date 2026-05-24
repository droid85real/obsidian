
`ctrl+alt+L` to auto format
`alt+enter` to import option

---
###### **ROADMAP ANDROID**
https://medium.com/@anandgaur2207/jetpack-compose-roadmap-for-android-developers-7c4ebbf6638f
https://github.com/skydoves/android-developer-roadmap
https://www.androidengineers.in/roadmap/android-fundamentals
https://www.androidengineers.in/roadmap

---

docs : https://developer.android.com/get-started/overview

jetpack compose Tutorial
- cheezy code: https://www.youtube.com/playlist?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev
- android knowledge: https://www.youtube.com/playlist?list=PLQ_Ai1O7sMV33aJHfqR-vquGZE1OCOS51

android basics by philipp lackner: https://youtube.com/playlist?list=PLQkwcJG4YTCSVDhww92llY3CAnc_vUhsm&si=62TwOgP6TgtsaUAI


freecodecamp: https://youtu.be/blKkRoZPxLc looks good but dont have time now

shivam sharma TODO: https://youtu.be/xBKQ01LRuuE  some jetpackcompose project

cheezycode TODO: https://youtu.be/uUBcyvw3uDE?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev


---
###### **Splash Screen**
android knowledge: https://youtu.be/bvQym_hszeI?list=PLQ_Ai1O7sMV33aJHfqR-vquGZE1OCOS51

check code here: https://github.com/droid85real/JetpackComposeUI/commit/cf21ade8b7ea52fb273fd4966f71078ea07050e4

---
###### **Text Composable and modifiers**
AK: https://youtu.be/RMQPHljE82I?list=PLQ_Ai1O7sMV33aJHfqR-vquGZE1OCOS51

---
###### **Row, Column & Box Layout**
AK: https://youtu.be/YbVm9Ue_J7E?list=PLQ_Ai1O7sMV33aJHfqR-vquGZE1OCOS51

Box layout for creating nested layout


---
###### **Alignment & Arrangement**
AK: https://youtu.be/bo5TAnctPCA?list=PLQ_Ai1O7sMV33aJHfqR-vquGZE1OCOS51


---
###### **Text , Image, Button, TextField composable**
cheezy code: https://youtu.be/0mXbFfYzVLw?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev


---
###### **textField compose states vs react input states**
composable function by shivam sharma https://youtu.be/U5dE-_E1wsg?t=3796

**React (what you already know)**

```jsx
import { useState } from "react";

function TextInput() {
  const [text, setText] = useState("");

  return (
    <div>
      <input
        value={text}
        onChange={(e) => setText(e.target.value)}
      />
      <p>{text}</p>
    </div>
  );
}
```

**Key ideas**
- `useState` → state holder
- `value={text}` → controlled input
- `onChange` → updates state
- UI re-renders when state changes

**Jetpack Compose (Android equivalent)**

```kotlin
@Composable
fun TextInput() {
    var text by remember { mutableStateOf("") }

    Column {
        TextField(
            value = text,
            onValueChange = { text = it } // onValueChange = { newValue -> text = newValue }
        )
        Text(text)
    }
}
```

**Same ideas, different clothes**
- `remember { mutableStateOf("") }` → state holder
- `value = text` → controlled input
- `onValueChange` → updates state
- UI recomposes automatically

**Direct mental mapping (important)**
- `useState` ⇔ `remember { mutableStateOf }`
- `setText(...)` ⇔ `text = it`
- JSX ⇔ Kotlin function calls
- Re-render ⇔ recomposition
- Component ⇔ `@Composable` function


simple login page app by AK: https://youtu.be/T4A1TtF-g5U?si=2Bn6ReR3JlAe80Hd


---
###### **List, Lazy Column, Lazy Row**
AK: https://youtu.be/zf6QJemVs2k?list=PLQ_Ai1O7sMV33aJHfqR-vquGZE1OCOS51

lazyColumn and LazyRow are recyclerview

---
###### **Floating Action Button**
AK: https://youtu.be/ppbyVn2SJ9Y?list=PLQ_Ai1O7sMV33aJHfqR-vquGZE1OCOS51

---
###### **Cards**
AK: https://youtu.be/4JoCUPVzqMo?list=PLQ_Ai1O7sMV33aJHfqR-vquGZE1OCOS51

---
###### **Checkboxes**
AK: https://youtu.be/lH9vyVuCK7o?list=PLQ_Ai1O7sMV33aJHfqR-vquGZE1OCOS51



---
###### **reuseable composable** 
https://youtu.be/z2bS2btp_AI?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev

###### **recomposition**
https://youtu.be/hl17pJFJmGc?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev

###### **recompose**
https://developer.android.com/develop/ui/compose/mental-model

###### **State concept, Hoisting and unidirectional flow**
cheezycode: https://youtu.be/zdCrYONv-ec?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev
AK: https://youtu.be/ClWcRPJ3Eyc?list=PLQ_Ai1O7sMV33aJHfqR-vquGZE1OCOS51
state management by easy tutor: https://youtu.be/ekB0w7tkG7k?list=PLgpnJydBcnPA5aNrlDxxKWSqAma7m3OIl

On rotate whole activity gets reloaded and hence loses states as well so we use `remembeSavable` which utilises the bundle also we can use viewmodel

ex-01 app https://youtu.be/tINJacwQFfQ?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev

###### **side effects**
sideeffect: https://youtu.be/r77aVJLh14g?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev

###### **`launchEffect`**
https://youtu.be/r77aVJLh14g?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev

**`LaunchedEffect`** in Jetpack Compose is used to **run a coroutine (side-effect)** when a composable enters the composition or when a given **key changes**.

In ultra-short terms:  
It lets you run background work (like API call, delay, navigation, animation trigger) tied to UI lifecycle.

Example:
```kotlin
LaunchedEffect(Unit) {
    // Runs once when composable appears
}
```

Think of it as Compose’s safe way to say: _“Hey, run this async task when this UI shows or updates.”_

**Similarity with React `useEffect`**
- Both run side effects
- Both re-run when dependency/key changes
- Both are lifecycle aware

###### **Coroutine**
cheezycode: https://youtu.be/0rKO3npQ7yg

A coroutine is **a lightweight task that can pause and resume without blocking a thread**.  
Not a thread. Not magic. Just cooperative scheduling.

Threads are expensive. Coroutines are cheap.

The core mental model (lock this in)
- **Thread** = worker
- **Coroutine** = job
- **Dispatcher** = which worker runs the job
- **Scope** = who owns the job (and kills it)

If you mess up **scope**, you leak work.  
If you mess up **dispatcher**, you freeze UI.

**Coroutine scopes (why they matter)**
- A coroutine **must live inside a scope**.
- Scope answers: “When should this coroutine die?”

Examples:
- `viewModelScope` → dies when ViewModel dies
- `lifecycleScope` → dies when Activity/Fragment dies


Basic coroutine launch (minimum viable pattern)

```kotlin
CoroutineScope(Dispatchers.Main).launch {
    // runs on main thread
}
```

This is fine for demos.  
**Do NOT do this in real Android code** unless you enjoy leaks.

**Correct Android pattern (lifecycle-aware)**

In Activity / Fragment

```kotlin
lifecycleScope.launch {
    // auto-cancelled when Activity/Fragment is destroyed
}
```
`launch` starts a coroutine


In ViewModel (most common)

```kotlin
class MyViewModel : ViewModel() {

    fun loadData() {
        viewModelScope.launch {
            // safe, lifecycle-aware
        }
    }
}
```

If you remember only one thing:  
**UI → lifecycleScope / viewModelScope**

**Dispatchers (when + why)**

```kotlin
Dispatchers.Main     // UI work only
Dispatchers.IO       // network, DB, file
Dispatchers.Default  // CPU-heavy work
```

**Correct usage example**

```kotlin
viewModelScope.launch {
    val data = withContext(Dispatchers.IO) {
        api.fetchUsers()   // background
    }

    textView.text = data.size.toString() // back on Main
}
```

`withContext` = switch thread, suspend, then come back.


**Sequential code that is actually async**

This looks blocking. It isn’t.

```kotlin
viewModelScope.launch {
    val user = fetchUser()
    val posts = fetchPosts(user.id)
    show(posts)
}
```

Behind the scenes, the coroutine **suspends**, frees the thread, and resumes later.

That’s the whole selling point.


Long-running task problem (why coroutines exist)

❌ Bad (freezes UI):

```kotlin
button.setOnClickListener {
    Thread.sleep(5000)
    textView.text = "Done"
}
```

✅ Good:

```kotlin
button.setOnClickListener {
    lifecycleScope.launch {
        delay(5000) // non-blocking
        textView.text = "Done"
    }
}
```

`delay()` suspends the coroutine, **not** the thread.


**Looper & Message Queue (only what matters)**
- Main thread has a **Looper**
- Looper pulls tasks from a **MessageQueue**
- Coroutines scheduled on `Dispatchers.Main` post work into that queue
- If you block the thread → queue stops → UI freezes

Coroutines don’t replace the looper.  
They **cooperate with it**.


**Cancellation (silent but deadly)**

```kotlin
viewModelScope.launch {
    repeat(10) {
        delay(1000)
        println(it)
    }
}
```

If ViewModel is cleared → coroutine is cancelled automatically.

Manual check (rare but useful):

```kotlin
if (!isActive) return
```


GlobalScope (use only if you know the consequences)

```kotlin
GlobalScope.launch {
    // lives until app process dies
}
```

Use cases:
- Analytics
- App-wide background logging

Everything else → **don’t**.


**Parallel work (real concurrency)**

```kotlin
viewModelScope.launch {
    val a = async { loadA() }
    val b = async { loadB() }

    val result = a.await() + b.await()
}
```

Use `async` only when results are independent.


**Common beginner mistakes (avoid these)**
- Launching coroutines without a scope
- Doing network calls on `Dispatchers.Main`
- Using `GlobalScope` everywhere
- Thinking coroutines = threads
- Forgetting cancellation exists


**One-page rulebook (save this)**
- UI work → `Main`
- Network/DB → `IO`
- CPU-heavy → `Default`
- UI layer → `lifecycleScope`
- ViewModel → `viewModelScope`
- Never block (`sleep`, heavy loops) on Main
- Prefer `suspend fun` over callbacks


**Minimal suspend function example**

```kotlin
suspend fun fetchUser(): User {
    delay(1000)
    return User("Alex")
}
```

Called only from a coroutine or another suspend function.


###### **Jetpack Compose Side Effects**
https://youtu.be/tBLwqpqYQlU?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev

First principle (burn this in)
**Composable functions can re-run anytime.**  
So anything that:
- launches coroutines
- talks to network
- logs
- shows toast
- navigates

→ **must NOT be done directly in the composable body**.

That’s what side-effect APIs are for.

`LaunchedEffect` — auto-run, composition-bound

What it is
- A **composition-managed coroutine**
- Starts **when the composable enters composition**
- Cancels **when composable leaves**
- Restarts **when key changes**

Basic usage
```kotlin
@Composable
fun UserScreen(userId: String) {

    LaunchedEffect(userId) {
        loadUser(userId)
    }

    Text("User Screen")
}
```

Key rule
- `LaunchedEffect(key)`
- If `key` changes → coroutine is cancelled + restarted

**Common patterns**
Run once
```kotlin
LaunchedEffect(Unit) {
    analytics.trackScreen()
}
```


React to state change

```kotlin
LaunchedEffect(isLoggedIn) {
    if (isLoggedIn) {
        navController.navigate("home")
    }
}
```


❌ What you CANNOT do with `LaunchedEffect`

```kotlin
Button(onClick = {
    LaunchedEffect(Unit) {   // ❌ illegal
        doSomething()
    }
}) {}
```

Why?
- `onClick` is **not composable**
- `LaunchedEffect` only works **inside composition**

This is where people get stuck.


###### `rememberCoroutineScope` — event-driven coroutines

What it is
- Gives you a **coroutine scope tied to composable lifecycle**
- You manually launch coroutines
- Perfect for **clicks, gestures, events**

Basic usage
```kotlin
@Composable
fun MyScreen() {
    val scope = rememberCoroutineScope()

    Button(onClick = {
        scope.launch {
            doSomething()
        }
    }) {
        Text("Click")
    }
}
```

Lifecycle behavior
- Composable removed → scope cancelled
- Rotation → old scope cancelled, new one created
- No memory leaks if used correctly


When to use WHAT (no ambiguity)

Use `LaunchedEffect` when:
- Work should start **automatically**
- Tied to **state or composition**
- Example:
    - Initial API call
    - Observe state
    - React to parameter change

Use `rememberCoroutineScope` when:
- Work should start **only on user action**
- Example:
    - Button click
    - Swipe
    - Manual retry

Side-by-side example (important)
❌ Wrong
```kotlin
@Composable
fun Screen() {
    Button(onClick = {
        viewModel.loadData() // launches coroutine internally
    }) {}
}
```

Hidden lifecycle bugs.

Correct (Compose-owned)

```kotlin
@Composable
fun Screen() {
    val scope = rememberCoroutineScope()

    Button(onClick = {
        scope.launch {
            viewModel.loadData()
        }
    }) {}
}
```

Configuration change behavior (what actually happens)
- Rotate screen →
    - composable destroyed
    - coroutine scope cancelled
    - `CancellationException` thrown internally
    - new composition → new scope

You don’t handle this manually. Compose does.

**Mental model (simple + accurate)**
- `LaunchedEffect` = **Compose auto-runs this**
- `rememberCoroutineScope` = **I decide when to run**
- Both:
    - lifecycle-aware
    - auto-cancel
    - safe

One-line rules (save this)
- **Auto side effect → `LaunchedEffect`**
- **User action → `rememberCoroutineScope`**
- **Never launch coroutines directly in composable body**
- **Never block Main thread**


**Minimal real-world example**

```kotlin
@Composable
fun LoginScreen() {
    val scope = rememberCoroutineScope()

    LaunchedEffect(Unit) {
        checkSession()
    }

    Button(onClick = {
        scope.launch {
            login()
        }
    }) {
        Text("Login")
    }
}
```

This is **idiomatic Compose**.

**Final truth**
Compose is **not reactive magic**.  
It’s deterministic _if_ you respect side-effect boundaries.

If you misuse them, bugs won’t crash your app —  
they’ll **silently ruin correctness**, which is worse.

Next sharp edge to learn:
- `rememberUpdatedState`
- `DisposableEffect`
- `SideEffect`

Those solve the _non-obvious_ bugs.


---

###### **`rememberUpdateState`**

rememberUpdateState https://youtu.be/VtMoZE_-HR0?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev

**The problem (before the solution)**

Coroutines **capture values at launch time**.
That means this code is **wrong** in a quiet, sneaky way:

```kotlin
@Composable
fun Timer(onTimeout: () -> Unit) {

    LaunchedEffect(Unit) {
        delay(5_000)
        onTimeout()   // ❌ may be OLD callback
    }
}
```

Why this breaks:
- `LaunchedEffect(Unit)` runs **once**
- `onTimeout` might change later
- coroutine still holds the **old reference**
Welcome to **stale lambda capture**.

What `rememberUpdatedState` actually does
It gives you:
- a **stable reference**
- that always points to the **latest value**
- without restarting the coroutine

Think: _pointer updates, not coroutine restarts_.

Correct fix using `rememberUpdatedState`

```kotlin
@Composable
fun Timer(onTimeout: () -> Unit) {

    val latestOnTimeout = rememberUpdatedState(onTimeout)

    LaunchedEffect(Unit) {
        delay(5_000)
        latestOnTimeout.value()
    }
}
```

Now:
- coroutine runs once
- callback can change
- coroutine always calls the **latest version**

Why NOT just put it in the key?

```kotlin
LaunchedEffect(onTimeout) {
    delay(5_000)
    onTimeout()
}
```

This **restarts the coroutine** every time `onTimeout` changes.

Bad if:
- delay timers
- animations
- long-running work

You didn’t want restart.  
You wanted **updated reference**.


One-sentence definition (memorize)
`rememberUpdatedState` updates **values**, not **effects**.


When you NEED it (common cases)

You need `rememberUpdatedState` when:
- `LaunchedEffect(Unit)` or long-lived coroutine
- Uses:
    - lambdas
    - callbacks
    - navigation
    - ViewModel functions
- Values may change **during composition**

Examples:
- `onClick`
- `onNavigate`
- `onTimeout`
- `onEvent`


Real-world example (navigation bug)

❌ Buggy:

```kotlin
LaunchedEffect(Unit) {
    viewModel.events.collect {
        navController.navigate("home")
    }
}
```

If `navController` changes → crash or wrong behavior.

 
 ✅ Fixed:

```kotlin
val latestNav = rememberUpdatedState(navController)

LaunchedEffect(Unit) {
    viewModel.events.collect {
        latestNav.value.navigate("home")
    }
}
```


Another classic: repeating task

```kotlin
@Composable
fun PollingScreen(onResult: (Int) -> Unit) {

    val latestOnResult = rememberUpdatedState(onResult)

    LaunchedEffect(Unit) {
        while (true) {
            delay(3_000)
            val data = fetch()
            latestOnResult.value(data)
        }
    }
}
```

No restarts. No stale data. No leaks.


What it does NOT do
- ❌ Does NOT launch coroutines
- ❌ Does NOT manage lifecycle
- ❌ Does NOT trigger recomposition
- ✅ ONLY updates a stored value safely

Mental model (clean)
- `remember` → stores once
- `LaunchedEffect(key)` → restarts on key change
- `rememberUpdatedState` → keeps reference fresh **without restart**

One-line rulebook
- Long-running effect + changing lambda → **use it**
- If restarting effect is okay → use key instead
- If restart is harmful → `rememberUpdatedState`

---

`DisposableEffect` https://youtu.be/H8e9p3ilqEo?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev

If `rememberUpdatedState` fixes _stale references_, `DisposableEffect` fixes _leaked side effects_.

**Core idea**
`DisposableEffect` is for **side effects that need explicit cleanup**.

If something has:
- `register` / `unregister`
- `addListener` / `removeListener`
- `start` / `stop`
- `open` / `close`

→ you need `DisposableEffect`.

**Why normal code fails in Compose**

❌ **Wrong**

```kotlin
@Composable
fun LocationTracker() {
    locationManager.requestUpdates() // ❌ leaks on recomposition
}
```

Composable can re-run → you re-register → never unregister → leak.

Compose won’t save you here.


Correct usage: `DisposableEffect`

```kotlin
@Composable
fun LocationTracker() {

    DisposableEffect(Unit) {
        locationManager.requestUpdates()

        onDispose {
            locationManager.removeUpdates()
        }
    }
}
```

Now:
- effect runs when composable enters
- cleanup runs when composable leaves
- zero leaks


Key-based disposal (important)

```kotlin
DisposableEffect(userId) {
    socket.connect(userId)

    onDispose {
        socket.disconnect()
    }
}
```

When `userId` changes:
1. old effect disposed
2. cleanup runs
3. new effect starts

This is **deterministic**, not magic.

**Real-world examples (where you MUST use it)**

1. Listener registration

```kotlin
DisposableEffect(lifecycleOwner) {
    val observer = LifecycleEventObserver { _, event ->
        // handle event
    }

    lifecycleOwner.lifecycle.addObserver(observer)

    onDispose {
        lifecycleOwner.lifecycle.removeObserver(observer)
    }
}
```

2. Broadcast receiver / callback API

```kotlin
DisposableEffect(Unit) {
    registerReceiver(receiver)

    onDispose {
        unregisterReceiver(receiver)
    }
}
```

3. System resources

```kotlin
DisposableEffect(Unit) {
    wakeLock.acquire()

    onDispose {
        wakeLock.release()
    }
}
```

What NOT to use it for
- ❌ Network calls
- ❌ API requests
- ❌ One-shot effects
- ❌ UI state changes

That’s `LaunchedEffect`, not this.


`DisposableEffect` vs `LaunchedEffect`

|Situation|Use|
|---|---|
|Async work|`LaunchedEffect`|
|Needs cleanup|`DisposableEffect`|
|Coroutine|`LaunchedEffect`|
|Listener / resource|`DisposableEffect`|

**The killer combo (advanced but real)**

Sometimes you need **both**:

```kotlin
@Composable
fun SensorScreen(onData: (Int) -> Unit) {

    val latestOnData = rememberUpdatedState(onData)

    DisposableEffect(Unit) {
        val listener = SensorListener { value ->
            latestOnData.value(value)
        }

        sensorManager.registerListener(listener)

        onDispose {
            sensorManager.unregisterListener(listener)
        }
    }
}
```

- `DisposableEffect` → manage lifecycle
- `rememberUpdatedState` → avoid stale lambda

This is **production-grade Compose**.

Common beginner mistakes
- Forgetting `onDispose`
- Using `LaunchedEffect` for listeners
- Putting cleanup logic outside `onDispose`
- Using `DisposableEffect` just to “run code”

If no cleanup is needed → don’t use it.

One-line mental model
- `LaunchedEffect` → **do work**
- `DisposableEffect` → **bind + unbind**
- `rememberUpdatedState` → **keep references fresh**


---
`produceState & derivedState` https://youtu.be/a5BzCvVcDnE?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev

Jetpack Compose has **two different problems** to solve:

1. **Getting data from the outside world**  
    (timers, Flow, network, sensors, DB, animations)
    
2. **Computing values from existing state efficiently**

`produceState` solves **#1**  
`derivedStateOf` solves **#2**
They do **different jobs**. Mixing them is a beginner mistake.


###### `produceState` — “Bring external async data into Compose”

What problem it solves
Compose UI reacts only to **Compose State**.  
But real apps depend on:
- timers
- Flow
- LiveData
- callbacks
- suspend functions

`produceState` is a **bridge**.

> External async source → Compose `State<T>`


Without `produceState` (old way)

```kotlin
val data by remember { mutableStateOf(0) }

LaunchedEffect(Unit) {
    while (true) {
        delay(1000)
        data++
    }
}
```

This is valid, but:
- state creation
- side effect are split


With `produceState` (cleaner)

```kotlin
val data by produceState(initialValue = 0) {
    while (true) {
        delay(1000)
        value++
    }
}
```

**What happened**
- `produceState` created state
- launched a coroutine
- exposed `value` to update state
- handled cancellation automatically

Less code. Same behavior.


Key rule (burn this in)

> **Inside `produceState`, you NEVER mutate UI directly.  
> You only assign to `value`.**


Realistic example: timer counter

```kotlin
@Composable
fun TimerText() {
    val seconds by produceState(initialValue = 0) {
        while (true) {
            delay(1000)
            value++
        }
    }

    Text("Seconds: $seconds")
}
```

- Coroutine runs
- `value` updates
- recomposition happens
- UI stays pure

When to use `produceState`
Use it when:
- data comes from **outside Compose**
- updates asynchronously
- lifecycle must auto-cancel

Examples:
- Flow → UI
- LiveData → UI
- countdown timer
- animation loop
- sensor values

###### `derivedStateOf` — “Compute state efficiently”

Now a **different problem**.

The problem
Compose recomposes **a lot**.  
If you compute values inside composables naively, they may recompute unnecessarily.

`derivedStateOf` says:
> “Only recompute this when its inputs change.”

Without `derivedStateOf` (inefficient)

```kotlin
val total = items.sumOf { it.price }
```

This runs **every recomposition**, even if `items` didn’t change.


With `derivedStateOf`

```kotlin
val total by remember {
    derivedStateOf {
        items.sumOf { it.price }
    }
}
```

Now:
- recomputed **only when `items` changes**
- skipped otherwise

This is **memoization**, not async.

 Important distinction
`derivedStateOf`:
- ❌ does NOT launch coroutines
- ❌ does NOT handle async work
- ✅ only derives values from existing state


Clean example: derived UI text

```kotlin
var count by remember { mutableStateOf(1) }

val message by remember {
    derivedStateOf {
        "5 x $count = ${5 * count}"
    }
}
```
- `count` changes → message recalculates
- unrelated recompositions → message stays cached

**Using both together (correctly)**
This is where your YT notes were heading.

```kotlin
@Composable
fun TableExample() {
    val index by produceState(initialValue = 1) {
        while (true) {
            delay(1000)
            value++
        }
    }

    val message by remember {
        derivedStateOf {
            "5 x $index = ${5 * index}"
        }
    }

    Text(message)
}
```

**Flow of truth**
```
produceState → index updates (async)
derivedStateOf → message recalculates (pure)
UI → recompose
```

Each tool does **one job**.

**Mental model (very important)**

Think like this:
- `produceState` = **source**
- `derivedStateOf` = **calculation**
- Composables = **render**

Never blur these layers.

**Brutal mistakes to avoid**
❌ Using `produceState` to compute simple values  
❌ Using `derivedStateOf` for async work  
❌ Putting heavy logic directly in composables  
❌ Forgetting `remember` with `derivedStateOf`

Compose won’t stop you.  
Your performance will silently degrade.

One-line summaries
- **`produceState`**  
    → _“Turn async/external data into Compose state.”_
- **`derivedStateOf`**  
    → _“Compute a value from state, but only when needed.”_

Once these click, you’re no longer a beginner in Compose — you’re thinking in **reactive systems**, not UI tricks.


---

ex02 app: https://youtu.be/t3ZonTbwzAs?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev


**Hilt** and **Dagger** are **dependency injection (DI)** frameworks used in Android to manage how objects are created and provided to other objects.

First, the core idea.

In any non-toy Android app, classes depend on other classes.  
A `ViewModel` needs a `Repository`.  
A `Repository` needs a `Database` or `ApiService`.  
If you manually create these with `new`, you get tight coupling, duplicated setup, and a mess during testing.

Dependency Injection solves this by saying:  
“Don’t build your dependencies yourself. Ask for them.”

**Dagger (the base framework)**
**Dagger** is a **general-purpose DI framework for Java/Kotlin**, not Android-specific.

What it does:
- Generates code at **compile time**
- Builds an object graph
- Knows how to create and reuse objects

What it’s like to use:
- Very powerful
- Very verbose
- Easy to shoot yourself in the foot

Typical Dagger problems:
- Lots of boilerplate
- Complex setup
- Android lifecycle integration is painful
- Error messages feel like they were written by an alien compiler god

Dagger is the engine. Raw. Unforgiving.



**Hilt (Android-friendly wrapper over Dagger)**
**Hilt** is **Google’s opinionated layer on top of Dagger**, made specifically for Android.

Think of it as:

> Dagger + Android defaults + less pain

What Hilt does:
- Uses Dagger under the hood
- Auto-generates most of the boilerplate
- Integrates with Android components:
    - Application
    - Activity
    - Fragment
    - ViewModel
    - Service
    - Worker

Instead of manually wiring everything, Hilt gives you:
- Predefined component scopes
- Sensible lifecycle handling
- Shorter annotations
- Fewer places to break things



**ViewModel** exists to solve one boring but brutal Android problem: **UI components die all the time**.

Activities and Fragments are fragile. Rotate the screen, switch apps, low memory—boom, they’re recreated. If your data lived there, it would evaporate. ViewModel is the **survivor layer**.

What a ViewModel actually is

A ViewModel is a class that:
- **Holds UI-related data**
- **Survives configuration changes** (like rotation)
- **Does NOT know about Views** (no Context, no Activity references)

Think of it as a **brain** that outlives the body.

UI = dumb  
ViewModel = logic + state

Why we use ViewModel
1. **State survives rotation**  
    Without ViewModel, screen rotation resets everything.  
    With ViewModel, data stays.
    
2. **Separation of concerns**  
    UI renders data.  
    ViewModel decides _what_ data.  
    Cleaner, testable, non-chaotic code.
    
3. **Lifecycle-aware**  
    ViewModel is destroyed only when the screen is truly gone (Activity finished).  
    Not on every tiny lifecycle hiccup.
    
4. **Works naturally with LiveData / StateFlow**  
    UI observes.  
    ViewModel emits.  
    No memory leaks, no manual lifecycle juggling.



Android side (exact mapping)
In Android:
- **Retrofit** → does the HTTP request (like `fetch`)
- **Coroutine** → async container (like Promise)
- **`suspend`** → async/await syntax



Web dev routing (what you already know)
In React / web apps:
- **Route** = URL → Component
- Browser manages history
- You can deep-link by default
- Refresh = reload everything

Android Navigation Compose
In Android:
- **Destination** = route string → Composable
- **NavController** manages back stack
- No browser, no reload, no free history
- Deep links are explicit, not automatic

TODO: https://youtu.be/uUBcyvw3uDE?list=PLRKyZvuMYSIO9sadcCwR0DR8UPi9bQlev


---

###### **viewModel**
android developer: https://youtu.be/5qlIPTDE274
cheezycode: https://youtu.be/OZBwLFV-OvI (old XML)
PL: https://youtu.be/9sqvBydNJSg
compose state or stateflow in viewModel: https://youtu.be/T8vApYJlW8o
AK: https://youtu.be/57LBdPAnuLk?list=PLQ_Ai1O7sMV33aJHfqR-vquGZE1OCOS51

First: what a ViewModel REALLY is (not the textbook version)

A **ViewModel is a long-living brain** for a screen.
- The **UI (Compose)** is dumb and disposable
- The **ViewModel** holds truth: data + logic
- Android may kill and recreate the UI at will
- The ViewModel survives and says:  
    “Relax, I still remember everything.”


Why normal variables fail (the pain)

Imagine this **Compose screen without ViewModel**:
```kotlin
@Composable
fun CounterScreen() {
    var count by remember { mutableStateOf(0) }

    Button(onClick = { count++ }) {
        Text("Count: $count")
    }
}
```

Rotate screen → 💥 **count resets**  
Process killed → 💥 **count gone**

`remember` is **NOT persistence**.  
It only survives recomposition, not destruction.


Enter ViewModel (the fix)

Step 1: Create a ViewModel
```kotlin
class CounterViewModel : ViewModel() {

    var count by mutableStateOf(0)
        private set

    fun increment() {
        count++
    }
}
```
Key things happening:
- `ViewModel()` = lifecycle-aware
- State lives **outside UI**
- UI cannot mutate state directly (`private set`)

Step 2: Use ViewModel in Compose
```kotlin
@Composable
fun CounterScreen(
    viewModel: CounterViewModel = viewModel()
) {
    val count = viewModel.count

    Button(onClick = { viewModel.increment() }) {
        Text("Count: $count")
    }
}
```

Now rotate the phone.

Nothing resets.  
Android recreates UI → ViewModel survives → state restored.

Important rule (no compromise)

> **ViewModel must NEVER know about UI**

❌ NO:
- `Context`
- `TextView`
- `Composable`
- `NavController`

✅ YES:
- State
- Business logic
- Network calls
- Repositories

Why?  
Because ViewModel outlives UI.  
Holding UI references = memory leaks + crashes.


**Where ViewModel actually shines (real apps)**

Example: Fake network call
```kotlin
class UserViewModel : ViewModel() {

    var userName by mutableStateOf("Loading...")
        private set

    init {
        loadUser()
    }

    private fun loadUser() {
        viewModelScope.launch {
            delay(2000) // pretend network
            userName = "Droid85"
        }
    }
}
```

Now UI:
```kotlin
@Composable
fun UserScreen(
    vm: UserViewModel = viewModel()
) {
    Text(text = vm.userName)
}
```

Rotate screen:
- ❌ No refetch
- ❌ No loading reset
- ✅ User instantly visible

That’s **why ViewModel exists**.


**ViewModel + Coroutine (critical combo)**

ViewModel has a built-in scope:

```kotlin
viewModelScope.launch {
    // safe coroutine
}
```

When screen is **finally destroyed**, Android:
- cancels all coroutines
- calls `onCleared()`

No leaks. No zombie jobs.


**How ViewModel fits with things you already learned**

|Concept|Role|
|---|---|
|`produceState`|Converts async → UI state|
|`derivedStateOf`|Computes from state|
|**ViewModel**|Owns state + logic|
|Compose|Renders state|

Correct architecture:

```
ViewModel (truth)
↓
Compose observes state
↓
User events
↓
ViewModel updates state
```

Unidirectional. Predictable. Debuggable.


**Brutal truths beginners need to hear**
- ViewModel is **not optional** in real apps
- Screens without ViewModel don’t scale
- `remember` is temporary, ViewModel is real
- If logic lives in Composables, you will suffer later


Final mental model (lock this in)
- **Compose** = body (can be destroyed)
- **ViewModel** = brain (persists)
- **State** = memory
- **Coroutine** = nervous system

Once you build with this separation, Android stops feeling hostile and starts behaving like a controlled system instead of chaos.

Next logical step after this:  
**ViewModel + Repository + Retrofit + Flow** — that’s where “toy apps” become real products.


also
- **ViewModel**
    - owns `LiveData` / `StateFlow`
- **Composable**
    - uses `mutableStateOf` (or collects StateFlow)
- **UI**
    - observes, never mutates business state


---

###### Dependency Injection
DI by PL: https://youtu.be/_qb87PN7jlI


---

android basics by philipp lackner: https://youtube.com/playlist?list=PLQkwcJG4YTCSVDhww92llY3CAnc_vUhsm&si=62TwOgP6TgtsaUAI

**What Context _really_ is (no mysticism)**
PL: https://youtu.be/YdnM2ZvrIFM?list=PLQkwcJG4YTCSVDhww92llY3CAnc_vUhsm

Context is **your app’s identity card inside Android**.

A plain Kotlin class is homeless.  
Give it a `Context`, and suddenly it can:
- read `R.string`
- open databases
- talk to system services
- launch activities

```kotlin
fun saveFile(context: Context) {
    context.openFileOutput("data.txt", Context.MODE_PRIVATE)
        .use { it.write("hello".toByteArray()) }
}
```
No `Context` → no Android world access. Simple.


**Two Contexts, two lifetimes (this matters)**

Activity Context
- Tied to **UI**
    
- Dies on rotation / back press
    
- Required for UI-bound things
    

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        val activityContext: Context = this
    }
}
```

###### **Application Context**
- Lives as long as the app process
- No UI connection
- Safe for long-lived objects

```kotlin
val appContext = applicationContext
```

**Rule you tattoo on your brain:**

> Short-lived object → can use long-lived context  
> Long-lived object → must NOT use short-lived context


**Jetpack Compose: where context comes from**

Compose is UI, but **not an Activity**.  
You explicitly ask for context.

```kotlin
@Composable
fun MyScreen() {
    val context = LocalContext.current

    Button(onClick = {
        Toast.makeText(context, "Hello", Toast.LENGTH_SHORT).show()
    }) {
        Text("Click")
    }
}
```

`LocalContext.current` is usually the **Activity context** when the Composable is on screen.


**ViewModel + Context: the classic foot-gun 🔫**

❌ Wrong (memory leak)
```kotlin
class MyViewModel : ViewModel() {
    lateinit var context: Context
}
```

```kotlin
viewModel.context = this // Activity reference leaks on rotation
```

Why this explodes:
- Activity is destroyed
- ViewModel survives
- GC can’t clean Activity
- RAM leak, subtle bugs, pain


**Correct patterns (real-world, used in production)**

**✅ Pattern 1: Don’t pass Context at all**

Move Android-specific work **outside** ViewModel.
```kotlin
class MyViewModel : ViewModel() {
    fun onButtonClick() {
        // emit event, no Android dependency
    }
}
```

```kotlin
@Composable
fun Screen(viewModel: MyViewModel = viewModel()) {
    val context = LocalContext.current

    Button(onClick = {
        viewModel.onButtonClick()
        Toast.makeText(context, "Clicked", Toast.LENGTH_SHORT).show()
    }) {}
}
```

Clean. Testable. Correct.


✅ Pattern 2: Application Context (only if unavoidable)

Use **AndroidViewModel**, not ViewModel.
```kotlin
class MyViewModel(
    application: Application
) : AndroidViewModel(application) {

    fun readPrefs(): String {
        val prefs = getApplication<Application>()
            .getSharedPreferences("prefs", Context.MODE_PRIVATE)

        return prefs.getString("key", "") ?: ""
    }
}
```
Still not ideal, but **safe**.


**When Activity Context is mandatory**

Some APIs _need_ a UI anchor.

Permissions (Compose + Activity)
```kotlin
val activity = LocalContext.current as Activity

ActivityCompat.requestPermissions(
    activity,
    arrayOf(Manifest.permission.CAMERA),
    100
)
```
Application context **cannot** do this.  
No UI = no permission dialog.


**Services, repositories, singletons: what context to use**

Repository / Database / DataStore
```kotlin
class UserRepository(context: Context) {
    private val db = Room.databaseBuilder(
        context.applicationContext,
        AppDatabase::class.java,
        "db"
    ).build()
}
```
Always force `applicationContext`.


**Brutal summary (no fluff)**
- Context = Android access key
- Activity Context = UI-bound, fragile
- Application Context = long-lived, safe
- ViewModel must **never** hold Activity context
- Compose uses `LocalContext.current`
- If you _need_ context in VM → rethink architecture first

Next natural continuation is **how Hilt/Dagger injects context safely**, because that’s where most devs mess this up without realizing it.


---
###### **Resources & Qualifiers**
PL: https://youtu.be/vj1ZdUfPlJM?list=PLQkwcJG4YTCSVDhww92llY3CAnc_vUhsm


Resources are **data the OS manages for you**, not just files.

Why they exist:
- automatic localization
- automatic dark mode
- automatic screen-size handling
- automatic API-level compatibility

If you hardcode values in Kotlin, **you opt out of all that**.


**The R class (why it exists and why it breaks builds)**

Every resource becomes an ID in `R`.
```kotlin
R.string.app_name
R.drawable.logo
R.color.primary
```
These are **integers**, not files.
Common beginner bug:
- importing the wrong `R` (from a library)

Correct import:
```kotlin
import com.yourpackage.name.R
```
If autocomplete shows multiple `R` classes, slow down. This causes silent wrong behavior.


**Accessing resources (classic vs Compose)**

Activity / Fragment
```kotlin
val title = getString(R.string.app_name)
val color = getColor(R.color.purple_200)
```

Non-Android class
```kotlin
class Repo(private val context: Context) {
    fun read(): String {
        return context.resources.getString(R.string.app_name)
    }
}
```

Always prefer:
```kotlin
context.applicationContext
```
for long-lived objects.


**Jetpack Compose: the modern way**

Compose hides most boilerplate.

Strings
```kotlin
Text(text = stringResource(R.string.app_name))
```

Colors
```kotlin
val color = colorResource(R.color.purple_200)
Box(modifier = Modifier.background(color))
```

Images
```kotlin
Image(
    painter = painterResource(R.drawable.kermit),
    contentDescription = null
)
```

Compose automatically reacts to:
- dark mode
- locale change
- configuration change

No `if (isDarkMode)` garbage.


**Resource folders that actually matter**

You’ll use these 90% of the time:
- `drawable/` → images, vectors
- `mipmap/` → **ONLY app icons**
- `values/strings.xml` → text
- `values/colors.xml` → color constants
- `values/dimens.xml` → spacing, font sizes

Example `dimens.xml`:
```xml
<dimen name="padding_small">8dp</dimen>
```

Compose:
```kotlin
val padding = dimensionResource(R.dimen.padding_small)
```


**Qualifiers = zero-logic superpower**

Qualifiers let Android **switch resources without code**.

Dark mode
```
values/colors.xml
values-night/colors.xml
```

Same name, different value:
```xml
<!-- values/colors.xml -->
<color name="bg">#FFFFFF</color>

<!-- values-night/colors.xml -->
<color name="bg">#000000</color>
```

Compose:
```kotlin
Box(modifier = Modifier.background(colorResource(R.color.bg)))
```
No checks. No flags. OS handles it.


Localization (done right)
```
values/strings.xml
values-de/strings.xml
values-hi/strings.xml
```

```xml
<string name="welcome">Welcome</string>
```

Compose:
```kotlin
Text(stringResource(R.string.welcome))
```
Change system language → UI updates automatically.

Hardcoded strings break accessibility and localization. Period.


**Screen size qualifiers (phones vs tablets)**
```
layout/
layout-sw600dp/
```

Or for Compose-heavy apps:
- still useful for **images, dimensions, fonts**

Example:
```
values/dimens.xml
values-sw600dp/dimens.xml
```
Tablet spacing without code changes.


**API-level qualifiers (clean backward compatibility)**
```
drawable-v24/
```
Used when newer APIs support better assets.

Android picks the **best match**, falling back safely.


Brutally honest rules (remember these)
- Resources = OS-managed state
- Hardcoding = opting out of Android features
- Qualifiers replace conditionals
- Compose + resources = reactive UI for free
- `mipmap` is ONLY for launcher icons
- Wrong `R` import = silent pain

Next logical topic after this is **themes vs MaterialTheme vs resources in Compose**, because that’s where people start mixing systems and get confused fast.


---

###### Intents and intent filters
PL: https://youtu.be/2hIY1xuImuQ?list=PLQkwcJG4YTCSVDhww92llY3CAnc_vUhsm


An Intent is just a **structured message**:
- who is sending
- what they want done (`action`)
- what data is involved (`data + type`)
- optional parameters (`extras`)

Android is basically a **message router**. Intents are the packets.


**Explicit intents: deterministic, boring, correct**

Internal navigation

Use this when **you control the target**.
```kotlin
val intent = Intent(this, SecondActivity::class.java)
startActivity(intent)
```
No chooser. No guessing. Fast.


**External explicit intent (package-based)**

Use only when you **require a specific app**.
```kotlin
val intent = packageManager.getLaunchIntentForPackage(
    "com.google.android.youtube"
)

if (intent != null) {
    startActivity(intent)
} else {
    // app not installed → fallback
}
```
Never assume the app exists. Android will crash you for arrogance.


**Implicit intents: “someone, anyone, do this”**

You describe **what**, not **who**.

Share text
```kotlin
val intent = Intent(Intent.ACTION_SEND).apply {
    type = "text/plain"
    putExtra(Intent.EXTRA_TEXT, "Hello Android")
}

startActivity(Intent.createChooser(intent, "Share via"))
```

System:
- scans apps
- filters by action + MIME type
- shows chooser

You didn’t write logic. Android did.


**MIME types matter more than you think**

Wrong type = app won’t appear.
Examples:
- `"text/plain"`
- `"image/*"`
- `"application/pdf"`

Sharing an image?
```kotlin
Intent(Intent.ACTION_SEND).apply {
    type = "image/*"
    putExtra(Intent.EXTRA_STREAM, imageUri)
}
```


**Receiving data (modern, non-deprecated)**

In Activity
```kotlin
val imageUri = if (Build.VERSION.SDK_INT >= 33) {
    intent.getParcelableExtra(Intent.EXTRA_STREAM, Uri::class.java)
} else {
    @Suppress("DEPRECATION")
    intent.getParcelableExtra(Intent.EXTRA_STREAM)
}
```
Yes, it’s annoying. Welcome to Android API evolution.


**Intent filters: how your app becomes “visible”**

This goes in **AndroidManifest.xml**.

Example: receive shared images
```xml
<activity
    android:name=".MainActivity"
    android:launchMode="singleTop">

    <intent-filter>
        <action android:name="android.intent.action.SEND" />
        <category android:name="android.intent.category.DEFAULT" />
        <data android:mimeType="image/*" />
    </intent-filter>

</activity>
```
Now your app appears in:
- Chrome share sheet
- Gallery share sheet
- Any image-sharing flow


Why `singleTop` actually matters
Without it:
- every share creates a **new Activity**
- UI state resets
- user gets confused

With `singleTop`:
```kotlin
override fun onNewIntent(intent: Intent?) {
    super.onNewIntent(intent)
    // handle new data here
}
```
Only one Activity instance lives.


**Correct Compose + ViewModel pattern**
Activity:
```kotlin
override fun onNewIntent(intent: Intent?) {
    super.onNewIntent(intent)
    viewModel.onNewImage(intent)
}
```

ViewModel:
```kotlin
class MainViewModel : ViewModel() {
    var imageUri by mutableStateOf<Uri?>(null)
        private set

    fun onNewImage(intent: Intent?) {
        imageUri = intent?.getParcelableExtra(Intent.EXTRA_STREAM)
    }
}
```

Compose UI:
```kotlin
@Composable
fun Screen(vm: MainViewModel) {
    vm.imageUri?.let {
        AsyncImage(model = it, contentDescription = null)
    }
}
```
This is **proper state flow**. No hacks.


**Queries (why Android suddenly says “no”)**

Modern Android blocks app scanning.

If you do:
```kotlin
intent.resolveActivity(packageManager)
```

You MUST declare intent visibility:
```xml
<queries>
    <intent>
        <action android:name="android.intent.action.SEND" />
        <data android:mimeType="image/*" />
    </intent>
</queries>
```
Otherwise Android pretends apps don’t exist.

This is privacy, not a bug.


**Brutally honest rules**
- Explicit intent → control
- Implicit intent → delegation
- MIME type decides visibility
- Manifest defines what your app **can receive**
- `singleTop + ViewModel` = sane share handling
- Forgetting `<queries>` = silent failure

After intents, the next natural topic is **navigation (NavController vs intents)**, because that’s where people misuse intents internally and create spaghetti.


---

**Broadcasts & Broadcast Receivers**
https://youtu.be/HDVyFsFUuVg?list=PLQkwcJG4YTCSVDhww92llY3CAnc_vUhsm

A broadcast is:
- an **Intent**
- sent to **many potential receivers**
- delivered **by the system**, not directly by you

Think: _radio signal_, not phone call.

Intent → point-to-point  
Broadcast → one-to-many

---

## 2. BroadcastReceiver: the listener

A `BroadcastReceiver` is a tiny, short-lived component.

- No UI
    
- No long work
    
- React → delegate → exit
    

```kotlin
class AirplaneModeReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        if (intent.action == Intent.ACTION_AIRPLANE_MODE_CHANGED) {
            val enabled = Settings.Global.getInt(
                context.contentResolver,
                Settings.Global.AIRPLANE_MODE_ON,
                0
            ) != 0
        }
    }
}
```

`onReceive()` must finish fast. Android will kill you if you abuse it.

---

## 3. Dynamic receivers (modern + safe)

### When to use

- UI is visible
    
- you only care **while the screen is alive**
    

### Register / unregister

```kotlin
private val receiver = AirplaneModeReceiver()

override fun onStart() {
    super.onStart()
    registerReceiver(
        receiver,
        IntentFilter(Intent.ACTION_AIRPLANE_MODE_CHANGED)
    )
}

override fun onStop() {
    super.onStop()
    unregisterReceiver(receiver)
}
```

Why `onStart/onStop` and not `onCreate/onDestroy`?

- avoids leaks
    
- respects visibility
    
- matches lifecycle reality
    

---

## 4. Static receivers (rare, restricted, dangerous)

Declared in **AndroidManifest.xml**.

```xml
<receiver
    android:name=".BootReceiver"
    android:exported="false">
    <intent-filter>
        <action android:name="android.intent.action.BOOT_COMPLETED" />
    </intent-filter>
</receiver>
```

### Reality check

- Most system broadcasts **no longer work** statically
    
- Google killed them for battery reasons
    
- `BOOT_COMPLETED` is a special exception
    

If someone tells you “just use a static receiver” — they’re outdated.

---

## 5. What receivers should actually do

Never do work directly.

Correct pattern:

```kotlin
override fun onReceive(context: Context, intent: Intent) {
    val work = OneTimeWorkRequestBuilder<SyncWorker>().build()
    WorkManager.getInstance(context).enqueue(work)
}
```

Broadcast → **trigger**  
Worker / Service → **work**

---

## 6. Custom broadcasts (app ↔ app communication)

### Sender

```kotlin
val intent = Intent("com.example.TEST_ACTION").apply {
    putExtra("data", "Hello")
}
sendBroadcast(intent)
```

### Receiver

```kotlin
if (intent.action == "com.example.TEST_ACTION") {
    val data = intent.getStringExtra("data")
}
```

Always namespace your action string.  
Generic strings are collisions waiting to happen.

---

## 7. Targeted broadcasts (security)

Broadcasts can be **too open**.

Safer:

```kotlin
intent.setPackage("com.example.targetapp")
sendBroadcast(intent)
```

This:

- avoids leaks
    
- avoids malicious listeners
    
- can wake static receivers in closed apps
    

---

## 8. Compose + ViewModel pattern (correct)

Receiver → ViewModel → UI

```kotlin
class NetworkReceiver(
    private val vm: MainViewModel
) : BroadcastReceiver() {

    override fun onReceive(context: Context, intent: Intent) {
        vm.onNetworkChanged()
    }
}
```

UI reacts via state, not callbacks.

---

## 9. Brutally honest rules

- Broadcasts are **signals**, not workers
    
- Dynamic receivers > static receivers
    
- Static receivers are mostly dead
    
- Never block `onReceive`
    
- Delegate immediately (Worker / ViewModel)
    
- Overusing broadcasts = battery abuse
    


Mental model to keep

**Intent** → ask someone to do something  
**Broadcast** → announce that something happened

Once you see broadcasts as announcements, not commands, Android suddenly behaves predictably.

Next natural step after this: **Services vs WorkManager**, because broadcasts almost always _trigger_ background work rather than perform it.


TODO: broadcast, foreground services , workmanager , uris, content providers https://youtu.be/HDVyFsFUuVg?list=PLQkwcJG4YTCSVDhww92llY3CAnc_vUhsm




---
###### exampleApp01
shivam sharma: https://youtu.be/U5dE-_E1wsg jetpack compose UI and other

composable function https://youtu.be/U5dE-_E1wsg?t=3796
accessing resources: https://youtu.be/U5dE-_E1wsg?t=4722
core components: https://youtu.be/U5dE-_E1wsg?t=6290
pending....

---

###### `Scaffold` — the skeleton

`Scaffold` is just a layout coordinator.  
It does **not** do navigation. It only reserves slots.

Think of it as a ribcage:
- `topBar`
- `bottomBar`
- `content`

```kotlin
Scaffold(
    bottomBar = { BottomBar() }
) { padding ->
    // NavHost goes here
}
```

What you must understand:
- `Scaffold` passes **padding** → you must apply it to `NavHost`
- `Scaffold` doesn’t remember state for you
- `Scaffold` is replaceable — don’t worship it

If you misuse padding → overlapping UI bugs. Classic beginner trap.


###### `BottomNavigation` / `NavigationBar` — just UI

In **Material 3**, you should use:

```kotlin
NavigationBar
NavigationBarItem
```

Not logic. Not navigation.  
Just buttons with icons.

```kotlin
NavigationBar {
    items.forEach { screen ->
        NavigationBarItem(
            selected = isSelected,
            onClick = { /* navigate */ },
            icon = { Icon(...) },
            label = { Text(screen.label) }
        )
    }
}
```
Key realization: Bottom bar does NOT control navigation. It only **requests** navigation.


**`NavController` — the brain**

This is the actual navigation engine.
```kotlin
val navController = rememberNavController()
```
Responsibilities:
- Back stack
- Current destination
- Navigation actions
- State restoration

**`NavHost` — the map**

`NavHost` defines **where you can go**.

```kotlin
NavHost(
    navController = navController,
    startDestination = "home"
) {
    composable("home") { HomeScreen() }
    composable("cart") { CartScreen() }
    composable("profile") { ProfileScreen() }
}
```

Think of it as a graph, not a switch statement.


**Route design**
Don’t hardcode strings everywhere.

Do this:
```kotlin
sealed class Screen(val route: String) {
    object Home : Screen("home")
    object Cart : Screen("cart")
    object Profile : Screen("profile")
}
```
Why?
- Compile-time safety
- Centralized routes
- Refactor-friendly


**Correct bottom navigation behavior (VERY important)**
Bottom navigation is **not** normal navigation.

Rules:
- Each tab has its own back stack
- Reselecting a tab should NOT recreate screen
- Back button should exit app from root tab

You must use this pattern:
```kotlin
navController.navigate(screen.route) {
    popUpTo(navController.graph.findStartDestination().id) {
        saveState = true
    }
    launchSingleTop = true
    restoreState = true
}
```


**Observing current route (to highlight selected tab)**

```kotlin
val navBackStackEntry by navController.currentBackStackEntryAsState()
val currentRoute = navBackStackEntry?.destination?.route
```

Then:
```kotlin
selected = currentRoute == screen.route
```

No hacks. No mutable state.


**What ELSE you must learn (non-negotiable)**
If you skip these, your navigation will rot:

**State hoisting**: Screens must not own navigation state.

**Single-activity architecture**: One `Activity`, everything else is composables.

**Navigation arguments**
```kotlin
composable("product/{id}") { backStack ->
    val id = backStack.arguments?.getString("id")
}
```

**ViewModel + Navigation**
- ViewModel survives config changes
- NavController does NOT belong in ViewModel

**Process death & restore**
Bottom navigation without `saveState` = broken app after OS kill.

Mental model (memorize this)
- `Scaffold` → layout
- `NavigationBar` → UI buttons
- `NavController` → state machine
- `NavHost` → graph
- Routes → contracts
- Back stack → reality

Learning order (strict)
1. NavController + back stack
2. NavHost + routes
3. Scaffold padding rules
4. NavigationBar UI
5. Correct bottom-nav navigation options
6. State restoration
7. Nested navigation graphs (advanced, but coming)

Once this clicks, you’ll stop fighting Compose and start _using_ it.

Next natural escalation: **nested graphs per tab** (home stack, cart stack, profile stack) — that’s where real apps live.


---

###### Navigation app example
https://developer.android.com/develop/ui/compose/navigation
https://developer.android.com/guide/navigation

navigaiton with nav arguments 
- easyTuto: https://youtu.be/wJKwsI5WUI4
- cheezyCode: https://www.youtube.com/watch?v=VU3SVwxmlz0&pp=ygUaamV0cGFjayBjb21wb3NlIG5hdmlnYXRpb24%3D
typesafe navigation by PL: https://www.youtube.com/watch?v=AIC_OFQ1r3k&pp=ygUaamV0cGFjayBjb21wb3NlIG5hdmlnYXRpb24%3D
bottom navigation bar by PL: https://youtu.be/c8XP_Ee7iqY

Phase 1 
- Official Navigation-Compose
- Sealed class routes
- Manual nav arguments
- Bottom navigation with state restore
Phase 2 (after 1–2 real screens)
- Add product detail with arguments
- Handle back button correctly
- Survive rotation & process death
Phase 3 (only then)
- Migrate to type-safe navigation **if you feel pain**
- Not because YouTube said so

Checkout whole code: https://github.com/droid85real/ecomm-android-app/commit/ca7bec427fd80aeb6cda44652445b6757a5f2df5?diff=split#diff-4a86c8131ef4dc67a12171df11b1c7f02e6cbaeaf267151d479851856a5971ef

---

###### Bottom navigation bar example app
easy tuto: https://youtu.be/O9csfKW3dZ4
PL: https://youtu.be/c8XP_Ee7iqY

**Step1: Upgrade screen sealed class with icon, label , flags**
Why sealed class?
Because:
- Routes are **finite**
- Compiler knows all possible screens
- No typo bugs like `"hme"` vs `"home"`

**Step2: BottomBar — what it is and what it does**

Material’s **BottomNavigation implementation**.  
It:
- Shows items horizontally
- Highlights selected tab
- Handles accessibility + animations

What does our BottomBar do?
1. Reads **current route**
2. Marks correct item as selected
3. Navigates when user taps

Why `currentBackStackEntryAsState()`?
Because Compose is **reactive**.
- When route changes → recomposition happens
- Bottom bar automatically updates selection
- No manual state tracking needed

Why `popUpTo(Screen.Home.route)`?
Without it:
- Home → Auth → Home → Auth → Home…
- Back stack becomes trash
- Back button behaves randomly

With it:
- Stack stays shallow
- Bottom nav behaves like **tab switching**, not drilling down

Why `launchSingleTop = true`?
If user taps the same tab again:
- You don’t want a new instance
- You want the existing one reused

This prevents:
- State loss
- Duplicate recompositions
- Back stack spam


**Step3: Scaffold — the glue**

What is Scaffold?
Think of it as a **screen skeleton**. It prevents overlap and handles padding.
- topBar
- bottomBar
- floatingActionButton
- content area

Without Scaffold:
- Bottom bar would sit _on top_ of screens
- Touches would break
- Layout would get messy

- `Scaffold` renders the bottom bar
- `paddingValues` ensures screens don’t hide behind it
- `NavHost` lives inside content area
- Bottom bar never gets recreated unnecessarily


checkout whole code: https://github.com/droid85real/ecomm-android-app/commit/4b1b2849e453435908989e1ea6f50499ad3e25c1

---

###### Sharing data between screens in jetpack compose
philipp lackner: https://youtu.be/h61Wqy3qcKg


---

###### Package structure in android
PL: https://youtu.be/ek682t-z2gQ

Modular structure approach


---


In React/JS, the mental stack is:  
**HTTP → async → promises → fetch/axios → state update**

In Android/Kotlin, it becomes:  
**HTTP → async → coroutines → Retrofit/OkHttp → state update**

---

###### Retrofit
https://medium.com/@KaushalVasava/retrofit-in-android-5a28c8e988ce
android knowledge: https://youtu.be/SvadOJrNdio
android knowledge hindi: https://youtu.be/U4vTRrLDICo
coroutine with retrofit by cheezycode: https://www.youtube.com/watch?v=135FpDGJeEQ
MVVM with retrofit : https://youtu.be/D29vhvGv9Cc
https://youtu.be/HzbTCLnPR24?list=PLEGrY4uRTu5mn5Hky0xTZS3gK4TbYM_CR
https://youtu.be/F5sj_PFzzx0
coroutine with retrofit by PL: https://www.youtube.com/watch?v=S-10lLA0nbk
https://www.youtube.com/watch?v=lT3-NBWV9HU

TODO: https://youtu.be/D29vhvGv9Cc?t=531


###### Why should I use kotlinx.serialization?
(what is):https://youtu.be/-_scGU1nkPg
(how to):https://youtu.be/698I_AH8h6s
(what is):https://youtu.be/Uxun8uUSibE
(custom)PL: https://youtu.be/_KQBp5pwUO0

docs: https://kotlinlang.org/docs/serialization.html#add-plugins-and-dependencies
https://github.com/Kotlin/kotlinx.serialization


Serialization = converting an object  
→ into **bytes / JSON / Bundle-safe form**  
→ so it can be **stored or transmitted**

**how to add** 
Step 1: Add serialization plugin to `libs.versions.toml`

Under `[plugins]`, add this:
```toml
kotlin-serialization = { id = "org.jetbrains.kotlin.plugin.serialization", version.ref = "kotlin" }
```

Step 2: Apply the plugin in your app module

In **`app/build.gradle.kts`**:
```kotlin
plugins {
    alias(libs.plugins.android.application)
    alias(libs.plugins.kotlin.compose)
    alias(libs.plugins.kotlin.serialization) // ← THIS
}
```

Step 3: Add serialization library dependency

In `libs.versions.toml`:
```toml
[libraries]
kotlinx-serialization-json = { 
    group = "org.jetbrains.kotlinx",
    name = "kotlinx-serialization-json",
    version = "1.6.3"
}
```

Then in `app/build.gradle.kts`:
```kotlin
dependencies {
    implementation(libs.kotlinx.serialization.json)
}
```


TODO: parcelize , parcelable

