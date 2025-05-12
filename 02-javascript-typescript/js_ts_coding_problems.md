# Practice Guide: JavaScript & TypeScript Coding Problems

**Goal:** Strengthen your grasp of modern JavaScript features and TypeScript basics by solving these problems in TypeScript. Each problem tells you which ES6+/TS features to use, and ends with a hint to get you unstuck.

---

## Problem 1: Typed Arrow Function

**Topics:** Arrow functions, type annotations

**Task:**  
In a file `math.ts`, write an arrow function named `multiply` that takes two parameters `a` and `b`—both numbers—and returns their product. Be sure to annotate the parameter types and return type.

```ts
// math.ts

// 1. Define `multiply` here as a typed arrow function.
// 2. Export it as a named export.
```

**Hint:**  
Remember the syntax  
```ts
export const fnName = (param: Type, …): ReturnType => { … }
```

---

## Problem 2: Object & Array Destructuring with Types

**Topics:** Destructuring, interfaces, type annotations

**Task:**  
In `user.ts`, define an interface `User` with properties `id: number`, `name: string`, and `roles: string[]`.  
Then write a function `describeUser` that:

1. Accepts a parameter of type `User`.  
2. Uses object destructuring to pull out `name` and `roles`.  
3. Uses array destructuring to extract the first two roles into `primary` and `secondary`.  
4. Returns a string:  
   `"User <name> has roles: <primary> and <secondary>."`

```ts
// user.ts

// 1. Define interface User { … }

// 2. Implement describeUser(user: User): string { … }

// 3. Export describeUser as default.
```

**Hint:**  
Object vs. array destructuring look like:  
```ts
const { name, roles } = user;
const [primary, secondary] = roles;
```

---

## Problem 3: ES Module Practice

**Topics:** ES modules, default & named exports

**Task:**  
Create two files:

1. **`stringUtils.ts`**  
   - Named-export a function `capitalize(s: string): string` that returns `s` with its first letter uppercased.  

2. **`app.ts`**  
   - Default-export a function `run()` that:  
     - Imports `capitalize` from `stringUtils.ts`.  
     - Calls `capitalize('typescript')` and logs the result to the console.

```ts
// stringUtils.ts
// export function capitalize(…)

// app.ts
// import { capitalize } …
// export default function run() { … }
```

**Hint:**  
- Named exports: `export function name…`  
- Default exports: `export default function…`  
- Import syntax: `import { capitalize } from './stringUtils';`

---

## Problem 4: Promises & Async/Await in TS

**Topics:** Promises, async/await, type annotations

**Task:**  
In `fetcher.ts`, implement two functions:

1. `fakeFetch(url: string): Promise<string>`  
   - Returns a `Promise` that resolves to `"Data from <url>"` after 500 ms.  

2. `async function getData()`  
   - Calls `fakeFetch('/api/test')` using `await`.  
   - Logs the returned string or catches and logs any error.

```ts
// fetcher.ts

// 1. export function fakeFetch(…): Promise<string> { … }

// 2. export async function getData(): Promise<void> { … }
```

**Hint:**  
- Wrap `setTimeout` inside `new Promise((res, rej) => { … })`.  
- Use `await fakeFetch(…)` inside a try/catch in `getData`.

---

## Problem 5: Interface & Class

**Topics:** Interfaces, classes, methods, type annotations

**Task:**  
In `shapes.ts`, do the following:

1. Define an interface `Shape` with a method signature `area(): number`.  
2. Create a class `Rectangle` that implements `Shape`:  
   - Constructor takes `width: number` and `height: number`.  
   - Implements `area()` to return width × height.  
3. Create a class `Circle` that implements `Shape`:  
   - Constructor takes `radius: number`.  
   - Implements `area()` to return π × radius² (use `Math.PI`).  
4. Export both `Rectangle` and `Circle` as named exports.

```ts
// shapes.ts

// interface Shape { area(): number }

// class Rectangle implements Shape { … }

// class Circle implements Shape { … }
```

**Hint:**  
- Class syntax:  
  ```ts
  class Name implements Interface {
    constructor(public x: number) { }
    method(): ReturnType { … }
  }
  ```
- Use `Math.PI` for π.

---

Good luck—these exercises will build a solid foundation for your upcoming React & React Native work!
