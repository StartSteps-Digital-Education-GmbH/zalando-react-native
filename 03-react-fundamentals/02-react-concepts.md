# Lesson 2: React Concepts

**Objective:**
Understand the foundational concepts of React—JSX, components, props, state, event handling, conditional rendering, and lists. These are critical to working effectively in React Native.

---

## Part A: JSX – JavaScript XML

JSX lets you write HTML-like syntax in JavaScript/TypeScript, which React transforms into elements using `React.createElement`.

```tsx
const element = <h1>Hello, world!</h1>;
```

> In React Native, JSX is used to declare native UI components like `<View>`, `<Text>`, and `<Image>` instead of HTML tags.

### Key Features

* Not a string or HTML, but syntactic sugar for `React.createElement`
* Allows **JavaScript expressions** inside `{ }`
* Each JSX expression must return a **single root element**
* JSX can include **props**, **conditional logic**, and **function calls**

---

## Part B: Components

Components are the basic units of a React app. In React Native, your entire UI is built from components.

### 1. Function Components (Preferred)

```tsx
function Welcome(props: { name: string }) {
  return <Text>Hello, {props.name}</Text>;
}
```

### 2. Class Components (Legacy)

```tsx
class Welcome extends React.Component<{ name: string }> {
  render() {
    return <Text>Hello, {this.props.name}</Text>;
  }
}
```

> React Native encourages **function components with Hooks**. Class components are supported but generally avoided in modern codebases.

---

## Part C: Props – Component Inputs

Props are read-only inputs passed from parent to child components.

```tsx
function Greeting(props: { name: string }) {
  return <Text>Hello, {props.name}!</Text>;
}

// Usage
<Greeting name="John" />
```

**Props are:**

* Immutable within the child component
* Passed via attributes
* Can be any valid JavaScript value (strings, numbers, objects, functions)

---

## Part D: State – Component Memory

State represents mutable data local to a component. When state changes, React re-renders the component.

### Class Component Example:

```tsx
class Counter extends React.Component {
  state = { count: 0 };

  render() {
    return (
      <View>
        <Text>Count: {this.state.count}</Text>
        <Button
          title="Increment"
          onPress={() => this.setState({ count: this.state.count + 1 })}
        />
      </View>
    );
  }
}
```

> In React Native, use `Button`, `Text`, and `View` instead of `button`, `p`, or `div`.

---

## Part E: Event Handling

React wraps native events into a consistent event system. You pass handler functions using `camelCase` props.

```tsx
function ButtonExample() {
  const handleClick = () => {
    console.log('Button clicked!');
  };

  return <Button title="Click me" onPress={handleClick} />;
}
```

> In React Native, use `onPress` instead of `onClick`.

---

## Part F: Conditional Rendering

Use standard JavaScript conditionals (if/else, ternary, &&) to show different components based on data:

```tsx
function Greeting({ isLoggedIn }: { isLoggedIn: boolean }) {
  return isLoggedIn ? <UserGreeting /> : <GuestGreeting />;
}
```

---

## Part G: Lists and Keys

Render lists with `map()` and provide a unique `key` to each element:

```tsx
function NumberList({ numbers }: { numbers: number[] }) {
  return (
    <FlatList
      data={numbers}
      keyExtractor={(item) => item.toString()}
      renderItem={({ item }) => <Text>{item}</Text>}
    />
  );
}
```

> For React Native, use `FlatList` or `SectionList` for performant list rendering.

---

## Part H: Best Practices

1. **Use function components** and **Hooks** (e.g., `useState`, `useEffect`)
2. **Lift state up** to common ancestors when shared between components
3. **Use keys** for lists to ensure correct reconciliation
4. **Compose components** instead of using inheritance
5. **Write small, focused components** for better reusability
6. **Avoid inline functions inside JSX** when performance is critical

---

## Summary

| Concept        | Key Idea                                            |
| -------------- | --------------------------------------------------- |
| JSX            | HTML-like syntax used in JS/TS to describe UI       |
| Components     | Reusable, isolated building blocks of the UI        |
| Props          | Read-only inputs to components                      |
| State          | Mutable data that affects rendering                 |
| Event Handling | Functions triggered by user actions (e.g., onPress) |
| Lists          | Use `FlatList` with keys for dynamic content        |
| Conditional    | Render UI based on conditions using JS syntax       |

---

## References

* [React Native: Intro to React](https://reactnative.dev/docs/intro-react?utm_source=chatgpt.com)
* [JSX in Depth](https://react.dev/learn/writing-markup-with-jsx?utm_source=chatgpt.com)
* [Components and Props](https://react.dev/learn/passing-props-to-a-component?utm_source=chatgpt.com)
* [State: A Component’s Memory](https://react.dev/learn/state-a-components-memory?utm_source=chatgpt.com)
* [Handling Events](https://react.dev/learn/responding-to-events?utm_source=chatgpt.com)
* [Rendering Lists](https://react.dev/learn/rendering-lists?utm_source=chatgpt.com)
