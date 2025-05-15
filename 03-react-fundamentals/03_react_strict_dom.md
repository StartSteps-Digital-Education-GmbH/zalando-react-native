# Lesson 3: React Strict DOM (RSD)

## Overview

React Strict DOM (RSD) is a library that provides a unified, cross-platform API for building user interfaces with a constrained set of HTML elements and CSS properties. By enforcing a strict subset of web and native primitives, RSD ensures type safety, design-system consistency, and smoother migration between web and native apps. Developers write familiar JSX and React paradigms—components, props, state, and hooks—while rendering through RSD’s `html` and `css` modules instead of raw DOM or React Native primitives.

---

## 1. Introduction to RSD

RSD defines a well-known subset of the DOM and styling APIs, exposing type-safe `html` elements and a CSS-in-JS system (`css.create`). This approach:

* **Typesafe Components**: Only cross-platform-compatible elements and attributes are allowed.
* **Design-System Alignment**: Styles are scoped and validated against a defined theme.
* **Ease of Migration**: Share code between React (web) and React Native with minimal changes.

### 1.1 Core Benefits

* **Cross-Platform Safety**: Eliminates accidental use of web- or native-only APIs.
* **Compile-Time Validation**: TypeScript catches invalid props and style values.
* **Atomic Styling**: CSS definitions are optimized for web, while mobile uses inline styles.

---

## 2. Markup with Strict HTML

Import UI elements from RSD’s `html` namespace instead of raw elements:

```jsx
import { html } from 'react-strict-dom';

function UserForm() {
  return (
    <html.main>
      <html.fieldset>
        <html.label htmlFor="username">Username</html.label>
        <html.input id="username" type="text" />
      </html.fieldset>
    </html.main>
  );
}
```

* **Type Safety**: `html.input` only accepts attributes common to both web and native. For example, `type="text"` is accepted because it exists in both platforms, but `autocomplete="on"` is not accepted as it is specific to web.
* **Accessibility**: Built-in support for ARIA roles via strict types.

### 2.1 RSD Element Compilation Examples

| RSD Tag         | Web Output            | iOS Output          | Android Output            | React Native Equivalent               |
| --------------- | --------------------- | ------------------- | ------------------------- | ------------------------------------- |
| `<html.div>`    | `<div>`               | `<UIView>`          | `android.view.View`       | `<View>`                              |
| `<html.button>` | `<button>`            | `<UIButton>`        | `android.widget.Button`   | `<TouchableOpacity>` or `<Pressable>` |
| `<html.input>`  | `<input type="text">` | `UITextField`       | `android.widget.EditText` | `<TextInput>`                         |
| `<html.label>`  | `<label>`             | N/A (uses `<Text>`) | N/A (uses `<Text>`)       | `<Text>`                              |
| `<html.main>`   | `<main>`              | `<View>` with role  | `<View>` with role        | `<View accessibilityRole="main">`     |

This mapping enables consistent rendering behavior while supporting cross-platform design.

---

## 3. Styling with `css.create`

RSD’s styling API lets you define style objects that compile to atomic CSS on web and inline styles on native.

```jsx
import { css, html } from 'react-strict-dom';

const styles = css.create({
  button: {
    backgroundColor: '#007bff',
    padding: { default: 12, ':hover': 14 },
    borderRadius: 4,
    color: 'white'
  }
});

function PrimaryButton({ children, ...props }) {
  return (
    <html.button {...props} style={styles.button}>
      {children}
    </html.button>
  );
}
```

* **Responsive Variants**: Support for pseudo-selectors like `:hover`.
* **Theme Integration**: Easily tie values to a shared theme object.

### 3.1 `css.create` Output Examples

| Property          | Web Output (CSS)            | iOS Output (Obj-C/Swift)          | Android Output (Kotlin/Java)         | React Native Style        |
| ----------------- | --------------------------- | --------------------------------- | ------------------------------------ | ------------------------- |
| `padding: 12`     | `padding: 12px;`            | `view.padding = 12`               | `view.setPadding(12)`                | `{ padding: 12 }`         |
| `borderRadius: 4` | `border-radius: 4px;`       | `view.layer.cornerRadius = 4`     | `view.setRadius(4)`                  | `{ borderRadius: 4 }`     |
| `:hover` variant  | `:hover { padding: 14px; }` | Not applicable                    | Not applicable                       | Not applicable (web-only) |
| `color: 'white'`  | `color: white;`             | `label.textColor = UIColor.white` | `textView.setTextColor(Color.WHITE)` | `{ color: 'white' }`      |

This abstraction ensures platform-specific implementations without losing expressiveness or control.

---

## 4. Incremental Adoption

RSD supports platform overrides by using extension-based file conventions:

```jsx
// Button.web.tsx
import { html, css } from 'react-strict-dom';
const webStyles = css.create({ btn: { padding: '0.75rem' } });
export function Button(props) {
  return <html.button style={webStyles.btn} {...props} />;
}

// Button.native.tsx
import { View, StyleSheet, Text, TouchableOpacity } from 'react-native';
const nativeStyles = StyleSheet.create({ btn: { paddingVertical: 12 } });
export function Button(props) {
  return (
    <TouchableOpacity {...props} style={nativeStyles.btn}>
      <Text>{props.children}</Text>
    </TouchableOpacity>
  );
}
```

* Place platform-specific implementations side by side while most of the codebase uses RSD elements.

---

## 5. Component Composition

Combine RSD primitives with your own presentational components:

```jsx
// src/components/Card.tsx
import { html, css } from 'react-strict-dom';

const cardStyles = css.create({ container: {
  border: '1px solid #ccc',
  borderRadius: 8,
  padding: '1rem',
  boxShadow: { default: '0 2px 4px rgba(0,0,0,0.1)' }
}});

export function Card({ children }) {
  return <html.div style={cardStyles.container}>{children}</html.div>;
}
```

* **Encapsulation**: Styles are scoped to the component.
* **Reusability**: Compose smaller RSD-based building blocks.

---

## 6. Handling Events

Event handling works the same as React:

```jsx
import { html } from 'react-strict-dom';

function ClickCounter() {
  const [count, setCount] = React.useState(0);
  return (
    <html.button onClick={() => setCount(c => c + 1)}>
      Clicked {count} times
    </html.button>
  );
}
```

* **SyntheticEvents**: RSD events are strongly typed.
* **Mobile Compatibility**: Touch events map automatically on native.

---

## 7. Conditional Rendering & Composition Patterns

Leverage standard React patterns with RSD:

```jsx
function Status({ state }) {
  if (state === 'loading') return <html.div>Loading...</html.div>;
  if (state === 'error')   return <html.div>Error!</html.div>;
  return <html.div>Done!</html.div>;
}
```

* Familiar React logic applies directly.

---

## 8. Best Practices & Tips

* **Centralize Themes**: Define color, spacing, typography in one place and reference via the CSS API.
* **Limit Overrides**: Use platform files sparingly to keep most codebase unified.
* **Leverage TypeScript**: Let compile-time checks enforce cross-platform compatibility.
* **Test Both Targets**: Regularly run web and native to catch discrepancies early.

---

## Further Reading

* [React Strict DOM GitHub](https://github.com/example/react-strict-dom)
* [Cross-Platform React Patterns](https://reactnative.dev/docs/platform-specific-code)
* [Atomic CSS Principles](https://atomiccss.com)
