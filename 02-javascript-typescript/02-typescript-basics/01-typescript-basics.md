# 📘 TypeScript Basics

TypeScript adds static typing to JavaScript, helping you catch bugs early and write more predictable, scalable React Native apps.

---

## 🧠 Why Use TypeScript?

* **Type safety**: Detect errors before runtime
* **Better tooling**: Get autocompletion, inline docs, and refactoring
* **Improved collaboration**: Know what functions/components expect
* **Common in React Native projects**: Increasingly used in professional codebases

---

## 📝 Type Annotations

Define the type of a variable or parameter using a colon `:`.

```ts
// Basic types
let name: string = 'John';
let age: number = 30;
let isActive: boolean = true;

// Arrays
let numbers: number[] = [1, 2, 3];
let names: string[] = ['John', 'Jane'];

// Avoid using `any` unless absolutely necessary
let anything: any = 'can be anything'; // ❌ disables type safety
```

---

## 🧩 Interfaces

Interfaces define the shape of an object. Ideal for defining props or data models.

```ts
interface Person {
  name: string;
  age: number;
  address?: string; // optional
}

const person: Person = {
  name: 'John',
  age: 30,
};
```

### ✅ Example in a React Native component

```tsx
interface GreetingProps {
  name: string;
  age: number;
}

function Greeting({ name, age }: GreetingProps) {
  return <Text>Hello {name}, you are {age} years old.</Text>;
}
```

---

## 🏷️ Type Aliases

Type aliases can be used for objects, primitives, or unions.

```ts
type Point = {
  x: number;
  y: number;
};

let point: Point = { x: 10, y: 20 };
```

> 🆚 Use `interface` for objects and props, `type` for unions or primitives.

---

## 💡 Type Inference

TypeScript can often figure out types for you.

```ts
let count = 5; // inferred as number

function greet(name: string) {
  return `Hello, ${name}`; // inferred as string
}
```

---

## 🧪 Union & Intersection Types

```ts
// Union type
type Status = 'active' | 'inactive' | 'pending';

let currentStatus: Status = 'active';

// Intersection type
type Employee = Person & {
  employeeId: number;
  department: string;
};
```

---

## 🧱 Classes

TypeScript supports object-oriented features with type safety.

```ts
class Animal {
  private name: string;

  constructor(name: string) {
    this.name = name;
  }

  public getName(): string {
    return this.name;
  }
}

const dog = new Animal('Rex');
```

---

## 🔁 Generics

Write reusable, type-safe functions and components.

```ts
function identity<T>(arg: T): T {
  return arg;
}

let result = identity<string>('hello'); // type is string
```

Another example:

```ts
function wrapInArray<T>(value: T): T[] {
  return [value];
}

const numbers = wrapInArray(10); // number[]
```

---

## ✅ Best Practices

1. ✅ Always type function parameters and return values
2. ✅ Use `interface` for props and data objects
3. ✅ Use `type` for unions and more complex types
4. ✅ Leverage inference when possible
5. ✅ Avoid `any`—use `unknown` if needed

---

## ⚠️ Common Pitfalls

* ❌ Overusing `any`—leads to runtime bugs
* ❌ Forgetting to type function parameters
* ❌ Not handling optional properties
* ❌ Misusing union types without type guards

---

## 🧰 Tooling Tip

Use **VSCode** or similar editors with TypeScript support for autocomplete, in-line errors, and better navigation.

---

## 🚀 What's Next?

Try converting a small React Native component to TypeScript!

👉 Head to:
**[Practice: TypeScript Conversion](./practice-session/01-typescript-conversion.md)**

