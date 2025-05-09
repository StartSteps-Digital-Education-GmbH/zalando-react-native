# JavaScript Practice Exercises

These exercises will help you practice the modern JavaScript concepts covered in the theory session.

## Exercise 1: Arrow Functions

Convert the following functions to arrow functions:

```javascript
// Original
function multiply(a, b) {
  return a * b;
}

function greet(name) {
  return "Hello, " + name + "!";
}

// Your solution here
```

## Exercise 2: Destructuring

Given the following data structures, use destructuring to extract values:

```javascript
const person = {
  name: 'John',
  age: 30,
  address: {
    city: 'New York',
    country: 'USA'
  }
};

const numbers = [1, 2, 3, 4, 5];

// Extract name and age from person
// Extract first and second numbers from the array
```

## Exercise 3: Promises

Create a function that returns a promise which:
1. Resolves after 2 seconds with a success message
2. Rejects if a random number is less than 0.5

```javascript
function delayedPromise() {
  // Your solution here
}
```

## Exercise 4: Async/Await

Create an async function that:
1. Fetches data from https://jsonplaceholder.typicode.com/todos/1
2. Logs the response
3. Handles any errors

```javascript
async function fetchTodo() {
  // Your solution here
}
```

## Exercise 5: Modules

Create two files:
1. `utils.js` - Export utility functions
2. `main.js` - Import and use the utility functions

```javascript
// utils.js
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

// main.js
// Import and use the functions
```

## Solutions

Try to solve the exercises on your own first. Solutions will be provided later.

## Additional Practice

For more practice, try:
1. Converting callback-based code to promises
2. Using destructuring in function parameters
3. Creating a module with multiple exports
4. Handling multiple promises with Promise.all 