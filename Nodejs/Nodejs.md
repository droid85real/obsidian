Node.js is a powerful runtime environment for executing JavaScript code.
+ It compiles/Interprets
+ Memory management
+ Handles Input/Output operations
+ Garbage Collection

Chrome browser uses V8 engine (runtime)

> **Note:**
+ `node fileName.js` to run the file

# Working of Nodejs

https://youtu.be/eiC58R16hb8

Client Request → Call Stack → Web APIs (Async Tasks) → Event Queue / Microtask Queue → Event Loop → Call Stack → Response Sent

- **Call Stack** 📦
    - Functions execute here (LIFO - Last In, First Out).
    - If a function is synchronous, it runs immediately.
    - If a function is asynchronous, it is sent to **Web APIs**.
        
- **Web APIs** 🌍
    - When an async operation occurs (like `setTimeout()`, `fetch()`, or `fs.readFile()`), it is **handled by Web APIs** or the **Thread Pool**.
    - Examples:
        - `setTimeout()` → Timer API
        - `fetch()` → Network API
        - `fs.readFile()` → Thread Pool
            
- **Event Queue (Callback Queue) 📬**
    - Once an async operation is done, its **callback** is placed in the **Event Queue**.
    - The **Event Loop** picks tasks from here when the Call Stack is empty.
        
- **Microtask Queue (Priority Queue) 🚀**
    - Holds **high-priority async tasks**, such as:
        - **Promises (`.then()` callbacks)**
        - **process.nextTick() (Node.js-specific)**
            
    - **Microtasks run before normal callbacks** from the Event Queue.
        
- **Event Loop** 🔄
    - The heart of Node.js, constantly checking:
        1. If the Call Stack is empty,
        2. It first executes **Microtasks**,
        3. Then executes tasks from the **Event Queue**.

- Node.js itself is **single-threaded**, but it uses **libuv** (written in C) to create a **thread pool**.
- **Thread Pool** is used for CPU-intensive tasks (file system, database queries, cryptography).
- Default size is **4 threads** but can be increased.

# Libuv
- **What is it?**  
    `libuv` is a **C++ library** used by Node.js to handle **asynchronous I/O operations** like file system tasks, networking, timers, and more.
    
- **Why is it important?**  
    Since Node.js is **single-threaded**, `libuv` helps it achieve **non-blocking I/O** by managing a **Thread Pool** for CPU-intensive tasks.
    
- **Key Features:**
    1. **Event Loop** – Manages async operations.
    2. **Thread Pool** – Handles CPU-heavy tasks (like file I/O, cryptography).
    3. **Asynchronous I/O** – Efficient handling of networking, file system, and DNS.
    4. **Cross-Platform** – Works on Windows, Linux, and macOS.


# HTTP
HTTP sets the rules for how the **client** (browser, app, etc.) and **server** (website backend) communicate. It defines:
1. **How to send a request** (methods like GET, POST, etc.)
2. **What info should be included** (headers, body, etc.)
3. **How the server should respond** (status codes, content types, etc.)

## HTTP Methods (Request Types)

| Method      | Purpose                                  |
| ----------- | ---------------------------------------- |
| **GET**     | Fetch data (e.g., loading a webpage)     |
| **POST**    | Send data (e.g., submitting a form)      |
| **PUT**     | Update existing data                     |
| **DELETE**  | Remove data                              |
| **PATCH**   | Partially update data                    |
| **OPTIONS** | Ask the server what methods are allowed  |
| **HEAD**    | Similar to GET but without response body |

## HTTP Status Codes (Response Types)
| Code Range  | Meaning |
|------------|---------|
| **1xx** | Informational (Processing) |
| **2xx** | Success (✅ Everything is good) |
| **3xx** | Redirection (🔄 Moved elsewhere) |
| **4xx** | Client Errors (❌ You messed up) |
| **5xx** | Server Errors (🔥 Server messed up) |

## Common Status Code
| Code | Meaning |
|------|---------|
| `200 OK` | Success |
| `301 Moved Permanently` | Redirected |
| `400 Bad Request` | Your request is wrong |
| `401 Unauthorized` | Login needed |
| `403 Forbidden` | You don’t have permission |
| `404 Not Found` | The page doesn’t exist |
| `500 Internal Server Error` | Server crashed |

## Content-Type (Tells the Client What Data to Expect)

| Content-Type       | Description  |
|--------------------|-------------|
| `text/html`       | HTML page   |
| `application/json` | JSON data   |
| `image/png`       | PNG image   |
| `audio/mp3`       | MP3 file    |


## Common js Require vs ES6 from
https://www.geeksforgeeks.org/difference-between-node-js-require-and-es6-import-and-export/

| Feature         | require (CommonJS)                  | import/export (ES6 Modules)                                                              |
| --------------- | ----------------------------------- | ---------------------------------------------------------------------------------------- |
| Module System   | CommonJS                            | ES6 Modules                                                                              |
| Syntax          | `const module = require('module');` | `import module from 'module';`                                                           |
| Loading         | Synchronous                         | Asynchronous                                                                             |
| Dynamic Loading | Supported                           | Not natively supported (can use `import()` for dynamic imports)                          |
| Exports         | Single object (`module.exports`)    | Named exports and default exports                                                        |
| Usage Context   | Primarily used in NodeJS            | Supported in modern JavaScript environments, including browsers and NodeJS               |
| File Extension  | `.js`                               | `.js` or `.mjs` (depending on environment and configuration)                             |
| Hoisting        | Non-lexical (stays where placed)    | Lexical (hoisted to the top)                                                             |
| Support         | Widely supported in NodeJS          | Requires enabling ES6 modules in NodeJS (e.g., setting “type”: “module” in package.json) |

# Creating Server
```js
const http = require("http"); //importing http module

const server = http.createServer((req, res) => { //createserver creates an instance of server and takes two parameter, (req,res) is callback function runs every time the server gets a request
    res.writeHead(200, { "Content-Type": "text/plain" }); //set response header
    res.end("Hello, World!\n");
});

const PORT = 3000; // Starts the server on port 3000.
server.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});

```

