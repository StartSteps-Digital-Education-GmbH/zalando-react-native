## Summary

React Native is an open-source framework from Meta that lets you build truly native mobile apps using React’s component model and JavaScript (or TypeScript).
Unlike “web React,” which renders to the browser’s DOM, React Native renders to platform-native UI elements, offering performance and look-and-feel of fully native apps. 
To get started on macOS, you’ll install Node.js, Watchman, Xcode, CocoaPods, and the React Native CLI, then initialize a new project.

---

## What Is React Native?

React Native is a **JavaScript library** for building mobile apps that render with **native components** on iOS and Android. It uses the same **declarative component** approach as React—JSX, props, state, and hooks—but instead of HTML elements (`<div>`, `<span>`), you work with React Native primitives like `<View>`, `<Text>`, and `<Image>`.
Under the hood, React Native runs your JavaScript code in a separate thread and communicates with the native platform over a batched bridge, converting your components into real native UI widgets.

---

## Differences from Web React

1. **Rendering Targets**

   * **Web React** renders HTML in the **DOM** (Document Object Model).
   * **React Native** renders to **platform-native UI** using components like `<View>`, `<Text>`, and `<ScrollView>`.

2. **Styling**

   * On the web, you use CSS or CSS-in-JS; in React Native, you use the **StyleSheet API**, a JavaScript abstraction over native styling, plus Flexbox for layout.

3. **Navigation & APIs**

   * Web apps use React Router or similar; React Native relies on libraries like **React Navigation** or **React Native Navigation** for stack/tab/drawer navigation.
   * Access to device features (camera, geolocation) via built-in **Native Modules** or community packages—no browser APIs.

4. **Lifecycle & Performance**

   * React’s Virtual DOM diffs HTML; React Native diffs a **Shadow Tree** and efficiently updates native views, offering near-native performance.

---

## Setting Up Your Development Environment on macOS

Follow React Native’s official environment guide for the **“React Native CLI Quickstart”** under the macOS tab ([React Native][2]).

### 1. Install Homebrew (if not already)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> Homebrew simplifies package installation on macOS.

### 2. Install Node.js & Yarn

```bash
brew install node
npm install --global yarn
```

> React Native requires Node.js ≥14; Yarn is optional but recommended.

### 3. Install Watchman

```bash
brew install watchman
```

> Watchman watches file changes, improving rebuild performance on macOS.

### 4. Xcode & CocoaPods

1. **Install Xcode** from the Mac App Store.
2. **Agree to Xcode license**:

   ```bash
   sudo xcodebuild -license accept
   ```
3. **Install CocoaPods** (for iOS native dependencies):

   ```bash
   sudo gem install cocoapods
   ```

> CocoaPods manages iOS project dependencies; required for iOS builds.

### 5. (Optional) Android Setup

If you plan to target Android:

1. **Download Android Studio** from [https://developer.android.com/studio](https://developer.android.com/studio).
2. In Android Studio’s **SDK Manager**, install **Android SDK**, **Platform-Tools**, and **Build-Tools**.
3. Set environment variables in `~/.zshrc` or `~/.bash_profile`:

   ```bash
   export ANDROID_HOME=$HOME/Library/Android/sdk
   export PATH=$PATH:$ANDROID_HOME/emulator:$ANDROID_HOME/platform-tools
   ```

> Android setup is similar on Linux; see React Native docs for details ([React Native][1]).

---

## Initializing a Project

### 1. Create a New App (Using React Native CLI)

```bash
npx @react-native-community/cli@latest init TestApp

```

> The app template is TypeScript by default and it adds `tsconfig.json` and `.tsx` support out of the box.

### 2. Run Your App

* **iOS**:

  ```bash
  cd TestApp
  npx pod-install ios
  npx react-native run-ios
  ```
* **Android** (with an emulator running):

  ```bash
  npx react-native run-android
  ```

> Your new app launches in the simulator or emulator—edit `App.tsx` to see hot reload.

---

### References

1. **Introduction – React Native** ([React Native][1])
2. **Get Started – Environment Setup** ([React Native][2])
3. **React Native on GitHub** ([GitHub][3])

[1]: https://reactnative.dev/docs/getting-started "Introduction - React Native"
[2]: https://reactnative.dev/docs/environment-setup "Get Started with React Native"
[3]: https://github.com/facebook/react-native "A framework for building native applications using React - GitHub"
