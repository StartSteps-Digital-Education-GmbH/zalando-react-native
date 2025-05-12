# Practice Guide 2: Logical JavaScript & TypeScript Challenges

**Languages Allowed:** JavaScript or TypeScript  
**Skills Covered:** Conditions, loops, arrays, string manipulation, recursion, and problem-solving logic  
**Instructions:**  
- Solve each challenge in its own file (`.js` or `.ts`).  
- Write clean, well-commented code.  
- For TypeScript solutions, add appropriate type annotations.  
- Test your code with a variety of inputs.  
- Optional: submit solutions on platforms like HackerRank or LeetCode (links provided).

---

## Challenge 1: Palindrome Validator

**Description:**  
Write a function `isPalindrome(input)` that returns `true` if `input` (a string) reads the same backward as forward when you ignore non-alphanumeric characters and case; otherwise return `false`.

```js
// e.g. isPalindrome("A man, a plan, a canal: Panama") → true
//      isPalindrome("Hello")                            → false
```

**Hint:**  
- Strip out everything except letters/numbers (`char.match(/[a-z0-9]/i)`)  
- Use two pointers (start/end) to compare characters  

**Further Practice:**  
- LeetCode “Valid Palindrome”:  
  https://leetcode.com/problems/valid-palindrome/  

---

## Challenge 2: Runner-Up Score

**Description:**  
Given an array of numbers, return the **second largest** unique value. If there is no runner-up, return `null`.

```js
// e.g. runnerUp([2, 3, 6, 6, 5]) → 5
//      runnerUp([10, 10, 10])   → null
```

**Hint:**  
- Use a `Set` or filter to dedupe the array  
- Sort or scan to find the maximum and second maximum  

**Further Practice:**  
- HackerRank “Runner-Up Score”:  
  https://www.hackerrank.com/challenges/find-second-maximum-number-in-a-list  

---

## Challenge 3: Deep Array Flatten

**Description:**  
Implement `flatten(arr)` that takes an array which may contain nested sub-arrays of arbitrary depth and returns a new flat array.

```js
// e.g. flatten([1, [2, [3, 4], 5], 6]) → [1, 2, 3, 4, 5, 6]
```

**Hint:**  
- Use recursion: if an element is an array, recurse; otherwise `push`  
- In JS: `Array.isArray(item)` to detect arrays  

**Further Practice:**  
- Codewars “Flatten” Kata:  
  https://www.codewars.com/kata/5250a89b1625e5decd000413  

---

## Challenge 4: Balanced Brackets

**Description:**  
Write `isBalanced(s)` that returns `true` if string `s` of brackets—`()`, `[]`, `{}`—is properly balanced and nested, else `false`.

```js
// e.g. isBalanced("({[]})") → true
//      isBalanced("([)]")   → false
```

**Hint:**  
- Use a **stack**: push opening brackets, pop and check matching closing bracket  
- Map closing → opening types for quick lookup  

**Further Practice:**  
- HackerRank “Balanced Brackets”:  
  https://www.hackerrank.com/challenges/balanced-brackets  

---

## Challenge 5: Longest Non-Repeating Substring

**Description:**  
Implement `lengthOfLongestSubstring(s)` that returns the length of the longest substring without repeating characters.

```js
// e.g. lengthOfLongestSubstring("abcabcbb") → 3  ("abc")
//      lengthOfLongestSubstring("bbbbb")    → 1  ("b")
```

**Hint:**  
- Use a **sliding window** with two indices and a `Set` or map to track seen chars  
- Expand end pointer, shrink start pointer when you hit a duplicate  

**Further Practice:**  
- LeetCode “Longest Substring Without Repeating Characters”:  
  https://leetcode.com/problems/longest-substring-without-repeating-characters/  

---

## Checklist

- [ ] Each solution runs without errors in Node.js (or via `ts-node` for TypeScript).  
- [ ] TypeScript files compile cleanly (`tsc --noEmit`).

Good luck—and happy coding! 