`node fileName.js` to run the file
```js
const http = require("http"); //import http module

// create http server
const server = http.createServer((req, res) => {
    
    if (req.url === "/") { // check if request url is '/'
        res.write("Hello, this is homepage"); // write some content
        res.end(); // end the response properly
        return; // exit the function early
    }

    // if URL is not "/" , handle other requests
    res.write("Welcome to the server");
    res.end(); // properly end the response
});

// server listening to port 3100
server.listen(3100, () => {
    console.log("Server is running on http://localhost:3100");
});
```

**`req.url`**
- It captures the path from the URL requested by the client.
**`res.end()`**
- Signals that the response is complete. You can pass data to it, and it will be sent as the final part of the response.
**`res.write()`**
- Sends a chunk of data to the client. You can call this multiple times if needed before ending the response.
**`return`**
- Stops further code execution inside the request handler function after sending the response.

The `fs` (File System) module in Node.js provides an **API** for interacting with the file system. It allows you to perform operations like reading from, writing to, and managing files and directories. 
#### Key Features:

- **Read Files**: `fs.readFile()` (async) / `fs.readFileSync()` (sync)
    
- **Write Files**: `fs.writeFile()` (async) / `fs.writeFileSync()` (sync)
    
- **Append to Files**: `fs.appendFile()` (async) / `fs.appendFileSync()` (sync)
    
- **Create Directories**: `fs.mkdir()` (async) / `fs.mkdirSync()` (sync)
    
- **Delete Files**: `fs.unlink()` (async) / `fs.unlinkSync()` (sync)
    
- **Check File/Directory Existence**: `fs.existsSync()` (sync, deprecated) or `fs.access()` (async)


# Two ways to create module in nodejs

# CommonJS Module (`require`, `module.exports`)

Export
```js
// file: math.js
function add(a, b) {
  return a + b;
}
module.exports = { add };
```

OR
```js
module.exports.add=function (a,b){
	return a + b;
};
```

OR
```js
module.exports.add=(a,b)=>{
	return a + b;
};
```

Import
```js
// file: app.js
const math = require('./math');
console.log(math.add(2, 3)); // 5
```

# ES6 Module (ECMAScript Modules) (`import`, `export`)

**Export**
```js
// file: math.mjs or math.js (with "type": "module" in package.json)
export function add(a, b) {
  return a + b;
}

export function sub(a, b) {
  return a - b;
}
```

OR
**Define export at bottom**
```js
// math.mjs or math.js
function add(a, b) {
  return a + b;
}

function sub(a, b) {
  return a - b;
}

export { add, sub };
```


**Named Import**
```js
// file: app.mjs or app.js
import { add, sub } from './math.js';

console.log(add(3, 2)); // 5
console.log(sub(3, 2)); // 1
```

OR
**Import Everything as an Object**
```js
import * as math from './math.js';

console.log(math.add(5, 5)); // 10
console.log(math.sub(5, 2)); // 3
```


**Using Default Export**
```js
// export.js
export default function sayHi() {
  console.log("Hi");
}

// import.js
import sayHi from './export.js';
```


Note: ⚠️ Make sure to set `"type": "module"` in `package.json` or use `.mjs` files for ES6 modules.

---


TODO: 
week2 topic1
+ Lec 4 nodemailer


---
# Events

In Node.js, the `req` object, representing an incoming HTTP request, emits several events during its lifecycle. These events allow you to interact with the request data and process it as it arrives. The most commonly used events are:

- **data**: Triggered when a chunk of request body data is received.
- **end**: Triggered when the full request body has been received.
- **error**: Triggered if an error occurs during the request.
- **close**: Triggered when the connection closes.
- **aborted**: Triggered if the client aborts the request.

## Handling Incoming POST Data in Node.js Using `req.on`

```js
// Import the built-in HTTP module
const http = require('http');

// Create an HTTP server
http.createServer((req, res) => {
  
  // Check if the request is a POST request
  if (req.method === 'POST') {
    let body = ''; // Variable to store incoming data chunks

    // 'data' event fires whenever a chunk of data is received
    req.on('data', (chunk)=> {
      body += chunk.toString(); // Convert Buffer to string and append to 'body'
    });

    // 'end' event fires when all data has been received
    req.on('end', () => {
      console.log('Received body:', body); // Output the complete body to console
      res.end('Body received'); // Respond to the client
    });

    // 'error' event fires if an error occurs while streaming data
    req.on('error', err => {
      console.error('Error while receiving data:', err); // Log the error
      res.statusCode = 500;
      res.end('Internal Server Error'); // Respond with a 500 error
    });

  } else {
    // For non-POST requests, send a simple response
    res.end('Send a POST request');
  }

// Server listens on port 3000
}).listen(3000, () => console.log('Server running on port 3000'));
```

Test above code using postman application
Inside command prompt write node filename.js to run this 

and in postman with post option at http://localhost:3000

inside body (json)
```json
{
    "id": 1,
    "name": "droid85"
}
```


---
# [Event Emitter](https://nodejs.org/en/learn/asynchronous-work/the-nodejs-event-emitter)

https://youtu.be/vw0rb1EnEvQ

week 2 | topic 1 
+ lec10 customevent
+ lec12 advantage of event driven architecture

<u><b>Best practise</b></u>
To apply **SOC** and **SRP** in Node.js:

1. **SOC (Separation of Concerns):**
    - Use a layered architecture (controllers, services, models, etc.).
    - Use middleware to handle concerns like authentication and validation.
    - Keep configuration separate from business logic.
        
2. **SRP (Single Responsibility Principle):**
    - Each module/class should have one responsibility (e.g., controller handles HTTP requests, service handles business logic, repository handles data interaction).
    - Keep modules focused on a single job, like validation, error handling, etc.
    - Isolate business logic from the data layer and use a repository pattern.


---
# Why use `Express`

**What is it?**  
A minimal and flexible Node.js web application framework designed for building web and mobile applications, especially APIs.

**Key Features**
- **Routing**: Easy handling of HTTP requests (GET, POST, PUT, DELETE).
- **Middleware**: Allows code to run during the request-response cycle (e.g., authentication, logging).
- **Extensibility**: Integrates with numerous libraries and modules to extend functionality.
- **Built on Node.js**: Leverages the event-driven, non-blocking nature of Node.js for high performance.
- **Minimal & Lightweight**: Small footprint, focuses on essential features without unnecessary overhead.
+ **TemplateEngine** 

