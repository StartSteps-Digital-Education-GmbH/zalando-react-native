# Lesson 1: Introduction to React & Creating Your First React + TypeScript Project

**Objective:**  
1. Understand what React is and its core concepts (components, JSX, props, state, one-way data flow, Virtual DOM).  
2. Scaffold and explore a new React + TypeScript project using Vite.

---

## Part A: What Is React?

### 1.1 React Overview  
- **Library, not Framework**: React is a **JavaScript library** for building user interfaces, maintained by Meta and a large community  ([React Introduction | GeeksforGeeks](https://www.geeksforgeeks.org/reactjs-introduction/?utm_source=chatgpt.com)).  
- **Component-Based**: UI is composed of **components**, self-contained pieces that render markup based on inputs (props) and internal state  ([React Fundamentals - React Native](https://reactnative.dev/docs/intro-react?utm_source=chatgpt.com)).  
- **Declarative**: You describe *what* the UI should look like given certain data; React handles *how* to update the DOM when data changes  ([Getting started with React - Learn web development | MDN](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Frameworks_libraries/React_getting_started?utm_source=chatgpt.com)).  
- **Virtual DOM**: React keeps a lightweight in-memory tree of your UI (“Virtual DOM”) and efficiently computes minimal updates to the real DOM  ([React](https://fr.wikipedia.org/wiki/React?utm_source=chatgpt.com)).  
- **Unidirectional Data Flow**: Data flows down from parent to child via props; state changes trigger re-renders in a predictable way.

### 1.2 Core Concepts

| Concept      | Description |
| ------------ | ----------- |
| **JSX**      | JavaScript syntax extension that looks like HTML. Under the hood it becomes `React.createElement` calls.  ([Introducing JSX - React](https://legacy.reactjs.org/docs/introducing-jsx.html?utm_source=chatgpt.com)) |
| **Component**| A function or class that returns JSX to render. Functional components (functions) are now the norm. |
| **Props**    | Inputs to components, passed as attributes. Immutable within the component. |
| **State**    | Internal, mutable data managed by a component via React Hooks (e.g. `useState`)  ([React Fundamentals - React Native](https://reactnative.dev/docs/intro-react?utm_source=chatgpt.com)). |
| **Hooks**    | Special functions (e.g. `useState`, `useEffect`) to tap into React features inside functional components. |
| **Lifecycle**| Conceptual phases when a component mounts, updates, and unmounts (managed by Hooks in functional components). |

---

## Part B: Scaffolding a React + TypeScript Project with Vite

We’ll use **Vite** to quickly generate a React project preconfigured for TypeScript. Vite gives extremely fast startup and hot-module replacement.

### 2.1 Prerequisites

- **Node.js** ≥ 18 installed  
- A terminal and code editor (e.g. VS Code)

### 2.2 Create the Project

Open your terminal and run:

```bash
# Scaffold a new React + TypeScript project named "my-app"
npm create vite@latest my-app -- --template react-ts
```
- This uses Vite’s `react-ts` template  ([Getting Started - Vite](https://vite.dev/guide/?utm_source=chatgpt.com), [Getting Started - Vite](https://v3.vitejs.dev/guide/?utm_source=chatgpt.com)).  
- When prompted for a framework, “React” and for variant, “TypeScript.”

### 2.3 Install Dependencies

```bash
cd my-app
npm install
```

### 2.4 Inspect the Project Structure

```
my-app/
├─ index.html        # Entry point, Vite serves this directly in dev
├─ package.json      # Scripts & dependencies
├─ tsconfig.json     # TypeScript compiler options
├─ vite.config.ts    # Vite configuration
└─ src/
   ├─ main.tsx       # App bootstrap: renders <App /> into the DOM
   ├─ App.tsx        # Root component
   ├─ index.css      # Global styles
   └─ assets/        # Static assets folder
```

> **Note:** Vite treats `index.html` as the app entry during development, enabling ultra-fast reloads.

### 2.5 Run the Development Server

```bash
npm run dev
```

- Open the URL printed in your terminal (usually `http://localhost:5173/`).  
- Any edits to `src/` will hot-reload instantly in the browser.

---

## Part C: Exploring Your First React Component

Open `src/App.tsx` in your editor:

```tsx
import { useState } from 'react';
import './index.css';

export function App() {
  // React Hook: declare a state variable 'count' initialized to 0
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

### 3.1 Key Points

1. **Importing Hooks**: We import `useState` from the React library.  
2. **Functional Component**: `App` is a function returning JSX.  
3. **State Management**: `useState` provides `[value, setter]`.  
4. **Event Handling**: `onClick` triggers the setter to update state.  
5. **TypeScript**: No extra type annotations needed here—Vite’s TS template configures `jsx: "react-jsx"` in `tsconfig.json` for automatic type inference.

---

## Part D: Next Steps

- **Experiment:** Modify `App.tsx`—add new state variables, more components, and styles.  
- **Learn More React Concepts:**  
  - Rendering lists with `.map()` and keys  
  - Conditional rendering  
  - Passing props to child components  
- **Preview in TypeScript:** Notice IDE autocompletion and type-checking for props, state, and event handlers.

---

### References

1. **Quick Start – React**  ([Quick Start - React](https://react.dev/learn?utm_source=chatgpt.com))  
2. **React Fundamentals**  ([React Fundamentals - React Native](https://reactnative.dev/docs/intro-react?utm_source=chatgpt.com))  
3. **Getting started with React** – MDN  ([Getting started with React - Learn web development | MDN](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Frameworks_libraries/React_getting_started?utm_source=chatgpt.com))  
4. **Vite Guide**  ([Getting Started - Vite](https://vite.dev/guide/?utm_source=chatgpt.com), [Getting Started - Vite](https://v3.vitejs.dev/guide/?utm_source=chatgpt.com))  
5. **Introducing JSX**  ([Introducing JSX - React](https://legacy.reactjs.org/docs/introducing-jsx.html?utm_source=chatgpt.com))  
6. **React Introduction** – GeeksforGeeks  ([React Introduction | GeeksforGeeks](https://www.geeksforgeeks.org/reactjs-introduction/?utm_source=chatgpt.com))  

---