## Introduction to JavaScript

This guide introduces JavaScript’s origins, its core characteristics, and how to write your first snippet. You’ll learn what makes JavaScript unique among languages, where it runs, and explore basic syntax—including variables, data types, and control flow—so you can confidently transition into modern frameworks like React and React Native.

---

## What Is JavaScript?

JavaScript (often abbreviated JS) is a lightweight, interpreted (or just-in-time compiled) programming language with first-class functions, predominantly known as the scripting language of the Web.
It supports multiple paradigms—object-oriented via prototypes and classes, imperative, and functional programming—making it extremely versatile.
Beyond browsers, JavaScript powers server-side environments such as Node.js, as well as desktop and mobile apps (e.g., Electron, React Native).

---

## History & Standardization

Created in just ten days in 1995 by Brendan Eich at Netscape, JavaScript was originally called Mocha and LiveScript before being renamed to leverage Java’s popularity. In 1997, it became standardized as ECMAScript under the ECMA-262 specification, ensuring cross-platform consistency of the “language core,” while the term “JavaScript” remains its everyday name.

---

## Where JavaScript Runs

- **Browser Engines**: Chrome’s V8, Firefox’s SpiderMonkey, Safari’s JavaScriptCore execute JS to manipulate web pages, handle events, and interact with browser APIs (DOM, fetch, localStorage).  
- **Server-Side**: Node.js uses V8 to run JS on servers, enabling full-stack development with a single language.
- **Cross-Platform Frameworks**: Electron (desktop), React Native (mobile), and others embed JS engines to power native-like apps

---

## Core Characteristics

- **Single-Threaded & Event-Driven**: JavaScript uses an event loop and non-blocking I/O, allowing high concurrency in web and server environments without multi-thread complexity.  
- **First-Class Functions**: Functions can be assigned to variables, passed as arguments, and returned from other functions—enabling callbacks, higher-order functions, and functional patterns.  
- **Dynamic Typing**: Variables do not have fixed types; values carry types at runtime, boosting flexibility but requiring careful handling to avoid type-related bugs.
---

## Your First JavaScript: “Hello, World!”

Place this in an HTML file and open it in a browser:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Hello JavaScript</title>
</head>
<body>
  <script>
    // Display an alert dialog
    alert('Hello, JavaScript!');
    console.log('Hello, JavaScript!'); // Also logs to the console
  </script>
</body>
</html>
```
Run this in any modern browser to see JavaScript in action.
---

## Variables & Data Types

- **Declarations**  
  - `let` & `const` introduce block-scoped variables; `const` for constants, `let` for mutable values.  
  - Legacy `var` is function-scoped and generally discouraged in modern code.
- **Primitive Types**  
  - `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, and (ES2020) `bigint`
- **Objects & Arrays**  
  - Objects: key-value stores for grouping related data.  
  - Arrays: ordered lists, manipulated via array methods (`push`, `map`, `filter`, etc.).

---

## Functions & Control Flow

- **Function Basics**  
  ```js
  function greet(name) {
    return `Hello, ${name}!`;
  }
  // Arrow function equivalent
  const greet = name => `Hello, ${name}!`;
  ```
  Arrow functions provide a concise syntax and lexically bind `this` .

- **Conditional Statements**  
  ```js
  if (age >= 18) {
    console.log('Adult');
  } else {
    console.log('Minor');
  }

  // Ternary operator
  const status = age >= 18 ? 'Adult' : 'Minor';
  ```

- **Loops**  
  ```js
  // for loop
  for (let i = 0; i < 5; i++) {
    console.log(i);
  }
  // for...of
  for (const item of [10,20,30]) {
    console.log(item);
  }
  ```
  JavaScript supports `while`, `do…while`, `for`, `for…in`, and `for…of` loops  ([The Modern JavaScript Tutorial](https://javascript.info/?utm_source=chatgpt.com)).

---

## Next Steps

- **Deepen Fundamentals**: Explore the Modern JavaScript Tutorial’s [JavaScript Fundamentals](https://javascript.info/intro) to reinforce these concepts  ([An Introduction to JavaScript](https://javascript.info/intro?utm_source=chatgpt.com)).  
- **Modules & Tooling**: Learn ES6 modules, bundlers (Webpack), and transpilers (Babel) to structure larger codebases.  
- **Async Patterns**: Practice Promises and `async`/`await` for clean asynchronous code.  
- **Hands-On Projects**: In the practical session, build a small interactive app (e.g., a “Guess the Number” game) to cement your understanding before moving on to React and TypeScript.

---