```js
const express = require("express");

const server = express(); //create server

//server.get(path,callback)
server.get("/", (req, res) => { //handle response
    res.send("Welcome to Express server");  //res.send is a wrapper around res.end with other header and other metadata
});

server.listen(3100, () => {
    console.log("Server is listening on 3100");
});
```

> Note :
+ `npm i express` to install express
+ `node filename.js` to run the file


---
### **Common `req` Properties in Express.js**

| Property            | Type                | Description                                                                                                                                            |
| ------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `req.body`          | `object`            | Contains data sent in the **body** of the request (e.g. POST, PUT). Requires body-parser middleware (like `express.json()` or `express.urlencoded()`). |
| `req.params`        | `object`            | Contains **route parameters** from the URL path (e.g. `/users/:id`).                                                                                   |
| `req.query`         | `object`            | Contains URL **query parameters** (e.g. `?name=John&age=25`).                                                                                          |
| `req.file`          | `object`            | Contains **single uploaded file** (used with `multer` middleware).                                                                                     |
| `req.files`         | `array` or `object` | Contains **multiple uploaded files** (also with `multer`).                                                                                             |
| `req.headers`       | `object`            | Contains HTTP **headers** sent by the client.                                                                                                          |
| `req.cookies`       | `object`            | Contains cookies sent by the client. Requires middleware like `cookie-parser`.                                                                         |
| `req.signedCookies` | `object`            | Contains signed cookies (if using `cookie-parser` with a secret).                                                                                      |
| `req.ip`            | `string`            | The IP address of the client making the request.                                                                                                       |
| `req.originalUrl`   | `string`            | The original request URL.                                                                                                                              |
| `req.method`        | `string`            | HTTP method used (GET, POST, PUT, DELETE, etc.).                                                                                                       |
| `req.url`           | `string`            | URL of the request, relative to the app’s root.                                                                                                        |
| `req.path`          | `string`            | The path part of the request URL.                                                                                                                      |
| `req.hostname`      | `string`            | Hostname of the request.                                                                                                                               |

### **Common `res` Methods in Express**
| Method             | Purpose                                     | Example Use Case                               | Notes & Tips                                               |
| ------------------ | ------------------------------------------- | ---------------------------------------------- | ---------------------------------------------------------- |
| `res.send()`       | Sends **string**, **Buffer**, or **object** | `res.send("OK")`, `res.send({ msg })`          | Auto-detects content type; flexible but not ideal for APIs |
| `res.json()`       | Sends JSON with correct `Content-Type`      | `res.json({ token, message })`                 | ✅ Best for APIs                                            |
| `res.status()`     | Sets the HTTP status code                   | `res.status(404).send("Not found")`            | Chain with `.send()` or `.json()`                          |
| `res.sendStatus()` | Sets status code and sends the status text  | `res.sendStatus(403)` → `"Forbidden"`          | Shortcut for status + text                                 |
| `res.redirect()`   | Redirects to another URL                    | `res.redirect('/login')`                       | Mostly for web apps                                        |
| `res.render()`     | Renders a view template (e.g., EJS, Pug)    | `res.render("profile", { user })`              | Used only if you're using a view engine                    |
| `res.set()`        | Sets response headers                       | `res.set("X-Powered-By", "none")`              | For custom headers                                         |
| `res.cookie()`     | Sets a cookie on client                     | `res.cookie("token", jwt, { httpOnly: true })` | Must use `cookie-parser` middleware                        |


---
## **Middleware**

+ In Node.js, middleware refers to functions that are executed during the request-response cycle. 
+ They have access to the `request`, `response` and `next` objects, and they can modify or log information, perform operations (like authentication, logging, data parsing), or pass control to the next middleware function.
+ order matter while execution.

https://www.geeksforgeeks.org/middleware-in-express-js/
https://expressjs.com/en/guide/using-middleware.html
https://youtu.be/n2c0mf1sza4

i.e.
```js
const express = require("express");

const server = express(); // Create server

// server.get(path, callback)
server.get(
  "/",  // Path
  (req, res, next) => { // First middleware
    console.log("first middleware");
    next(); // This calls the next middleware
  },

  (req, res) => { // Second middleware
    // Handle response
    res.send("Welcome to Express server"); // Send is a wrapper around res.end with other headers and metadata
    console.log("second middleware");
  }
);

server.listen(3100, () => {
  console.log("Server is listening on 3100");
});

```

First middleware if not ending response then its first middleware responsibility to call the second middleware by using `next` parameter and `next()` function

i.e.
```js
const express = require("express");

const server = express(); //create server

// Global middleware function
function globalMiddleware(req, res, next) {
  console.log("this is global middleware");
  next(); // Pass control to the next middleware in the stack
}

// Second middleware function
function secondMiddleware(req, res, next) {
  console.log("this is 2nd middleware");
  next(); // Pass control to the next middleware in the stack
}

server.use(globalMiddleware); // Apply the global middleware to all routes

// Define route with multiple middlewares
server.get(
  "/send",  // Path for this route
  (req, res, next) => { // First middleware
    console.log("first middleware");
    next(); // Call the next middleware in the stack
  },

  secondMiddleware, // Second middleware

  (req, res) => { // Third middleware (handles the response)
    res.send("Welcome to Express server"); // Sends the response to the client
    console.log("third middleware");
  }
);

server.listen(3100, () => {
  console.log("Server is listening on 3100");
});
```


---
## **HTTP headers**
https://www.geeksforgeeks.org/http-headers/
https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers

An HTTP header is a key-value pair sent between a client (like a browser) and a server during an HTTP request or response. Headers carry additional information about the request or response, such as content type, authentication, caching, and more.

Here are some common use cases for HTTP headers:

|Header|Use Case|
|---|---|
|`Content-Type`|Specifies the media type of the resource (e.g., `application/json`)|
|`Authorization`|Sends credentials (e.g., tokens) for secure APIs|
|`User-Agent`|Identifies the client software (e.g., browser or app)|
|`Accept`|Informs the server what content types the client can handle|
|`Cache-Control`|Tells browsers how to cache content|
|`Set-Cookie`|Server sets a cookie in the client|
|`Cookie`|Client sends stored cookies back to server|
|`Host`|Specifies the domain name of the server being requested|
|`Referer`|Indicates the previous web page (useful for tracking or security)|
|`X-Forwarded-For`|Reveals original IP address when behind a proxy/load balancer|


