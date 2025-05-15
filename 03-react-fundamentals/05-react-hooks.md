# Lesson 5 — Essential React Hooks (for React Native)

**Objective:**

* **Master `useState` and `useEffect`**—including syntax, variations, edge cases, and best practices.
* **Familiarize with advanced hooks** like `useRef`, `useContext`, `useMemo`, and `useCallback`, so you know when and how to reach for them.

> 🧠 You’ve already learned components, props, state, JSX, and styled-components. Hooks now unlock powerful behaviors like dynamic updates and side effects—all with clean functional code.

---

## 1. `useState`: Local State in Functional Components

> 🔧 Manage internal component state that drives UI changes.
> [Docs →](https://react.dev/reference/react/useState)

### Basic Usage

```tsx
import { useState } from 'react';
import { View, Text, Button } from 'react-native';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <View>
      <Text>Count: {count}</Text>
      <Button title="Increment" onPress={() => setCount(count + 1)} />
    </View>
  );
}
```

* `useState(initialValue)` returns `[value, setter]`.
* `setter(newValue)` triggers a re-render with the updated state.
* ✅ TypeScript Tips:

  * `useState(0)` → infers `number`.
  * Explicit types: `useState<number | null>(null)`.

### Functional Updates

Use a function when new state depends on previous:

```tsx
setCount(prev => prev + 1);
```

This avoids stale values in closures—especially useful in effects or async logic.

### Common Patterns

* **Multiple State Variables**

  ```tsx
  const [age, setAge] = useState(30);
  const [name, setName] = useState('Alice');
  ```

* **Updating Object State**

  ```tsx
  const [user, setUser] = useState({ name: '', age: 0 });

  setUser(prev => ({
    ...prev,
    age: prev.age + 1,
  }));
  ```

* ❌ Avoid over-nesting or packing too much into a single state object.

---

## 2. `useEffect`: Side Effects After Render

> ⚙️ Synchronize your component with the outside world—timers, fetch calls, subscriptions, etc.
> [Docs →](https://react.dev/reference/react/useEffect)

### Basic Structure

```tsx
import { useEffect } from 'react';

function Timer() {
  useEffect(() => {
    const id = setInterval(() => {
      console.log('tick');
    }, 1000);

    return () => clearInterval(id); // cleanup
  }, []); // run once on mount

  return <Text>Check console for ticks</Text>;
}
```

* `useEffect(callback, deps?)` runs **after** render.
* Return a function to **clean up** timers, listeners, etc.
* `[]` → run only once (after mount)
* `[value]` → re-run when `value` changes
* `undefined` → run after every render (⚠️ usually avoid)

### Best Practices

* ✅ Include **all variables** used inside the effect in the `deps` array.
* ✅ Always handle **cleanup** if you subscribe or schedule.
* ⚠️ Avoid race conditions and “state update on unmounted component” errors.

### 💡 You Might Not Need an Effect

> Before using `useEffect`, ask: *Can I compute this in render?*

Example:

```tsx
// ❌ Inefficient useEffect
useEffect(() => {
  setFiltered(items.filter(...));
}, [items]);

// ✅ Just compute in render
const filtered = items.filter(...);
```

👉 See: [You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect)

---

## 3. Overview: Other Core Hooks

| Hook            | What It Does                                                                                                          |
| --------------- | --------------------------------------------------------------------------------------------------------------------- |
| `useRef()`      | Store a **mutable reference** (`ref.current`) across renders. Useful for timers or direct access to DOM/native views. |
| `useContext()`  | Access a **global context value** without prop drilling.                                                              |
| `useMemo()`     | **Memoize a computed value**—recomputes only when dependencies change.                                                |
| `useCallback()` | **Memoize a callback function** to avoid unnecessary re-renders or props.                                             |

> ℹ️ These are especially helpful in larger apps or performance-critical areas.

---

## 🧠 Summary

* You now know how to:

  * Manage state with `useState`
  * Run effects and clean them up with `useEffect`
  * Understand dependencies and functional updates
* Other hooks like `useRef`, `useContext`, `useMemo`, and `useCallback` will show up as your apps grow—now you know what they’re for.
