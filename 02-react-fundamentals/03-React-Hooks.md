# Guide 3: Essential React Hooks for React Native

**Objective:**  
- Master `useState` and `useEffect`—their syntax, variations, edge cases, and best practices—for building robust React Native components.  
- Get a quick refresher on other key Hooks (`useRef`, `useContext`, `useMemo`, `useCallback`) to know when to reach for them.

---

## 1. The `useState` Hook

> Declare and manage local state in functional components.  ([useState - React](https://react.dev/reference/react/useState?utm_source=chatgpt.com))

### 1.1 Basic Usage

```tsx
import { useState } from 'react';

function Counter() {
  // count: number, setCount: React.Dispatch<React.SetStateAction<number>>
  const [count, setCount] = useState(0);

  return (
    <View>
      <Text>Count: {count}</Text>
      <Button title="Increment" onPress={() => setCount(count + 1)} />
    </View>
  );
}
```

- `useState(initial)` returns `[value, setter]`.  
- Calling `setter(newValue)` schedules a re-render with the updated state.  
- **TypeScript Tip:**  
  - Let TS infer: `useState(0)` infers `number`.  
  - Or explicitly: `useState<number | null>(null)`.

### 1.2 Functional Updates

When new state depends on previous:

```tsx
setCount(prevCount => prevCount + 1);
```

### 1.3 Edge Cases & Best Practices

- **Multiple State Variables:**  
  ```tsx
  const [age, setAge] = useState(30);
  const [name, setName] = useState('Alice');
  ```
- **Merging State:**  
  - `useState` **replaces** the complete state.  
  - For objects, spread manually:  
    ```tsx
    const [user, setUser] = useState({name:'', age:0});
    setUser(prev => ({...prev, age: prev.age + 1}));
    ```
- **Avoid Over-nesting:**  
  - Keep each piece of state as focused as possible.

---

## 2. The `useEffect` Hook

> Synchronize with external systems (data fetching, subscriptions, DOM) after renders.  ([useEffect - React](https://react.dev/reference/react/useEffect?utm_source=chatgpt.com))

### 2.1 Basic Usage & Dependencies

```tsx
import { useEffect } from 'react';

function Timer() {
  useEffect(() => {
    const id = setInterval(() => {
      console.log('tick');
    }, 1000);

    return () => clearInterval(id); // cleanup on unmount
  }, []); // empty array → run once after mount

  return <Text>Check console for ticks</Text>;
}
```

- **`effect` callback** runs **after** render.  
- **Cleanup**: return a function to dispose subscriptions/timers.  
- **Dependencies array** (`deps`):  
  - `[]` → run once on mount  
  - `[dep1, dep2]` → re-run when any dep changes  
  - Omit → run **after every** render (rarely desired)  ([6 use cases of the useEffect ReactJS hook - DEV Community](https://dev.to/colocodes/6-use-cases-of-the-useeffect-reactjs-hook-282o?utm_source=chatgpt.com))


- Always handle **cleanup** to avoid setting state on unmounted components.  
- Include all variables from outside scope that the effect uses in the deps array.

- **“You Might Not Need an Effect”**: Sometimes you can compute values directly in render instead of using an effect  ([You Might Not Need an Effect - React](https://react.dev/learn/you-might-not-need-an-effect?utm_source=chatgpt.com)).

---

## 3. Quick Overviews: Other Useful Hooks

| Hook         | Purpose                                                  |
| ------------ | -------------------------------------------------------- |
| **useRef**   | Persist a mutable value (`ref.current`) across renders without re-rendering; access native views . |
| **useContext**| Consume React Context, avoiding prop drilling . |
| **useMemo**  | Memoize expensive computations; recompute only when deps change . |
| **useCallback** | Memoize callback functions; keep function identity stable between renders . |

---

### Summary & Next Steps

- You now have a deep understanding of **useState** and **useEffect**—use them to manage state and synchronize with external systems in your React Native components.  
- Remember to handle cleanup, specify correct dependencies, and use functional updates to avoid stale state.  
- Explore **useRef**, **useContext**, **useMemo**, and **useCallback** as needed to optimize and structure your components.  
- In the practical session, you’ll implement components with timers, data fetchers, and complex state logic to cement these Hooks in action. 
