# Building Your First React Native App

This practice session will guide you through building a simple React Native app.

## Exercise 1: Setup

1. Create a new React Native project:
```bash
npx react-native init MyFirstApp
cd MyFirstApp
```

2. Install React Strict DOM:
```bash
npm install @react-strict-dom/core
```

3. Start the development server:
```bash
npx react-native start
```

4. Run the app on your device/emulator:
```bash
# For Android
npx react-native run-android

# For iOS
npx react-native run-ios
```

## Exercise 2: Basic Layout

Create a simple layout with:
- A header section
- A content section
- A footer section

```jsx
// App.js
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

function App() {
  return (
    <View style={styles.container}>
      <View style={styles.header}>
        <Text style={styles.headerText}>My First App</Text>
      </View>
      <View style={styles.content}>
        <Text>Welcome to React Native!</Text>
      </View>
      <View style={styles.footer}>
        <Text>Footer Content</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  // Add your styles here
});

export default App;
```

## Exercise 3: Styling with React Strict DOM

Convert the previous layout to use React Strict DOM:

```jsx
import { css } from '@react-strict-dom/core';

const styles = css`
  .container {
    display: flex;
    flex-direction: column;
    flex: 1;
  }
  .header {
    background-color: #f0f0f0;
    padding: 20px;
  }
  .content {
    flex: 1;
    padding: 20px;
  }
  .footer {
    background-color: #f0f0f0;
    padding: 20px;
  }
`;
```

## Exercise 4: Adding User Input

Add a text input and button to the app:

```jsx
import { useState } from 'react';
import { TextInput, Button } from 'react-native';

function App() {
  const [text, setText] = useState('');

  return (
    <View style={styles.container}>
      {/* Previous components */}
      <View style={styles.inputContainer}>
        <TextInput
          value={text}
          onChangeText={setText}
          placeholder="Enter text"
          style={styles.input}
        />
        <Button
          title="Submit"
          onPress={() => console.log(text)}
        />
      </View>
    </View>
  );
}
```

## Exercise 5: Platform-Specific Styling

Add platform-specific styles to your components:

```jsx
import { Platform } from 'react-native';

const styles = StyleSheet.create({
  container: {
    ...Platform.select({
      ios: {
        backgroundColor: '#fff',
      },
      android: {
        backgroundColor: '#f5f5f5',
      },
    }),
  },
});
```

## Exercise 6: Image Component

Add an image to your app:

```jsx
import { Image } from 'react-native';

function App() {
  return (
    <View style={styles.container}>
      <Image
        source={{ uri: 'https://example.com/image.jpg' }}
        style={styles.image}
      />
    </View>
  );
}
```

## Exercise 7: ScrollView

Make your content scrollable:

```jsx
import { ScrollView } from 'react-native';

function App() {
  return (
    <ScrollView style={styles.container}>
      {/* Your content here */}
    </ScrollView>
  );
}
```

## Final Exercise: Complete App

Combine all the previous exercises to create a complete app with:
1. A scrollable layout
2. Platform-specific styling
3. User input handling
4. Image display
5. React Strict DOM styling

## Additional Challenges

1. Add error handling for the image loading
2. Implement form validation
3. Add animations to the components
4. Create reusable components
5. Add dark mode support

## Next Steps

After completing these exercises, you should:
1. Test the app on both iOS and Android
2. Review the code for best practices
3. Consider performance optimizations
4. Document your components 