---
## **Serving static html file**
+ `npm init` to initialise app 
+ `npm i express` to install express.js
+ `node index.js` to run the code

create file structure where index.js is main entry point.
```
project/
├── index.js        ← Entry point
├── src/
│   └── public/
│       └── index.html
```

index.js
```js
const express=require('express');
const path=require('path');

const app=express();
// Serve static files from 'src/public'
app.use(express.static(path.join(__dirname,'src','public')));

app.listen(3000,()=>{
    console.log('server is running at http://localhost:3000');
});
```

>`path.join(__dirname,'src','public')` ensures the path resolves correctly regardless of where the script is run from.


## Path module

https://www.geekster.in/articles/path-module-in-node-js/

### 🔹 `__dirname`
- It is a **global variable** in Node.js.
- Always returns the **absolute path of the directory** that contains the **currently executing file**.
- It does **not** change regardless of where the script is run from.

i.e.
```js
console.log(__dirname);
// Output might be: /Users/yourname/project/src
```

---

### 🔹 `path.resolve([...paths])`

- It is a **method** from Node.js's `path` module.
- Resolves a sequence of paths or path segments into an **absolute path**.
- It starts from the rightmost path and processes it as an absolute path **if it is already absolute**; otherwise, it uses the current working directory or previous segments.

i.e.
```js
const path = require('path');

console.log(path.resolve('foo/bar'));
// Output: /Users/yourname/current-dir/foo/bar

// Using __dirname
console.log(path.resolve(__dirname, 'foo/bar'));
// Output: /Users/yourname/project/src/foo/bar
```

---
### ✅ When to Use What?

| Use Case                        | Use `__dirname`                          | Use `path.resolve()`                          |
| ------------------------------- | ---------------------------------------- | --------------------------------------------- |
| Get current file’s directory    | ✅                                        | ❌ unless combined with `__dirname`            |
| Build absolute paths safely     | ✅ with `path.join()` or `path.resolve()` | ✅ (usually with `__dirname` or process.cwd()) |
| Relative to current working dir | ❌                                        | ✅                                             |

**If You're Using CommonJS :**

```js
return res.sendFile(path.join(__dirname,'src','views','index.html'));
```

✅ Works fine — `__dirname` is available.

### If You're Using ES Modules (e.g., using `import` like in your code):

`__dirname` is **not available by default** in ES Modules.
```js
return res.sendFile(path.join(path.resolve(),'src','views','index.html'));
```

✅ `path.resolve()` with no arguments is equivalent to `process.cwd()` (the current working directory). This works as long as you run your app from the project root.

```js
return res.sendFile(path.resolve('src','views','index.html'));
```

---

### **MVC architecture**

The three parts of the MVC software-design pattern can be described as follows:

1. Model: Manages data and business logic.
2. View: Handles layout and display.
3. Controller: Routes commands to the model and view parts.
 🧠 In Node.js (with Express), you can organize your project in MVC style for clarity and separation of concerns.


---
### **REST API**

**Architectural style** for designing networked applications.

- Uses HTTP methods: `GET`, `POST`, `PUT`, `DELETE`
- Resources are identified by **URLs**.
- Cross platform support.
- **Stateless** – every request from client to server must contain all the information to understand the request.


---
### **Web API**

More **generic** term. Any API that’s accessible over the web.

- REST API is **a type** of Web API.
- Web API could also use **`GraphQL`**, **SOAP**, or **`WebSockets`**, not just **REST**.

Example: REST API in Node.js using MVC

```
project/
├── models/
│   └── userModel.js
├── controllers/
│   └── userController.js
├── routes/
│   └── userRoutes.js
├── app.js
```

- `app.js` → Sets up Express and routes.
- `userRoutes.js` → Defines REST endpoints.
- `userController.js` → Handles logic for each endpoint.
- `userModel.js` → Handles database-related logic.


---
---
## Inventory App Project
used
+ express
+ ejs (for dynamic content)
+ ejs-layout (to separate web page components)
+ mvc pattern (architecture style)
+ express-validator (for form validation)
+ multer (to upload file)
+ express-session (for session)
+ cookie-parser (for cookies)
+ dotenv (for env support)

Start
+ `npm init` to initialise app 
+ `npm i express` we will we working with express.js
+ create file structure where index.js is main entry point.
+ change `"type": "module",` in `package.json` and stick with ES6 import/Export 

For template literals in product.html to dynamically load data we use `npm ejs`
https://www.npmjs.com/package/ejs
+ `npm i ejs` to install 
+ then setup view engine in index.js
+ also rename `product.html` to `product.ejs`
+ and use `res.render(view,data)` to send data dynamically in `product.controller.js`
+ `res.render(view,data)` in here data is key value pair and is optional
+ use `<%= %>` to assign variable in `product.ejs`

Separate `nav` from `main` in `product.ejs`
https://www.npmjs.com/package/express-ejs-layouts
+ `npm i express-ejs-layouts` To install ejs layout
+ setup `express-ejs-layout` in index.js
+ split `product.ejs` into `nav.ejs` and `layout.ejs` in views
+ to include nav and body in `layout.ejs` use
	+ `<%- include('nav') %>` for nav
	+ `<%- body %>` for rest of body

Add new product form
+ inside product.controler.js we make another `getAddForm` (function) so user can get form to add product in product.controller.js
+ then, in index.js set routing using `server.get(route,functioncall)` in index.js
+ add another function `addNewForm(req,res)` which submit new product in product.controller.js
+ then add routing `server.post('/',productController.addNewForm)` in index.js
+ parse data and update on submit
	+ to parse `server.use(express.urlencoded({extended:true}));` in index.js
	+ and to add data we create `static add()` in product.model.js
	+ and pass data to it we use `addNewForm()` in product.controller.js and call it at index.js
	+ and to input data we used `new-product.ejs` using form html

Validating form data, server side and html form and also repopulate on error
+ validating data at `addNewForm()` in product.controller.js
+ and then passing `errorMessage` and `formData` (to repopulate) if error>0, through `getAddForm()` to `new-product.ejs` using `res.render(route,data)` in product.controller.js
+ also passing `errorMessage` and `formData` initially as null and empty in `getAddForm()` in product.controller.js
+ and looping over `errorMessage` and set `formData` in value of form to repopulate in `new-product.ejs`

