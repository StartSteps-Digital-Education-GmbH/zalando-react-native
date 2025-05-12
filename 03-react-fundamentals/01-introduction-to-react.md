# 01 - Introduction to React & Creating Your First React + TypeScript Project

**Objective:**

1. Understand the core ideas behind React (components, JSX, props, state, Virtual DOM, unidirectional data flow).
2. Set up and explore a new React + TypeScript project using [Vite](https://vite.dev/).

> **Why this matters:** React Native builds on core React concepts. Mastering React fundamentals will help you write clean, scalable components in React Native.

---

## Part A: What Is React?

### 1.1 React Overview

* **Library, not Framework**: React is a **JavaScript library** for building user interfaces, developed by Meta.
* **Component-Based**: UIs are built from **components**—reusable pieces of code that describe how parts of the UI should look and behave.
* **Declarative**: You describe *what* the UI should look like; React handles *how* to update it.
* **Virtual DOM**: React maintains a lightweight in-memory representation of the DOM and syncs it efficiently with the browser DOM.
* **Unidirectional Data Flow**: Data flows from parent to child. Updates to state trigger re-renders in a predictable, controlled way.

---

## Part B: Core React Concepts

| Concept       | Description                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------ |
| **JSX**       | A syntax extension that lets you write HTML-like code in JavaScript. Compiled to `React.createElement(...)`. |
| **Component** | A function (or class) that returns JSX. Functional components are now the standard.                          |
| **Props**     | Data passed to a component, similar to function arguments. Props are read-only.                              |
| **State**     | Local, reactive data that lives inside a component. State is mutable and causes re-renders.                  |
| **Hooks**     | Functions like `useState`, `useEffect` let you use React features in functional components.                  |
| **Lifecycle** | Components go through lifecycle phases: mount, update, unmount. Managed with hooks in function components.   |

> Learn more: [React Fundamentals - React Native Docs](https://reactnative.dev/docs/intro-react)

---

## Part C: Scaffold a React + TypeScript Project with Vite

We’ll use **Vite** to bootstrap a fast, lightweight React project with TypeScript. Vite provides blazing-fast dev server and HMR.

### 3.1 Prerequisites

* Node.js 18+ installed
* Terminal + VS Code (or any editor)

### 3.2 Create the Project

```bash
npm create vite@latest my-app -- --template react-ts
```

Choose:

* **Framework**: React
* **Variant**: TypeScript

Then:

```bash
cd my-app
npm install
```

### 3.3 File Structure Overview

```
my-app/
├─ index.html         # Vite uses this as the dev entry point
├─ package.json       # Project metadata and scripts
├─ tsconfig.json      # TypeScript config
├─ vite.config.ts     # Vite config
└─ src/
   ├─ main.tsx        # App entry point
   ├─ App.tsx         # Root component
   ├─ index.css       # Global styles
   └─ assets/         # Static files
```

> ⚡ `index.html` is directly served during development—no need for a full build to preview changes.

### 3.4 Run the Dev Server

```bash
npm run dev
```

* Visit `http://localhost:5173/` (or the URL shown in your terminal).
* Try editing `App.tsx` and see it hot reload instantly.

---

## Part D: Your First React Component

Open `src/App.tsx`:

```tsx
import { useState } from 'react';
import './index.css';

export function App() {
  const [count, setCount] = useState(0);

  return (
    <div className="app">
      <h1>Hello, React + TypeScript!</h1>
      <p>Current count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}

export default App;
```

### What’s Happening?

| Feature             | Description                                                                           |
| ------------------- | ------------------------------------------------------------------------------------- |
| `useState(0)`       | Initializes a `count` variable with value `0` and a `setCount` function to update it. |
| `onClick`           | When the button is clicked, `count` is incremented.                                   |
| JSX                 | Looks like HTML but is actually compiled JavaScript.                                  |
| Automatic Inference | TypeScript infers types automatically from hooks and JSX.                             |

---

## Part E: Try It Yourself

* Modify the JSX: Add more text, buttons, or images.
* Add a new state variable: Try managing input text.
* Notice TypeScript features: Autocompletion and inline errors are already working.

---

## References

* [React Fundamentals – React Native Docs](https://reactnative.dev/docs/intro-react)
* [Quick Start – React](https://react.dev/learn)
* [JSX – React Docs](https://legacy.reactjs.org/docs/introducing-jsx.html)
* [Getting Started – Vite](https://vite.dev/guide/)
* [React Introduction – MDN](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Frameworks_libraries/React_getting_started)
* [React Overview – GeeksforGeeks](https://www.geeksforgeeks.org/reactjs-introduction/)

---
