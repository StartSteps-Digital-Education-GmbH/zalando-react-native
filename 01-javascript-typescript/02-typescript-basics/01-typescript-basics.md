# TypeScript Basics

This section covers the fundamental TypeScript concepts needed for React Native development.

## Type Annotations

TypeScript adds static typing to JavaScript. Here's how to use type annotations:

```typescript
// Basic types
let name: string = 'John';
let age: number = 30;
let isActive: boolean = true;

// Arrays
let numbers: number[] = [1, 2, 3];
let names: string[] = ['John', 'Jane'];

// Any type (only use if nessessary)
let anything: any = 'can be anything';
```

## Interfaces

Interfaces define the structure of objects:

```typescript
interface Person {
  name: string;
  age: number;
  address?: string; // Optional property
}

const person: Person = {
  name: 'John',
  age: 30
};
```

## Classes

TypeScript classes support access modifiers and type checking:

```typescript
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

## Type Inference

TypeScript can often infer types without explicit annotations:

```typescript
// TypeScript infers the type as number
let count = 5;

// TypeScript infers the return type as string
function greet(name: string) {
  return `Hello, ${name}`;
}
```

## Generics

Generics allow for reusable type-safe code:

```typescript
function identity<T>(arg: T): T {
  return arg;
}

let result = identity<string>('hello');
```

## Type Aliases

Type aliases create new names for types:

```typescript
type Point = {
  x: number;
  y: number;
};

let point: Point = { x: 10, y: 20 };
```

## Union and Intersection Types

```typescript
// Union type
type Status = 'active' | 'inactive' | 'pending';

// Intersection type
type Employee = Person & {
  employeeId: number;
  department: string;
};
```

## Best Practices

1. Use explicit types for function parameters and return values
2. Leverage type inference for simple variables
3. Use interfaces for object shapes
4. Prefer type aliases for complex types
5. Use generics for reusable components

## Common Pitfalls

1. Using `any` too liberally
2. Not handling optional properties properly
3. Forgetting to type function parameters
4. Not using type guards with union types

## Next Steps

Proceed to the practice sessions:
- [TypeScript Conversion](./practice-session/01-typescript-conversion.md)