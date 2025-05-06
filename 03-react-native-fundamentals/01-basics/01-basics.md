# React Native Basics

This section covers the fundamental concepts of React Native development.

## Core Components

React Native provides a set of core components that map to native platform components:

```jsx
import { View, Text, Image, ScrollView } from 'react-native';

function MyComponent() {
  return (
    <ScrollView>
      <View>
        <Text>Hello, React Native!</Text>
        <Image
          source={{ uri: 'https://example.com/image.jpg' }}
          style={{ width: 200, height: 200 }}
        />
      </View>
    </ScrollView>
  );
}
```

Common core components:
- `View`: Container component
- `Text`: Display text
- `Image`: Display images
- `ScrollView`: Scrollable container
- `TextInput`: Text input field
- `Button`: Touchable button
- `TouchableOpacity`: Customizable touchable component

## Styling

React Native uses a subset of CSS properties for styling:

```jsx
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#fff',
  },
  text: {
    fontSize: 16,
    color: '#333',
  },
});
```

Key styling concepts:
- Use `StyleSheet.create` for performance
- Styles are camelCase (e.g., `backgroundColor`)
- No CSS selectors or inheritance
- No units (numbers are density-independent pixels)

## Layout with Flexbox

React Native uses Flexbox for layout:

```jsx
const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'center',
    alignItems: 'center',
  },
  box: {
    width: 50,
    height: 50,
    backgroundColor: 'red',
  },
});
```

Common Flexbox properties:
- `flex`: Grow/shrink factor
- `flexDirection`: Main axis direction
- `justifyContent`: Main axis alignment
- `alignItems`: Cross axis alignment
- `alignSelf`: Individual item alignment

## React Strict DOM

React Strict DOM is Zalando's preferred styling approach:

```jsx
import { css } from '@react-strict-dom/core';

const styles = css`
  .container {
    display: flex;
    flex-direction: column;
    padding: 20px;
  }
  .text {
    color: #333;
    font-size: 16px;
  }
`;

function MyComponent() {
  return (
    <div className={styles.container}>
      <p className={styles.text}>Hello, React Strict DOM!</p>
    </div>
  );
}
```

Benefits of React Strict DOM:
- Consistent styling across platforms
- Better type safety
- Improved performance
- Easier maintenance

## Handling User Input

```jsx
import { useState } from 'react';
import { TextInput, Button } from 'react-native';

function InputExample() {
  const [text, setText] = useState('');

  return (
    <View>
      <TextInput
        value={text}
        onChangeText={setText}
        placeholder="Enter text"
      />
      <Button
        title="Submit"
        onPress={() => console.log(text)}
      />
    </View>
  );
}
```

## Platform-Specific Code

```jsx
import { Platform } from 'react-native';

const styles = StyleSheet.create({
  container: {
    ...Platform.select({
      ios: {
        backgroundColor: 'red',
      },
      android: {
        backgroundColor: 'blue',
      },
    }),
  },
});
```

## Best Practices

1. Use core components appropriately
2. Follow platform conventions
3. Optimize performance with `StyleSheet.create`
4. Use React Strict DOM for styling
5. Handle platform differences gracefully
6. Test on both iOS and Android

## Next Steps

Proceed to the practice session to apply these concepts:
- [Building Your First App](./practice-session/01-first-app.md) 