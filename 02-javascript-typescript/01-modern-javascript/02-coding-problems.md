# Guide 2: Learning JavaScript by Solving Coding Problems

In this guide, we’ll solve a series of classic JavaScript problems using only the basics Each problem includes:

1. **Problem Description**  
2. **Step-by-Step Solution**  
3. **Code Example**  
4. **Key Takeaways**

---

## Problem 1: Reverse a String

**Description:**  
Write a function `reverseString(str)` that takes a string `str` and returns a new string with its characters in reverse order.

### Solution Steps

1. Split the string into an array of characters (using a simple loop or `split('')`).  
2. Reverse the array by swapping elements.  
3. Reassemble into a string.

### Code Example

```js
/**
 * Reverse a string without using .reverse()
 * @param {string} str
 * @returns {string}
 */
function reverseString(str) {
  // Convert string to array
  var arr = str.split('');  

  // Reverse the array in place
  var left = 0;
  var right = arr.length - 1;
  while (left < right) {
    var temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;
    left++;
    right--;
  }

  // Join back into a string
  return arr.join('');
}

// Test
console.log(reverseString('hello')); // 'olleh'
```

**Key Takeaways:**  
- String → array via `.split('')`  
- Manual array reversal via a two-pointer swap  
- Array → string via `.join('')`

---

## Problem 2: Sum All Numbers in an Array

**Description:**  
Write a function `sumArray(nums)` that returns the sum of all numeric elements in an array.

### Solution Steps

1. Initialize a running total to `0`.  
2. Loop through the array, adding each element to the total.  
3. Return the total.

### Code Example

```js
/**
 * Sum all numbers in an array using a simple loop
 * @param {number[]} nums
 * @returns {number}
 */
function sumArray(nums) {
  var total = 0;
  for (var i = 0; i < nums.length; i++) {
    total += nums[i];
  }
  return total;
}

// Test
console.log(sumArray([1, 2, 3, 4])); // 10
```

**Key Takeaways:**  
- Use a `for` loop to iterate over array elements  
- Accumulate values in a variable

---

## Problem 3: Remove Duplicates from an Array

**Description:**  
Write `uniqueValues(arr)` that returns a new array containing only the unique elements of `arr`, preserving their first occurrence order.

### Solution Steps

1. Create an empty array `result`.  
2. For each element in `arr`, check if it’s already in `result` via `indexOf`.  
3. If not present, `push` it into `result`.  
4. Return `result`.

### Code Example

```js
/**
 * Get unique values from an array without using Set
 * @param {any[]} arr
 * @returns {any[]}
 */
function uniqueValues(arr) {
  var result = [];
  for (var i = 0; i < arr.length; i++) {
    var item = arr[i];
    if (result.indexOf(item) === -1) {
      result.push(item);
    }
  }
  return result;
}

// Test
console.log(uniqueValues([1, 2, 2, 3, 3, 4])); // [1, 2, 3, 4]
```

**Key Takeaways:**  
- Check presence with `indexOf`  
- Build a new array using `push`

---

## Problem 4: FizzBuzz

**Description:**  
Print numbers 1 to 20. For multiples of 3, print `"Fizz"`; for multiples of 5, print `"Buzz"`; for multiples of both, print `"FizzBuzz"`; otherwise print the number.

### Code Example

```js
for (var i = 1; i <= 20; i++) {
  var output = '';

  if (i % 3 === 0) {
    output += 'Fizz';
  }
  if (i % 5 === 0) {
    output += 'Buzz';
  }

  // If output is still empty, fall back to the number
  if (output === '') {
    output = i;
  }

  console.log(output);
}
```

**Key Takeaways:**  
- Use the modulo operator (`%`) for divisibility checks  
- Build strings conditionally, with a fallback to the number

---

## Next Steps

In the next lesson we’ll cover **ES6+ features** (arrow functions, destructuring, modules, Promises, and `async`/`await`) and rewrite these solutions using the more modern syntax. Then we’ll introduce **TypeScript** to add type safety on top of these patterns.
