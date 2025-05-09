# 🧠 Introduction to JavaScript

This guide introduces JavaScript’s origins, syntax, and mindset. You’ll understand what makes JavaScript so powerful, where it runs, and how it’s used in mobile development—especially with React Native. We’ll write our first JavaScript snippet, cover key concepts like variables, types, functions, and control flow, and set the foundation for the next lessons.

> 🧭 **Prerequisites**: You should have basic familiarity with HTML and CSS. This lesson builds directly on that.

---

## 🛠 Why JavaScript?

JavaScript is the programming language **behind the web**, and it's also the **core language of React Native**, the mobile app framework we’ll be using throughout this course. With JavaScript, you can:

* Add behavior and interactivity to web pages.
* Write full mobile apps (React Native).
* Build server-side apps (Node.js).
* Share logic across web, mobile, and desktop platforms.

---

## 🧬 What Is JavaScript?

JavaScript (often abbreviated JS) is a **lightweight, interpreted** language with **first-class functions**, meaning functions are treated like values.

* **Multi-paradigm**: You can write object-oriented, functional, or procedural code.
* **Dynamic typing**: Variable types are flexible and determined at runtime.
* **Runs everywhere**: Browsers, servers, mobile apps, even IoT devices.

---

## 📜 A Bit of History

JavaScript was created by **Brendan Eich** in 1995 in just 10 days. Originally called *Mocha*, then *LiveScript*, it was renamed to ride the popularity of Java at the time.

In 1997, it became standardized under **ECMAScript (ECMA-262)**. “JavaScript” is the practical name we still use.

---

## 🌍 Where Does JavaScript Run?

```txt
HTML + CSS → JS adds logic and behavior → Platforms like React Native run JS in special environments
```

JavaScript can run in:

* **Browsers** – Chrome (V8), Firefox (SpiderMonkey), Safari (JavaScriptCore).
* **Servers** – Node.js.
* **Cross-platform frameworks** – React Native for mobile apps, Electron for desktop apps.

---

## 🚀 Your First JavaScript

Let’s embed JavaScript into an HTML file:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello JavaScript</title>
  </head>
  <body>
    <script>
      alert('Hello, JavaScript!');
      console.log('Hello, JavaScript!');
    </script>
  </body>
</html>
```

> 💡 You can also test JS live using:
>
> * [JSFiddle](https://jsfiddle.net)
> * [CodePen](https://codepen.io/)
> * [PlayCode.io](https://playcode.io/)

---

## 🧱 Variables & Data Types

JavaScript uses 3 main keywords for declaring variables:

```js
let name = "Ali";     // mutable
const age = 25;       // constant
var city = "Berlin";  // function-scoped (legacy, avoid)
```

### ✅ Data Types

| Type      | Example           |
| --------- | ----------------- |
| string    | `"Hello"`         |
| number    | `42`, `3.14`      |
| boolean   | `true`, `false`   |
| undefined | `let x;`          |
| null      | `let x = null;`   |
| object    | `{ name: "Ali" }` |
| array     | `[1, 2, 3]`       |

---

## ⚙️ Functions & Control Flow

### Functions

```js
function greet(name) {
  return `Hello, ${name}!`;
}

const greetArrow = name => `Hello, ${name}!`;
```

> 💡 In React and React Native, arrow functions are commonly used.

---

### Conditionals

```js
let age = 20;

if (age >= 18) {
  console.log('Adult');
} else {
  console.log('Minor');
}

// Shorthand: Ternary
let status = age >= 18 ? 'Adult' : 'Minor';
```

---

### Loops

```js
// for loop
for (let i = 0; i < 3; i++) {
  console.log(i);
}

// for...of (arrays)
for (let fruit of ['apple', 'banana']) {
  console.log(fruit);
}
```

> JavaScript also supports `while`, `do...while`, and `for...in`.

---

## ⚠️ Common Mistakes

* ❌ Using `=` (assignment) instead of `===` (comparison).
* ❌ Forgetting `let` or `const` leads to global variables.
* ❌ Mixing types: `"5" + 1` is `"51"`, not `6`.

---

## 🔁 JavaScript in React Native

In React Native, you’ll use JavaScript to:

* Build user interfaces using components (`function App() {}`).
* Handle logic and interactivity (hooks, state, events).
* Manage data and fetch from APIs.

We’ll cover these step by step—but it all starts here.

---

## 🧩 What’s Next?

This was a crash course in the JavaScript mindset. To deepen your skills:

* 🏗 Explore [JavaScript.info - The Modern JavaScript Tutorial](https://javascript.info/)
* 👩‍💻 Practice with interactive tools like [JSFiddle](https://jsfiddle.net) or [Codewars](https://www.codewars.com/)
* 💡 Next lessons: **coding problems**, **modern JavaScript (ES6)**, and more.
