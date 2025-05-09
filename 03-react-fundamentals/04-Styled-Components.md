# Lesson 4: Styled Components

## What Is Styled-Components & Why Use It?

**Styled-components** is a library that lets you write CSS inside your JavaScript or TypeScript files when building React apps. Instead of using separate `.css` files or class names, you define styles alongside your components using a special syntax. Each styled component becomes a regular React component with scoped styles, improving maintainability and reducing conflicts.

It automatically generates unique class names for every component, so styles don’t clash. It also supports **theming**, letting you define a centralized set of design tokens (colors, spacing, typography) and reuse them across your app.

> ✅ **Note:** While this guide focuses on using styled-components with **React for web**, the same library also works with **React Native** using a slightly different setup and native elements like `View`, `Text`, and `TouchableOpacity`.

---

## 1. Installation & Setup

```bash
npm install styled-components
# (Optional, for TypeScript projects)
npm install --save-dev @types/styled-components
```

---

## 2. Creating Basic Styled Components

Wrap any HTML element with `styled` to create a styled component:

```tsx
import styled from 'styled-components';

const Button = styled.button`
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
`;
```

```tsx
function App() {
  return <Button>Click Me</Button>;
}
```

> 🎯 **Why this is useful**:
>
> * Only styles used by rendered components are injected (no unused CSS).
> * Unique class names prevent collisions in large apps.

---

## 3. Dynamic Styling with Props

You can pass props to your styled components and use them in your styles:

```tsx
interface ButtonProps {
  primary?: boolean;
}

const Button = styled.button<ButtonProps>`
  background: ${props => (props.primary ? '#BF4F74' : 'white')};
  color:     ${props => (props.primary ? 'white'    : '#BF4F74')};
  border:    2px solid #BF4F74;
  padding:   0.5em 1em;
  border-radius: 3px;
`;
```

```tsx
<Button>Normal</Button>
<Button primary>Primary</Button>
```

---

## 4. Theming

Use `ThemeProvider` to define a theme and make it accessible to all components:

```tsx
// theme.ts
export const theme = {
  colors: { primary: '#007bff', secondary: '#6c757d' },
  spacing: (n: number) => `${8 * n}px`,
};
```

```tsx
// App.tsx
import { ThemeProvider } from 'styled-components';
import { theme } from './theme';

<ThemeProvider theme={theme}>
  <App />
</ThemeProvider>;
```

```tsx
const Heading = styled.h1`
  color: ${({ theme }) => theme.colors.primary};
  margin-bottom: ${({ theme }) => theme.spacing(2)};
`;
```

> 🎨 **Benefits**:
>
> * Centralized tokens for colors, spacing, and typography.
> * Easy theme switching for light/dark modes or brand customization.

---

## 5. Global Styles & Reusable Fragments

### 5.1 Global Styles

```tsx
import { createGlobalStyle } from 'styled-components';

const GlobalStyle = createGlobalStyle`
  body {
    margin: 0;
    font-family: sans-serif;
    background: #f8f9fa;
  }
`;
```

```tsx
function App() {
  return (
    <>
      <GlobalStyle />
      {/* rest of app */}
    </>
  );
}
```

> 💡 **Tip:** Global styles are only supported in React DOM, not React Native. For React Native, reuse base components instead of global rules.

---

### 5.2 CSS Helper Fragments

You can use the `css` helper to define reusable style blocks:

```tsx
import { css } from 'styled-components';

const cardStyles = css`
  padding: 16px;
  border: 1px solid #ddd;
  border-radius: 8px;
`;

const Card = styled.div`
  ${cardStyles}
  background: white;
`;
```

> ♻️ Promotes **DRY** code: share common styles across components.

---

## 6. Extending & Polymorphic Components

### 6.1 Extending Styles

```tsx
const PrimaryButton = styled(Button)`
  background-color: ${({ theme }) => theme.colors.primary};
  color: white;
`;
```

> ➕ Build new style variants by extending existing components.

---

### 6.2 Polymorphic `as` Prop

```tsx
<Button as="a" href="/login">
  Login Link
</Button>
```

> 🔁 Renders a styled component as another HTML tag.

---

## 7. Best Practices

* **Co-locate logic and styles**: Keep related code in one file.
* **Use themes instead of hard-coded values**: Improves consistency and flexibility.
* **Create small, reusable components**: Focus on one responsibility.
* **Use TypeScript for dynamic props**: Ensures style safety.

---

## 8. React vs React Native: Styled Components Comparison

| Feature           | React DOM (Web)        | React Native (Mobile)                     |
| ----------------- | ---------------------- | ----------------------------------------- |
| Component tags    | `styled.div`, `button` | `styled.View`, `Text`, `TouchableOpacity` |
| Style syntax      | CSS-in-JS (true CSS)   | CSS-like but compiles to JS styles        |
| Global styles     | ✅ `createGlobalStyle`  | ❌ Not supported                           |
| Theming support   | ✅ via `ThemeProvider`  | ✅ via `ThemeProvider`                     |
| Browser fallbacks | ✅ Yes                  | ❌ Not needed (uses native styling)        |

> 🧭 **Note:** You’ll dive deeper into React Native styling with styled-components in upcoming lessons.