Shifting validation code to middleware level
+ for SOP and lose coupling
+ shift validation code from `addNewForm()` (product.controller.js) to validate.middleware.js
+ and add middleware in index.js
	+  `server.post('/',valdationMiddleware,productController.addNewForm); `

Using express-validator for validating data instead of our own validator
https://www.npmjs.com/package/express-validator
+ `npm i express-validator` To install express validator
+ remove old validation code in validate.middleware.js and 
+ express validator requires three steps 
1.setup rules
+ using `body` object from `express-validator`
2.run those rules
+ running rules can be async so we use promise
+ `Promise.all()` it takes an array of promises and execute all of them and `await` is for waiting for execution to end
+ and `await` requires `async`
3.check if there any errors after running the rules
+ using `validationResult` from express-validator
+ `validationResult` return all the errors that appeared while running the rules 
+ and then pass that error to `new-product.ejs` through `errorMessage` in `res.render()` in `validation.middleware.js`

Update Product that already exist
+ `getUpdateProductView()` in product.controller.js so if product exist it return view or else error
	+ we used `req.params.id` to get access to id parameter
+ create static `getProductById()` in product.model.js to return product by id
+ create `update-product.ejs` in views
	+ it shows old data of product and have id input hidden
+ and provide routing in index.js i.e. `server.get("/update-product:id,middleware")`
+ add update button in `product.ejs`
	+  which send id embedded with URL

+ and now to update the data 
+ create `server.post("/update-product",productController.postUpdateProduct);` in index.js
+ in `update-product.ejs` in form action 
	+ `<form action="/update-product" method="post">`
+ in product.controller.js create `postUpdateProduct()` to pass data and redirect
+ in product.model.js create `static update()` to update the product data

Adding Delete product button and functionality
+ add delete button in `products.ejs`
+ add routing in index.js `server.get("/delete-product/:id",productController.deleteProduct);`
+ add `deleteProduct()` in product.controller.js which checks if product is present then delete or else throw status code 401 not found
+ add `static delete()` in product.model.js

Confirm before delete
+ `onClick("deleteProduct('')")` in `products.ejs`
+ then add main.js in public
+ link main.js using script tag in `products.ejs`
+ in product.model.js , at `add()` we changed id generator to take current time as id

Add and Upload files instead of image URL using Multer
https://www.npmjs.com/package/multer
+ `npm i multer` To install `multer`
+ make changes in `new-product.ejs` and `add-product.ejs`
	+ changing `<input type="file" accept="images/*" />` to accept only all images
	+ and `<form enctype="multipart/form-data" >` To accept file as well as some text
+ create `upload.middleware.js` and config `multer` so files uploaded are stored inside `public/images` using `diskStorage()`
	+ `diskStorage()` have two call back function , destination(to tell the storage location) and filename (to tell filename)
+ apply middleware in index.js at `server.post('/',uploadFile.single("imageUrl"),valdationMiddleware,productController.addNewForm);`

| `Multer` changes how the uploaded data appears in  |  `req`:     |
| -------------------------------------------------- | ----------- |
| Text fields (e.g., `name`, `description`, `price`) | `req.body`  |
| Single file upload (e.g., `imageUrl`)              | `req.file`  |
| Multiple files (e.g., `images[]`)                  | `req.files` |

+ make changes to product.model.js to accept `imageUrl` from `req.file` instead of `req.body` in `static add()`
+ similar changes to `update-product.ejs` and update in product.model.js and  `postUpdateProduct()` in product.controller.js and also apply middleware in index.js `server.post("/update-product/",uploadFile.single("imageUrl"),productController.postUpdateProduct);`

User registration and login
registration
+ create user.model.js inside it define constructor
+ create `register.ejs` define html form for user registration
+ create user.controller.js and inside it define `getRegistrationForm()` and inside it `res.render("ejs fileName which needs to be rendered")`
+ in index.js create instance of `UserController` and define routing `server.get("/register",usersController.getRegistrationForm);`

+ inside user.controller.js define `postRegistrationForm()` to pass data to `user.model.js` and redirect to login
+ inside user.model.js define `addUser()` to add new user and add user sample data
+ to post data define `server.post("/register",usersController.postRegistrationForm);`

+ create `userRegisterValidation.middleware.js` and setup and configure user validation using `express-validator`
+ make changes to `register.ejs` so it can show error and repopulate old data when error occur
+ in index.js, change to `server.post("/register",userRegisterValidationMiddleware,usersController.postRegistrationForm);`
+ in user.controller.js , change `getRegistrationForm` so it sends `errorMessage` and `formData` initially to `null` and `{}`
+ in user.controller.js ,in `postRegistrationForm()`, check if user already exist .
+ in index.js define `server.post("/login",usersController.postLogin);` to post login data


login
+ similar steps for login
+ create view `login.ejs`
+ create `getLogin()` to render `login.ejs` in user.controller.js
+ in index.js define routing `server.get("/login",usersController.getLogin);`
+ create `postLogin()` in user.Controller.js to check posted data and grant login


Session and logout feature
https://www.npmjs.com/package/express-session
+ `npm i express-session` To install express session
+ in index.js ,setup `express-session`
+ user.controller.js ,in `postLogin()` , save user data to session using `req.session`
+ create auth.middleware.js which check if every request made by client have session id, if not then redirect to login
+ in index.js ,apply middleware to secure add-product, update-product and delete-product request only be done by logged in user
+ add logout button in `nav.ejs` using `locals` of `ejs`
+ place, config `users` globally in `res.locals` for all views, after express-session config in index.js
+ destroy session on `logout()` in user.controller.js
+ and define routing in index.js `server.get("/logout",usersController.logout,);`

Cookies
https://www.npmjs.com/package/cookie-parser
+ `npm i cookie-parser` To install cookie parser
+ create `lastSeen.middleware.js` and inside it setup cookie and `res.cookie(nameOfCookie,Data,options)`
+ in `products.ejs `, make changes to show last seen
+ in index.js before express-session config , config cookie-parser and `setLastVisit` middleware

+ destroy cookie on `logout()` in user.controller.js
+ set cookie on get product request only in index.js

Secure secret key, add .env support
https://www.npmjs.com/package/dotenv
+ `npm install dotenv` To install `dotenv`
+ change security code in session cause it is exposed in git 
+ create .env and setup session-token code there
+ create .`env.example` for example for other dev
+ config `dotenv` in index.js like this `dotenv.config();`
+ and use `secret:process.env.SESSION_SECRET` to secure session secret key in config session in index.js

