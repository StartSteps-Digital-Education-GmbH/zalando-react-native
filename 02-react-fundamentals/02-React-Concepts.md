# React Concepts

This section covers the fundamental concepts of React that you'll need for React Native development.

## JSX

JSX is a syntax extension for JavaScript that allows you to write HTML-like code in your JavaScript files:

```jsx
const element = <h1>Hello, world!</h1>;
```

Key points about JSX:
- It's not a string
- It gets compiled to JavaScript
- You can embed expressions using curly braces
- It must have a single root element

## Components

Components are the building blocks of React applications. They can be either function components or class components.

### Function Components

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

### Class Components

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

## Props

Props (short for properties) are how components receive data from their parent:

```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Usage
<Greeting name="John" />
```

Props are:
- Read-only
- Passed from parent to child
- Can be any JavaScript value

## State

State is data that changes over time and affects what a component renders:

```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Increment
        </button>
      </div>
    );
  }
}
```

## Component Lifecycle

Class components have several lifecycle methods:

```jsx
class Example extends React.Component {
  componentDidMount() {
    // Runs after component is mounted
  }

  componentDidUpdate(prevProps, prevState) {
    // Runs after component updates
  }

  componentWillUnmount() {
    // Runs before component is removed
  }

  render() {
    return <div>Example</div>;
  }
}
```

## Event Handling

React events are similar to DOM events but with some differences:

```jsx
function Button() {
  function handleClick(e) {
    e.preventDefault();
    console.log('Button clicked!');
  }

  return <button onClick={handleClick}>Click me</button>;
}
```

## Conditional Rendering

You can conditionally render elements using JavaScript operators:

```jsx
function Greeting({ isLoggedIn }) {
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}
```

## Lists and Keys

When rendering lists, you need to provide a unique key prop:

```jsx
function NumberList({ numbers }) {
  return (
    <ul>
      {numbers.map((number) => (
        <li key={number.toString()}>{number}</li>
      ))}
    </ul>
  );
}
```

## Best Practices

1. Keep components small and focused
2. Use composition over inheritance
3. Lift state up when needed
4. Use controlled components for forms
5. Use keys when rendering lists