# Quick Setup Guide: React-Strict-DOM with Vite and StyleX Styling

This guide will walk you through the essential steps to create a new Vite + React + TypeScript project and configure it to use `react-strict-dom` for UI elements and its built-in `css` object for styling. The `css` object in `react-strict-dom` utilizes StyleX technology, so we'll configure the necessary StyleX plugin for Vite.

**Prerequisites:**
*   Node.js and npm (or yarn/pnpm) installed.

---

## Step 1: Create a New Vite + React + TypeScript Project

1.  **Generate the Project:**
    Open your terminal and run the following command. Replace `my-rsd-app` with your desired project name.
    ```bash
    npm create vite@latest my-rsd-app -- --template react-ts
    ```

2.  **Navigate into Project Directory:**
    ```bash
    cd my-rsd-app
    ```

---

## Step 2: Configure `package.json` for Compatibility

`react-strict-dom` and its underlying StyleX dependencies have specific version requirements that might differ from the latest versions scaffolded by Vite. We need to adjust these.

1.  **Edit `package.json`:**
    Open the `package.json` file in the root of your `my-rsd-app` project.
    Replace its entire content with the following, ensuring versions match. This configuration is known to work:

    ```json
    {
      "name": "my-rsd-app",
      "private": true,
      "version": "0.0.0",
      "type": "module",
      "scripts": {
        "dev": "vite",
        "build": "tsc && vite build",
        "lint": "eslint . --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
        "preview": "vite preview"
      },
      "dependencies": {
        "@stylexjs/stylex": "^0.9.3",
        "react": "^18.2.0",
        "react-dom": "^18.2.0",
        "react-strict-dom": "^0.0.27"
      },
      "devDependencies": {
        "@types/react": "^18.2.0",
        "@types/react-dom": "^18.2.0",
        "@vitejs/plugin-react": "^4.2.1",
        "eslint": "^8.57.0",
        "eslint-plugin-react-hooks": "^4.6.0",
        "eslint-plugin-react-refresh": "^0.4.6",
        "typescript": "^5.2.2",
        "vite": "^5.2.13", // Using Vite 5.x for vite-plugin-stylex compatibility
        "vite-plugin-stylex": "^0.13.0" // The Vite plugin for StyleX
        // Note: Add back any other ESLint/TypeScript plugins if your scaffolded project had them
        // (e.g., "@typescript-eslint/eslint-plugin", "@typescript-eslint/parser")
      },
      "overrides": {
        "react-native": { // Resolves potential peer dependency issues from react-strict-dom
          "react": "$react",
          "@types/react": "$@types/react"
        }
      }
    }
    ```

    **Key Package Explanations:**
    *   `react-strict-dom@0.0.27`: Provides `html.<element>` components and the `css` styling object.
    *   `@stylexjs/stylex@^0.9.3`: The core StyleX library required by `react-strict-dom`'s `css` object and compatible with `vite-plugin-stylex@0.13.0`.
    *   `react@^18.2.0`, `react-dom@^18.2.0`: Required by `react-strict-dom`.
    *   `vite@^5.2.13`: Vite 5.x, required by `vite-plugin-stylex@0.13.0`.
    *   `vite-plugin-stylex@^0.13.0`: Essential Vite plugin to compile StyleX syntax used by `css.create()`.
    *   `overrides`: Helps manage version conflicts from indirect dependencies.

---

## Step 3: Install Dependencies

After saving the changes to `package.json`:

1.  **Clean Previous `node_modules` (Important for version changes):**
    ```bash
    rm -rf node_modules package-lock.json
    ```
    (On Windows, use `rd /s /q node_modules` and `del package-lock.json`)

2.  **Install Dependencies:**
    ```bash
    npm install
    ```
    This will install all the packages specified in your updated `package.json`.

---

## Step 4: Configure Vite for StyleX

The `css.create()` API from `react-strict-dom` relies on StyleX, which needs a build-time plugin to compile styles.

1.  **Edit `vite.config.ts`:**
    Open the `vite.config.ts` file in your project root.
    Replace its content with the following:

    ```typescript
    // vite.config.ts
    import { defineConfig } from "vite";
    import react from "@vitejs/plugin-react";
    import styleX from "vite-plugin-stylex"; // Import the StyleX plugin

    export default defineConfig({
      plugins: [
        react(), // Standard Vite plugin for React (handles JSX, HMR)
        styleX({ // Configure and add the StyleX plugin
          importSources: [
            // This is crucial: it tells the plugin to look for StyleX API calls
            // (like css.create) when `css` is imported from "react-strict-dom".
            {
              from: "react-strict-dom",
              as: "css",
            },
            // It's also good practice to include the default StyleX import source
            // in case you or another library use `stylex.create()` directly.
            "@stylexjs/stylex",
          ],
          // Optional: You can specify the output filename for the generated CSS
          // fileName: 'stylex-generated.css',
        }),
      ],
      // Optional: Sometimes helpful for react-strict-dom, but not always necessary
      // optimizeDeps: {
      //   exclude: ["react-strict-dom"],
      // },
    });
    ```

    **Explanation:**
    *   `vite-plugin-stylex` is added to the `plugins` array.
    *   The `importSources` option is configured to recognize `css.create()` calls when `css` is imported from `react-strict-dom`.

---

## Step 5: Basic Global CSS (Optional but Recommended)