+ `npm audit` To check for vulnerability

inside .gitignore define below so we ignore rest file but keep .gitkeep 
```
src/public/images/*
!src/public/images/.gitkeep
```





---
---
### `express-session` For session
https://www.npmjs.com/package/express-session
+ http is stateless so session provide additional information
+ Sessions are used to persist user data cross multiple requests. This is crucial for functionalities like login/logout ,shopping cart etc
+ A session stores data on the server about the user where as cookies stores data on the client/browser

+ `npm i express-session` To install express session

configure session middleware for the express app
``` js
//inside index.js
app.use(session({
  secret: 'your-secret-key',
  resave: false,
  saveUninitialized: false,
  cookie: { maxAge: 1000 * 60 * 60 }// 1 hour
}));
```

- `secret`: Signs the cookie to prevent tampering.
- `resave: false`: Don’t resave if session is unchanged.
- `saveUninitialized: false`: Avoid saving empty sessions (e.g., anonymous visits).
- `cookie.maxAge`: Session lifespan (in ms). After this, session expires.
You can also use:
- `secure: true` → cookie sent only over HTTPS
- `httpOnly: true` → prevents JavaScript access (helps stop XSS attacks)
- `sameSite: 'strict' | 'lax' | 'none'` → controls cross-site cookie behaviour

+ save user data to session using `req.session`


---
---
TODO:  Session Store
By default, sessions are stored **in-memory**, which is **not recommended** for production. Instead, use:
- `connect-mongo` → store sessions in MongoDB
- `connect-redis` → store sessions in Redis
- `express-mysql-session` → store sessions in MySQL

---
---
### `res.locals` (Express)
- Temporary object to pass data from Express backend to views.
- Lives only during the current request–response cycle.

```js
app.use((req, res, next) => {
  res.locals.user = req.session.user || null;
  next();
});
```
This middleware attaches the currently logged-in user to `res.locals`, so you can **access `user` in all EJS templates without explicitly passing it every time**.

use case:
+ Make data (like session user, flash messages, etc.) available in all EJS views without passing in `res.render()` every time.

- Use it in EJS as just `user`, not `res.locals.user`.
- `res.locals` is **backend-side** (Express).
- Views access it as `user`, not `res.locals.user`.

---
### locals (EJS)

- Internal object used by EJS to hold all view variables.
- You can use `<%= title %>` or `<%= locals.title %>` (both work).
- Comes from either `res.render('view', { ... })` or `res.locals`.
- You rarely write `locals.` — it's handled behind the scenes.

---
### `cookie-parser` For Cookies 
+ Cookies in Node.js are key-value pairs stored on the client’s browser
+ sent with each request to the server. 
+ They are commonly used for sessions, user preferences, authentication, etc.

https://www.npmjs.com/package/cookie-parser
`cookie-parser` is a middleware for Express that **parses cookies** from the HTTP `Cookie` header and makes them **easily accessible via `req.cookies`**.
+ `npm i cookie-parser` To install cookie parser
+ use `req.cookies` To access, `res.cookie()` to set, `res.clearCookie()` to delete
+ use `cookie-parser('secret key)` To signed cookies
+ `res.cookie(nameOfCookie,Data,options)`

```js
import express from 'express';
import cookieParser from 'cookie-parser';

const app = express();

// Optional: add a secret string to sign cookies
app.use(cookieParser('mySecretKey'));

// Reading cookies
app.get('/get', (req, res) => {
  console.log(req.cookies);         // Unsigned cookies
  console.log(req.signedCookies);   // Signed cookies
  res.send('Check your console');
});

// Setting a cookie
app.get('/set', (req, res) => {
  res.cookie('user', 'droid85', { maxAge: 900000, httpOnly: true });
  res.send('Cookie has been set');
});

// Setting a signed cookie
app.get('/set-signed', (req, res) => {
  res.cookie('token', 'abc123', { signed: true });
  res.send('Signed cookie set');
});

// Deleting a cookie
app.get('/delete', (req, res) => {
  res.clearCookie('user');
  res.send('Cookie deleted');
});

```

---
### `dotenv` For env support
https://www.npmjs.com/package/dotenv
+ `npm install dotenv` To install `dotenv`
+ create .env and setup session-token code there i.e. `VARIABLE_NAME=longSecretKey`
+ create .`env.example` for example for other dev
+ config `dotenv` in index.js like this `dotenv.config();`
+ and use `secret:process.env.VARIABLE_NAME` to secure session secret key in config session in index.js

---
### `npm audit` 
- Scans all your **dependencies and their sub-dependencies**
- Checks them against the **NPM vulnerability database**
- Tells you:
    - What’s vulnerable
    - What severity (low → critical)
    - What to upgrade/fix

