# TypeScript Conversion Practice

These exercises will help you practice converting JavaScript code to TypeScript.

## Exercise 1: Basic Type Annotations

Convert the following JavaScript code to TypeScript by adding appropriate type annotations:

```typescript
// Original JavaScript
function calculateTotal(items) {
  return items.reduce((total, item) => total + item.price, 0);
}

const items = [
  { name: 'Book', price: 20 },
  { name: 'Pen', price: 5 }
];

// Your TypeScript solution here
```

## Exercise 2: Interface Creation

Create an interface for the following object and use it to type the function:

```typescript
// Original JavaScript
function processUser(user) {
  console.log(`Processing ${user.name} (${user.age} years old)`);
  if (user.email) {
    console.log(`Contact: ${user.email}`);
  }
}

// Your TypeScript solution here
```

## Exercise 3: Class Conversion

Convert the following JavaScript class to TypeScript:

```typescript
// Original JavaScript
class Vehicle {
  constructor(make, model, year) {
    this.make = make;
    this.model = model;
    this.year = year;
  }

  getInfo() {
    return `${this.year} ${this.make} ${this.model}`;
  }
}

// Your TypeScript solution here
```

## Exercise 4: Generic Function

Create a generic function that can work with different types of arrays:

```typescript
// Create a function that takes an array of any type
// and returns a new array with the first and last elements swapped
function swapFirstAndLast<T>(arr: T[]): T[] {
  // Your solution here
}
```

## Exercise 5: Union Types

Create a function that handles different types of input:

```typescript
// Create a function that accepts either a string or a number
// and returns a formatted string
function formatInput(input: string | number): string {
  // Your solution here
}
```

## Exercise 6: Type Guards

Implement type guards for the following function:

```typescript
interface Circle {
  kind: 'circle';
  radius: number;
}

interface Square {
  kind: 'square';
  sideLength: number;
}

type Shape = Circle | Square;

function getArea(shape: Shape): number {
  // Your solution here
}
```

## Solutions

Try to solve the exercises on your own first. Solutions will be provided at the end of the session.

## Additional Practice

For more practice, try:
1. Converting a larger JavaScript file to TypeScript
2. Creating interfaces for complex data structures
3. Implementing type-safe API response handling