1.  **Create or Modify `src/global.css`:**
    Vite's default template might create `src/index.css`. You can rename it to `src/global.css` or delete `index.css` and create `src/global.css`. Add some basic reset/global styles:

    ```css
    /* src/global.css */
    body {
      margin: 0;
      font-family: system-ui, -apple-system, sans-serif;
      background-color: #f0f0f0;
      color: #333;
    }

    * {
      box-sizing: border-box;
    }
    ```

2.  **Import `global.css` in `src/main.tsx`:**
    Open `src/main.tsx` and ensure your global CSS file is imported:

    ```typescript
    // src/main.tsx
    import React from 'react';
    import ReactDOM from 'react-dom/client';
    import App from './App.tsx';
    import './global.css'; // Import your global styles

    // If vite-plugin-stylex is configured with a specific 'fileName' for its output,
    // you might need to import that generated CSS file here as well, e.g.:
    // import './stylex-generated.css'; 

    ReactDOM.createRoot(document.getElementById('root')!).render(
      <React.StrictMode>
        <App />
      </React.StrictMode>,
    );
    ```

---

## Step 6: Test with a Simple `react-strict-dom` Component

Let's modify `src/App.tsx` to verify that `react-strict-dom` and its `css` styling are working.

1.  **Edit `src/App.tsx`:**
    Replace the content of `src/App.tsx` with the following:

    ```tsx
    // src/App.tsx
    import { useState } from 'react';
    import { html, css } from 'react-strict-dom'; // Import html and css

    // 1. Define styles using css.create()
    const styles = css.create({
      container: {
        display: 'flex',
        flexDirection: 'column',
        alignItems: 'center',
        justifyContent: 'center',
        minHeight: '100vh',
        backgroundColor: '#e0e0e0', // A light grey background for the container
        padding: '20px',
      },
      title: {
        fontSize: '2rem',
        color: '#333',
        marginBottom: '20px',
      },
      button: {
        backgroundColor: '#007bff',
        color: 'white',
        paddingTop: '10px', // StyleX prefers string units, but numbers can work for px
        paddingBottom: '10px',
        paddingLeft: '20px',
        paddingRight: '20px',
        borderStyle: 'none', // Equivalent to 'border: none'
        borderRadius: '5px',
        cursor: 'pointer',
        fontSize: '1rem',
        // Example of a dynamic style property (though not used by this button directly)
        // opacity: (isDisabled) => isDisabled ? 0.5 : 1,
      },
      // Example :hover (Note: For full pseudo-class support, css.props() is more robust)
      buttonHoverable: {
        backgroundColor: '#007bff',
        color: 'white',
        padding: '10px 20px', // Shorthand padding
        borderStyle: 'none',
        borderRadius: '5px',
        cursor: 'pointer',
        fontSize: '1rem',
        transition: 'background-color 0.3s ease', // Smooth transition for hover
        ':hover': { // This will be compiled into a separate class by StyleX
          backgroundColor: '#0056b3',
        }
      },
      counterText: {
        fontSize: '1.5rem',
        margin: '20px',
      }
    });

    function App() {
      const [count, setCount] = useState(0);

      return (
        // 2. Apply styles using the `style` prop OR `css.props()`
        // For this quick setup guide, we show `style={...}` as per your findings.
        // If complex styles (like :hover above) don't work as expected with `style={...}`,
        // switch to `css.props()` for those elements.
        <html.div style={styles.container}>
          <html.h1 style={styles.title}>React Strict DOM + StyleX Test</html.h1>

          {/* Button with basic style application */}
          <html.button
            style={styles.button} // Applying styles directly
            onClick={() => setCount((c) => c + 1)}
          >
            Increment Count (Basic)
          </html.button>

          <html.p style={styles.counterText}>Count is: {count}</html.p>

          {/* Button demonstrating :hover (best applied with css.props) */}
          <html.p>For robust :hover, use css.props():</html.p>
          <html.button
            {...css.props(styles.buttonHoverable)} // Using css.props for full StyleX features
            onClick={() => alert('Hoverable button clicked!')}
          >
            Button with Hover (using css.props)
          </html.button>
        </html.div>
      );
    }

    export default App;
    ```

    **Important Note on Applying Styles in `App.tsx`:**
    *   We define styles using `css.create()`.
    *   The example shows applying styles with `style={styles.button}` for the first button.
    *   For the second button (`buttonHoverable`), which includes a `:hover` pseudo-class, it demonstrates the standard StyleX way using `{...css.props(styles.buttonHoverable)}`. **This `css.props()` method is generally more robust for features like pseudo-classes and media queries.** If `style={styles.yourStyle}` doesn't correctly apply more complex styles (like `:hover`), you should use `css.props()` instead for those specific elements.

---

## Step 7: Run the Development Server

1.  **Start the Server:**
    If it's not already running, or if you stopped it to make changes:
    ```bash
    npm run dev
    ```

2.  **View in Browser:**
    Open `http://localhost:5173` (or the address shown in your terminal).

    You should see your title and buttons.
    *   The "Increment Count (Basic)" button should have its basic styles.
    *   The "Button with Hover (using css.props)" button should change its background color when you hover over it.
    *   Clicking the first button should increment the count.

    If you see the styles applied and the `css.create` call does not throw a runtime error, your `react-strict-dom` and StyleX setup (via `vite-plugin-stylex`) is working correctly!

---

This setup provides a solid foundation for building applications with `react-strict-dom` and leveraging its StyleX-based `css` object for styling within a Vite environment. Remember the distinction between `style={...}` and `css.props()` for applying styles, especially when dealing with pseudo-classes or other advanced CSS features.