---
### `npm audit fix`
- Automatically updates vulnerable packages **only if safe**  
    (doesn't break server or known compatibility)
- Leaves the rest for you to **manually decide** if needed

---

|Feature|MVC (EJS-based)|REST API (JSON-based)|
|---|---|---|
|**Rendering**|Server renders views (HTML)|Frontend handles rendering (React, etc.)|
|**Frontend-Backend**|Tightly coupled|Decoupled (can serve mobile/web/other apps)|
|**Scalability**|Limited|High — plug into multiple clients|
|**Data format**|HTML|JSON (standard for web APIs)|
|**Best for**|Small apps, internal tools, admin panels|Public APIs, large systems, SPAs|


>Note:
>// ✅ Always define static routes like "/filter" BEFORE dynamic ones like "/:id"




---
---
## E-comm project using REST API
Uses
+ express
+ body-parser (to parse json data)
+ multer (to upload image)
+ dotenv (for env support)
+ 



**Start**
+ `npm init` to initialise app 
+ `git init` To initialise git
+ create repo in github and use ssh
+ create `.gitignore` and `.env` 
+ `npm i express` To install express
+ create file structure where index.js is main entry point.
+ create basic server with express in index.js and `node index` To run
+ change `"type": "module",` in `package.json` and stick with ES6 import/Export
+ `git status` and then `git add .` then `git commit -m "msg"` then `git push` 

Basic Folder Structure
├── index.js                  // Entry point
├── .env                     // Environment config
├── .gitignore               // Ignore node_modules, .env  etc
└── src/
    └── modules/
        └── product/
            ├── product.routes.js       // Routing logic
            └── product.controllers.js  // Business logic


+ in index.js , `server.use("/api/products",productRoutes);` To redirect all product related request to `productRoutes` 
+ define `productRoutes` in product.routes.js using `express.Router()`
+ and for routing `productRoutes.httpMethodName("route",productController.middlewareName);` and here routes have already completed `/api/products`
+ define different middleware inside product.controller.js like
	+ `getAllProducts() , postAddProduct(), rateProduct(), getOneProduct(), filterProduct()`

+ create product.model.js ,define constructor , sample products and `static getAll()`
+ in product.controller.js , in `getAllProducts()` use `getAll()` and `res.send(products);`
+ now check "http://localhost:3000/api/products" you will get all the products

**Use body-parser to parse json data** 
https://www.npmjs.com/package/body-parser
+ `npm i body-parser` To install body-parser
+ in index.js ,  config body-parser ,`server.use(bodyParser.json());`
+ in product.model.js define static add() to add new product and call this in `postAddProduct()` and set route in `product.route.js` on post req 

+ now test post, in product.controller.js in `postAddProduct()` use `console.log(req.body)`
+ open postman , httpmethod: post, url: http://localhost:3000/api/products , body>raw>json 
```json
  {
    "name": "Puma Sports T-shirt",
    "desc": "Breathable, sweat-wicking t-shirt for gym and outdoor workouts.",
    "price": 899,
    "imageUrl": "https://dummyimage.com/200x200/ff0066/ffffff&text=Puma+Tee",
    "category": "Clothing",
    "sizes": [
      "S",
      "M",
      "L"
    ]
  }
```


**Add and Upload files instead of image URL using Multer**
https://www.npmjs.com/package/multer
+ `npm i multer` To install `multer`
+ create `fileUpload.middleware.js`
+ create `fileUpload.middleware.js` and config `multer` so files uploaded are stored inside `src/uploads` using `diskStorage()`
	+ `diskStorage()` have two call back function , destination(to tell the storage location) and filename (to tell filename)
+ apply middleware in product.routes.js at `productRoutes.post("/",uploadFile.single("imageUrl"),productController.postAddProduct,);`

| `Multer` changes how the uploaded data appears in  |  `req`:     |
| -------------------------------------------------- | ----------- |
| Text fields (e.g., `name`, `description`, `price`) | `req.body`  |
| Single file upload (e.g., `imageUrl`)              | `req.file`  |
| Multiple files (e.g., `images[]`)                  | `req.files` |

+ make changes to product.model.js to accept `imageUrl` from `req.file` instead of `req.body` in `static add()` and sizes to array.
+ test `addProduct()` using postman
	+  httpreq: post , url: http://localhost:3000/api/products
	+ body>form-data>


inside .gitignore define below so we ignore rest file but keep .gitkeep 
```
src/uploads/*
!src/uploads/.gitkeep
```

**Get One Product API**
+ create `static get()` in product.model.js and create `getOneProduct()` in product.controller.js and call it in product.routes.js at `productRoutes.get("/:id",productController.getOneProduct);`

**Get Filtered Products** 
+ create `static filter()` in product.model.js and create `getFilteredProduct()` which use `req.query` to get filters in product.controller.js and define route in product.routes.js which calls `getFilteredProduct()` i.e. `productRoutes.get("/filter",productController.getFilteredProducts);`
+ and always define static routes first then dynamic route like /:id

+ Test it in postman httpReq: GET, url: http://localhost:3000/api/products/filter?minPrice=10&maxPrice=20000&category=Clothing


**Basic User signup, signin**
+ create user.model.js , user.controller.js , user.routes.js in user folder
+ define `server.use("/api/users",userRoutes);` in index.js to redirect all user related req to user.routes.js
+ define user.routes.js for routes
	+ initialize `express.Routes()`
	+ create instance of `UserController()`
	+ `userRoutes.httpMethodName("route",middleware)` to call method like signUp and signIn on that route
	+ in user.controller.js , we create middleware like signUp and signIn and pass req and send res
+ in user.model.js ,define methods `SignUp()` and `SignIn()` to actually handle user creation and loggin 

+ Test using postman
	+ httpReq: POST , URL: http://localhost:3000/api/users/signin
	+ body>raw>json
```json
{ 
  "name": "Test User",
  "email": "test@example.com",
  "password": "Password1",
  "type": "buyer"
}
```


**Basic Authentication using req.headers***
+ create `basicAuthorizer.middleware.js` , 
- Middleware Entry Point:  `const basicAuthorizer=(req,res,next)=>{`
    The function receives `req`, `res`, and `next` to control route access.
    
- Check Authorization Header (HTTP header validation)_:
    - Look for `Authorization` header in the request. Using `req.headers`
    - If missing → respond with `401 Unauthorized`.
    
- Extract and Decode Base64 Credentials (Base64 decoding with `Buffer`)_:
    - Remove the `"Basic"` prefix.
    - Decode the Base64 string into a `utf8` string in the format: `email:password`.
    
- Parse Credentials (String splitting)_:
    - Use `.split(":")` to extract `email` and `password` values.
    
- User Lookup (Simple in-memory user validation)_:
    - Call `UserModel.findByEmail(email)` to find the user.
    - If not found → respond with `401 Incorrect Credentials`.
    
- Password Validation
    - Compare decoded password with the stored password.
    - If mismatch → respond with `401 Incorrect Password`.
    
- Access Granted:
    - If credentials match → call `next()` to continue to the protected route.

+ apply basicAuth middleware in index.js `server.use("/api/products",basicAuthorizer,productRoutes);`

+ Test it in postman
	+ httpReq: get , URL: http://localhost:3000/api/products
	+ Authorization (BasicAuth), then fill username:email and password:password


**JWT implementation**
+ in user.controller.js , in `postSignIn()` , create JWT , when user credential matches.
	+ sign token , `jwt.sign(payload, secretOrPrivateKey, [options, callback])`
	+ and return token 
+ Test on postman
	+ httpReq: POST , URL: http://localhost:3000/api/users/signin
	+ body>raw>json
```json
{
  "email": "test@example.com",
  "password": "Password1"
}
```

+ Verify JWT 
	+ create `jwt.middleware.js` , and check if req.headers have token 
		+ if no token then return unauthorized
		+ and if token present then verify token using `jwt.verify(token, secretOrPublicKey, [options, callback])` which returns payload
		+ if error occur then send unauthorised 
		+ call `next()` middleware
	+ apply jwtAuth middleware instead of basicAuth in index.js `server.use("/api/products",jwtAuth,productRoutes);`

+ Test in postman
	+ To signUp
	+ httpReq: POST , URL: http://localhost:3000/api/users/signup
	+ body>raw>json>
``` json
{
  "name": "Test User",
  "email": "test@example.com",
  "password": "Password1",
  "type": "buyer"
}
```

+ To signIn (token creation)
+ httpReq: POST, URL: http://localhost:3000/api/users/signin
+ body>raw>json
```json
{
  "email": "test@example.com",
  "password": "Password1"
}
```

+ To load products after jwt auth (token verification)
+ httpReq: GET , URL: http://localhost:3000/api/products/filter?minPrice=10&maxPrice=20000&category=Clothing
+ Headers>Key: Authorization , Value: token received from logging


**Rate Products** 
+ in product.model.js,  create `static rateProduct()` which first validate user, using UserModel.findByEmail(), which get userEmail from req.user=payload on verification of jwt, which is defined in jwt.middleware.js.
+ then validate product and checks if user have already rated product before if so then update rating if no rating by that user exist then create rating
+ in product.controller.js , create postRateProduct() middleware , which handle passing of req.query and sending status and res.
+ in product.routes.js , `productRoutes.post("/rate",productController.postRateProduct);`
	+ call postRateProduct() for route "http://localhost:3000/api/products/rate"

+ Test on postman
	+ To signin
	+ httpReq: POST , URL: http://localhost:3000/api/users/signin
	+ Body>raw>json
```json
{
    "email": "seller@com.com",
    "password": "Password1"
}
```

+ To test rating
+ httpReq: POST , URL: http://localhost:3000/api/products/rate?productId=1&rating=5
+ Headers>key: Authorization, Value: token received from logging(from above)


**Cart Feature**
+ create cart.routes.js , cart.model.js , cart.controller.js
+ in index.js , add `server.use("/api/cart",jwtAuth,cartRoutes);` To redirect all cart related req to cart.routes.js
+ in cart.routes.js , initialize express router , create instance of cart controller and define routes for get req to call getCart middleware and for post req on that route to call postAddCart middleware.
+ in cart.controller.js , define `postAddCart()` whose work is to pass productId,quantity from query and userId from req.user.userId (JWT verification payload) to add in cart.model.js and
+ `getCart()` to get cart related to authenticated user
+ in cart.model.js , define `add()` To add cart item
+ and `get()` To get cart related to specific user

+ To delete cart
+ 

Test on postman
+ To signin
+ httpReq: POST , URL: http://localhost:3000/api/users/signin
+ BODY>raw>json
```json
{
    "email": "seller@com.com",
    "password": "Password1"
}
```

+ To post product to cart
+ httpReq: POST , URL: http://localhost:3000/api/cart?productId=2&quantity=1
+ Headers>key: Authorization , value: Token received from loggin


+ To get cartItem
+ httpReq: GET, URL: http://localhost:3000/api/cart
+ Headers>key: Authorization , value : Token received from loggin









delete






week 6 | Topic 1 | 
+ lec6















---

TODO:
+ express-validator to validate data before adding product
+ In a real-world scenario, you'd **hash passwords on sign up** and **compare hashes** on login using `bcrypt.compare()`.
+ Move from req.query to req.body for post req at postAddcart and in rating.
+ instead of using same post req to add and update cartIteam ,split it into post (to add) and put (to update)
+ deleteCartItem, one cart on every one user, contain multiple products. and user and product validation and cart validation before delete.



---
TODO: in depth 
ejs (for dynamic content)
ejs-layout (to separate web page components)
express-validator (for form validation)
Multer (to upload file)
cookie-parser
express-session
body-parser





---
### JWT (JSON Web Token)
https://www.geeksforgeeks.org/web-tech/json-web-token-jwt/
https://www.jwt.io
https://www.npmjs.com/package/jsonwebtoken

+ A JWT is a self-contained token that contains information (called claims) about the user and is digitally signed so it can't be tampered with.

**Structure**
```
xxxxx.yyyyy.zzzzz
|     |     |
|     |     └── Signature (to verify integrity)
|     └─────── Payload (user data)
└───────────── Header (token type & algorithm used for signing)
```

**Why use JWT in Node.js?**
- **Stateless** (no session store on the server)
- **Scalable** (ideal for microservices)
- **Portable** (can be stored in cookies or localStorage)

**How JWT Auth works(Flow)**

|Step|Description|
|---|---|
|1.|User sends login credentials|
|2.|Server verifies credentials|
|3.|Server creates a **JWT** and sends it back|
|4.|Client stores the JWT (localStorage/cookies)|
|5.|Client includes JWT in `Authorization` header in each request|
|6.|Server **verifies JWT** on each request to authorize user|

**Tech Stack**
- `jsonwebtoken` – to sign/verify tokens
- `bcrypt` – to hash passwords
- `express` – web framework


+ `npm i jsonwebtoken` To install JWT
+ `jwt.sign(payload, secretOrPrivateKey, [options, callback])` To sign token after credential verification
+ `jwt.verify(token, secretOrPublicKey, [options, callback])` To very token received from user using req.headers to get token then verify

|Do|Don't|
|---|---|
|Use **short-lived** access tokens|Don't store tokens in plain text|
|Store secret in `.env`|Never expose `SECRET_KEY` in frontend|
|Use **HTTPS**|Don’t use JWT for sensitive data (e.g. password)|
|Implement **refresh tokens** for long sessions|Don’t keep token lifetime too long|


|Feature|JWT|Session|
|---|---|---|
|Stateless|✅ Yes|❌ No (stored server-side)|
|Scalable|✅ Yes|❌ Limited by server memory|
|Storage|Client (cookie/localStorage)|Server (RAM or DB)|
|Token expiry|Built-in|Manual|

---

|Use `req.query` when:|Use `req.body` when:|
|---|---|
|You’re doing a **GET**|You’re doing **POST/PUT**|
|You’re **filtering**|You’re **sending data**|
|URLs like `/products?cat=shoes`|JSON like `{ productId: 1, quantity: 2 }`|