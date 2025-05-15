# Lesson 4 — StyleX (stylexjs) Guide 🧩

> **Audience:** Engineers in the Zalando React Native Learning Program

> **Prerequisites:** React & JSX basics, CSS/styled-components familiarity

> **Goal:** Learn how to use `stylex` for scalable, performant, and type-safe styles in Zalando apps.

---

## 🧠 What is StyleX?

**StyleX** is a fast, atomic CSS-in-JS library developed by Meta (Facebook) and used by Zalando in conjunction with [`react-strict-dom`](https://github.com/zalandosei/react-strict-dom). It brings:

* ⚡ **Atomic CSS** at compile time — small, reusable style classes
* ✅ **Type safety** & autocompletion
* 📦 **No runtime style merging**
* 💅 Full compatibility with Zalando's design tokens & cross-platform styling

---

## 🚀 React-Strict-DOM Uses StyleX

Zalando uses `react-strict-dom` across its codebase to unify styling for web and mobile. Under the hood, it’s wired to **StyleX**.

```ts
import { html } from 'react-strict-dom';
```

Use `html.div`, `html.span`, etc. — not regular HTML tags or `View`, `Text` if you are coding in React.

---

## 🧪 Example: Basic Styled Card

```tsx
import { html } from 'react-strict-dom';
import * as stylex from '@stylexjs/stylex';

const styles = stylex.create({
  card: {
    backgroundColor: '#fff',
    padding: 16,
    borderRadius: 8,
    boxShadow: '0 1px 3px rgba(0,0,0,0.1)',
  },
  title: {
    fontSize: 18,
    fontWeight: 'bold',
    color: '#333',
  },
});

export function Card() {
  return html.div(
    stylex.props(styles.card),
    html.span(stylex.props(styles.title), 'Welcome to StyleX!')
  );
}
```

---

## 🔧 How to Use StyleX

### 1. Define Styles

```ts
const styles = stylex.create({
  box: {
    padding: 16,
    backgroundColor: '#eee',
    borderRadius: 6,
  },
});
```

### 2. Apply Styles with `stylex.props()`

```tsx
html.div(stylex.props(styles.box), 'Content here')
```

> 🧠 You should use `stylex.props()` — if `style={{ ... }}` was **not supported**.

---

## 🎯 Best Practices

### ✅ Conditional Styles

```ts
const styles = stylex.create({
  base: {
    padding: 16,
    borderRadius: 8,
  },
  selected: {
    backgroundColor: 'blue',
  },
  unselected: {
    backgroundColor: 'gray',
  },
});

const button = isSelected
  ? [styles.base, styles.selected]
  : [styles.base, styles.unselected];

html.div(stylex.props(...button), 'Selectable Box');
```

---

### ❌ Avoid Inline Dynamic Styles

```tsx
// ❌ DON'T DO THIS
html.div({ style: { padding: someValue } });
```

Instead:

```ts
const styles = stylex.create({
  small: { padding: 8 },
  large: { padding: 24 },
});
```

```tsx
html.div(stylex.props(isLarge ? styles.large : styles.small));
```

---

## 🎨 Design Tokens in Real Apps

In Zalando codebases, StyleX works hand-in-hand with **design tokens** for consistent theming:

```ts
const styles = stylex.create({
  title: {
    fontSize: tokens.typography.heading.md,
    color: tokens.color.text.primary,
    marginBottom: tokens.spacing.md,
  },
});
```

These are available via internal libraries and will be introduced later in the course.

---

## 🛠️ Debugging Tips

| ✅ Do                     | 🚫 Avoid                    |
| ------------------------ | --------------------------- |
| Use `html.div` etc.      | Don't use raw `div`/`span`  |
| Use pre-defined variants | Avoid inline dynamic values |

Use **React DevTools** to inspect which atomic styles are applied (you'll see classnames like `x1y2z3a`).

---

## 🏁 Summary

| Feature             | How StyleX Handles It                         |
| ------------------- | --------------------------------------------- |
| Style declaration   | `stylex.create({ ... })`                      |
| Style application   | `stylex.props(...styles)`                     |
| Conditional styling | Use conditionally chosen variants             |
| Compatibility       | Works with `react-strict-dom` + design tokens |
| Performance         | Atomic CSS with compile-time safety           |

---

## ✅ Optional Practice Task

> Create a `Button` component with the following:

* Base styling for padding, border-radius
* `primary` and `secondary` color variants
* A `disabled` state that dims the button

Use `html.button` with `stylex.props()`.

