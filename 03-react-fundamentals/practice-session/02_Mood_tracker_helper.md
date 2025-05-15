# 🧪 Practical Project: Building a Mood Tracker

In this hands-on project, you'll build a "Mood Tracker" web application. This project is designed to solidify your understanding of core React concepts while introducing you to `react-strict-dom` for building UIs and its powerful `css` object for styling (which uses StyleX technology from Meta).

## 🧭 Project Objective:

Create a simple yet functional **Mood Tracker** where users can:
1.  Select their current mood (e.g., Happy, Sad, Neutral).
2.  View a log of their recent mood entries, each with a timestamp.
3.  See a motivational quote that dynamically changes based on their selected mood.

---

## ✅ Concepts You'll Master:

| Concept                     | Application in this Project                                                   |
| --------------------------- | ----------------------------------------------------------------------------- |
| **React Fundamentals**      | Functional components, JSX syntax, props for data flow, state (`useState`), and side effects (`useEffect`). |
| **Component-Based Architecture**| Breaking down the application into small, reusable UI pieces.             |
| **`react-strict-dom`**      | Using `html.div`, `html.button`, etc., as the building blocks for all your DOM elements. |
| **Styling with `css` from `react-strict-dom`** | Defining component-specific styles using `css.create()` and applying them. This leverages StyleX for optimized CSS. |
| **Vite Build Tool**         | Setting up a modern React project, running a fast development server, and understanding basic configuration. |
| **TypeScript**              | Enhancing code quality with types for props, state, and custom data structures (like enums and type aliases). |
| **Event Handling**          | Managing user interactions, like button clicks.                               |
| **Simulated Asynchronicity**| Using `setTimeout` within `useEffect` to mimic real-world data fetching.     |

---

## 🛠 Key Project Features:

1.  **MoodSelector:** A component enabling users to choose their current mood from a predefined list.
2.  **MoodLog:** A component that displays a chronological list of previously selected moods.
3.  **MotivationalQuote:** A component that shows an uplifting quote, tailored to the user's current mood.

---

## 📁 Final Project File Structure:

```
/mood-tracker/
├── public/                     // Static assets
├── src/
│   ├── components/             // Reusable React components
│   │   ├── MoodSelector.tsx
│   │   ├── MoodLog.tsx
│   │   └── MotivationalQuote.tsx
│   ├── styles/                 // Styling-related files
│   │   └── theme.ts            // Theme constants for consistent styling
│   ├── types/                  // TypeScript type definitions
│   │   └── mood.ts
│   ├── utils/                  // Utility functions
│   │   └── quotes.ts
│   ├── App.tsx                 // Main application component
│   ├── main.tsx                // Entry point of the application
│   └── global.css              // Global styles for the application
├── .eslintrc.cjs               // ESLint configuration (if using)
├── index.html                  // Main HTML page
├── package.json                // Project metadata and dependencies
├── tsconfig.json               // TypeScript compiler options
├── tsconfig.node.json          // TypeScript options for Node.js environment (e.g., vite.config.ts)
└── vite.config.ts              // Vite build tool configuration
```

---

## 🚀 Step-by-Step Guide to Building Your Mood Tracker:

### Step 0: Setting Up Your Development Environment

**Why this step is important:**
Before we can write any code for our app, we need to create a project structure and install all the necessary tools and libraries. We'll use **Vite** for a fast and modern development experience. We'll also configure specific versions of **React**, **`react-strict-dom`**, and **StyleX** related packages to ensure they all work together smoothly, as these are cutting-edge technologies.

1.  **Create a New Vite Project:**
    Open your terminal (Command Prompt, PowerShell, Terminal app, etc.) and run this command:
    ```bash
    npm create vite@latest mood-tracker -- --template react-ts
    ```
    *   **What this does:** `npm create vite@latest` is the command to start a new Vite project. `mood-tracker` will be the name of your project folder. `-- --template react-ts` tells Vite to set up the project using React and TypeScript.

2.  **Navigate into Your Project Directory:**
    Once the command finishes, change your current directory to the newly created project folder:
    ```bash
    cd mood-tracker
    ```

3.  **Configure `package.json` (The Project's Recipe Book):**
    The `package.json` file lists all the libraries (dependencies) your project needs and how to run scripts like starting your app. We need to adjust it to use specific versions that are known to work well together for `react-strict-dom` and its styling system.

    Open the `mood-tracker/package.json` file in your code editor and replace its entire content with the following (this is based on the working configuration you provided):
    ```json
    {
      "name": "mood-tracker", // You can keep the name Vite generated if you prefer
      "private": true,
      "version": "0.0.0",
      "type": "module",
      "scripts": {
        "dev": "vite",
        "build": "tsc && vite build", // tsc checks types before building
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
        "@vitejs/plugin-react": "^4.2.1", // Compatible with Vite 5
        "eslint": "^8.57.0", // Or your scaffolded ESLint version
        "eslint-plugin-react-hooks": "^4.6.0",
        "eslint-plugin-react-refresh": "^0.4.6",
        "typescript": "^5.2.2", // Or your scaffolded TypeScript version
        "vite": "^5.2.13", // Vite 5.x for compatibility with vite-plugin-stylex
        "vite-plugin-stylex": "^0.13.0"
        // If your `npm create vite` scaffolded specific ESLint/TS plugins like
        // "@typescript-eslint/eslint-plugin" and "@typescript-eslint/parser",
        // ensure they are also listed here with compatible versions.
      },
      "overrides": {
        "react-native": {
          "react": "$react",
          "@types/react": "$@types/react"
        }
      }
    }
    ```
    *   **Key Packages Explained:**
        *   **`react`, `react-dom`:** Core React libraries, version `18.2.0`.
        *   **`react-strict-dom`:** Version `0.0.27`, provides `html.<element>` components and the `css` styling object.
        *   **`@stylexjs/stylex`:** Version `0.9.3`, the underlying StyleX library that powers `react-strict-dom`'s `css` object.
        *   **`vite`:** Version `5.2.13`, our project build tool.
        *   **`vite-plugin-stylex`:** Version `0.13.0`, the Vite plugin essential for processing StyleX syntax (which `css.create()` uses).
        *   **`overrides`:** Helps manage version conflicts for indirect dependencies.

4.  **Install All Dependencies:**
    Now that `package.json` is updated, we need to download and install these libraries. To ensure a clean installation, first delete any existing `node_modules` folder and `package-lock.json` file:
    ```bash
    rm -rf node_modules package-lock.json
    ```
    Then, run the install command:
    ```bash
    npm install
    ```
    *   **What this does:** npm reads your `package.json` and installs all the specified libraries into a `node_modules` folder.

5.  **Configure Vite for StyleX (`vite.config.ts`):**
    We need to tell Vite to use `vite-plugin-stylex` so it can understand and compile our styles.
    Open (or create if it doesn't exist) `mood-tracker/vite.config.ts` and set its content to (this is based on your working configuration):
    ```typescript
    // vite.config.ts
    import { defineConfig } from "vite";
    import react from "@vitejs/plugin-react";
    import styleX from "vite-plugin-stylex";

    export default defineConfig({
      plugins: [
        react(),
        styleX({
          importSources: [
            // This tells the plugin to process `css.create()` calls
            // when `css` is imported from `react-strict-dom`.
            {
              from: "react-strict-dom",
              as: "css",
            },
            // It's good practice to also include the default StyleX import source
            // in case you (or a library) ever use `stylex.create()` directly.
            "@stylexjs/stylex",
          ],
        }),
      ],
      // The following optimization might be helpful for react-strict-dom in some cases
      // but can be omitted if everything works fine without it.
      // optimizeDeps: {
      //   exclude: ["react-strict-dom"],
      // },
    });
    ```
    *   **Why this configuration?**
        *   `vite-plugin-stylex` is crucial. It finds your `css.create()` calls (used for styling), converts them into highly optimized CSS, and ensures your app uses these styles correctly.
        *   The `importSources` option tells the plugin which specific import patterns (like `import { css } from 'react-strict-dom'`) contain StyleX API calls that need processing.

6.  **Create Global CSS File (`src/global.css`):**
    This file will hold very basic styles that apply to your entire application.
    *   If Vite created an `src/index.css`, you can rename it to `src/global.css` or delete `index.css` and create `global.css`.
    *   Put the following content in `src/global.css`:
        ```css
        /* src/global.css */
        /* Base styles for the entire application */
        @stylex stylesheet;
        
        body {
          margin: 0; /* Remove default browser margin */
          font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto,
            Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
          background-color: #f4f7f9; /* A light, neutral background for the page */
          color: #333; /* Default text color */
          line-height: 1.6; /* Improves readability */
        }

        /* A common reset for consistent box sizing */
        * {
          box-sizing: border-box;
        }
        ```

7.  **Import Global CSS in `src/main.tsx`:**
    Your application needs to load these global styles.
    Open `src/main.tsx` and make sure it imports `global.css`:
    ```typescript
    // src/main.tsx
    import React from 'react';
    import ReactDOM from 'react-dom/client';
    import App from './App.tsx';
    import './global.css'; // <-- IMPORT YOUR GLOBAL STYLES

    ReactDOM.createRoot(document.getElementById('root')!).render(
      <React.StrictMode>
        <App />
      </React.StrictMode>,
    );
    ```

8.  **Initialize Git (Highly Recommended):**
    Git is a version control system that helps you track changes to your code.
    ```bash
    git init
    git add .
    git commit -m "Initial project setup: Vite, React, react-strict-dom, StyleX configured"
    ```

9.  **Run the Development Server:**
    Let's see if everything is set up correctly!
    ```bash
    npm run dev
    ```
    Vite will start a development server. Open your web browser and go to the local address shown in your terminal (usually `http://localhost:5173/`). You should see the default Vite + React welcome page. If errors occur, double-check `package.json`, `vite.config.ts`, and ensure `npm install` completed successfully.

---

### A Note on Applying Styles: `style={...}` vs. `css.props()`

In this guide, we will primarily use the `style={styles.yourStyleObject}` pattern to apply styles defined with `css.create()`, as this has been found to work in our current project configuration.

```javascript
// Example of how we'll apply styles in this guide:
const styles = css.create({ myButton: { color: 'blue' } });
// ...
// <html.button style={styles.myButton}>Click</html.button>
```

However, it's important for you to know that the standard and fully-featured way to apply styles with StyleX (which powers `react-strict-dom`'s `css` object) is by using `css.props()`:

```javascript
// Standard StyleX pattern:
const styles = css.create({ myButton: { color: 'blue', ':hover': { color: 'red' } } });
// ...
// <html.button {...css.props(styles.myButton)}>Click</html.button>
```

**Why `css.props()` is typically recommended:**
*   **Full Feature Support:** `css.props()` is designed to correctly handle all StyleX features, including pseudo-classes (like `:hover`, `:focus`), pseudo-elements, media queries, and complex conditional styles defined in `css.create()`. These are translated into optimized CSS class names.
*   **Performance:** It allows StyleX to apply its full range of optimizations.

**If `style={...}` doesn't work for complex styles:**
While `style={...}` might work for basic CSS properties in our setup, if you find that more complex styles (especially pseudo-classes like `:hover` or media queries) are not applying correctly, **you should switch to using `css.props()` for that specific style application.** It's a more robust method for leveraging StyleX's capabilities.

For the remainder of this guide, we will use `style={...}` for simplicity, but keep `css.props()` in mind as the standard and more powerful alternative.

---

### Step 1: Defining Data Structures (Types) and Utility Data

**Why this step is important:**
TypeScript allows us to define the "shape" of our data. This makes our code more predictable, easier to understand, and helps catch errors early. We'll define what a "mood" is and how we'll store mood entries and quotes.

1.  **Create Mood Types (`src/types/mood.ts`):**
    *   Create a new folder `src/types`.
    *   Inside `src/types`, create a file named `mood.ts`.
    *   Add the following code:
        ```typescript
        // src/types/mood.ts
        export enum Mood {
          Happy = "🙂 Happy",
          Neutral = "😐 Neutral",
          Sad = "🙁 Sad",
          Excited = "🤩 Excited",
          Tired = "😴 Tired",
        }

        export type MoodEntry = {
          id: string; // A unique identifier for each log entry
          mood: Mood; // The mood selected
          timestamp: Date; // When the mood was logged
        };
        ```

2.  **Create Motivational Quotes (`src/utils/quotes.ts`):**
    *   Create a new folder `src/utils`.
    *   Inside `src/utils`, create a file named `quotes.ts`.
    *   Add the following code:
        ```typescript
        // src/utils/quotes.ts
        import { Mood } from '../types/mood';

        type QuotesCollection = {
          [key in Mood]?: string[];
        } & { general: string[] };

        const quotes: QuotesCollection = {
          [Mood.Happy]: [
            "Keep shining, the world needs your light!", "Happiness is not by chance, but by choice.",
          ],
          [Mood.Sad]: [
            "This too shall pass. Tough times don't last, tough people do.", "It's okay not to be okay.",
          ],
          [Mood.Neutral]: [
            "Even a quiet day can be a good day.", "Find beauty in the ordinary.",
          ],
          [Mood.Excited]: [
            "Ride the wave of enthusiasm!", "Channel that energy into something amazing!",
          ],
          [Mood.Tired]: [
            "Rest is not idleness. It's a vital part of progress.", "Listen to your body.",
          ],
          general: [
            "Believe you can and you're halfway there.", "The best way to predict the future is to create it.",
          ],
        };

        export const getRandomQuote = (mood: Mood | null): string => {
          const moodQuotes = mood ? quotes[mood] : undefined;
          const availableQuotes = (moodQuotes && moodQuotes.length > 0) ? moodQuotes : quotes.general;
          return availableQuotes[Math.floor(Math.random() * availableQuotes.length)];
        };
        ```

---

### Step 2: Creating Theme Constants for Consistent Styling

**Why this step is important:**
A theme helps ensure visual consistency. By defining these values in one place, you can easily update them later. We'll create JavaScript constants that our `css.create()` calls will use.

1.  **Create Theme File (`src/styles/theme.ts`):**
    *   Create a new folder `src/styles`.
    *   Inside `src/styles`, create a file named `theme.ts`.
    *   Add the following code:
        ```typescript
        // src/styles/theme.ts
        export const theme = {
          primaryColor: '#007bff',
          secondaryColor: '#6c757d',
          textColorLight: '#ffffff',
          textColorDark: '#212529',
          backgroundColorPage: '#f4f7f9',
          happyColor: '#28a745',
          neutralColor: '#ffc107',
          sadColor: '#17a2b8',
          excitedColor: '#fd7e14',
          tiredColor: '#6f42c1',
          cardBackgroundColor: '#ffffff',
          borderColor: '#ced4da',
          lightGray: '#f8f9fa',
          mediumGray: '#6c757d',
          fontFamily: 'system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif',
          spacingXs: '4px',
          spacingSmall: '8px',
          spacingMedium: '16px',
          spacingLarge: '24px',
          spacingXl: '32px',
          borderRadiusSmall: '4px',
          borderRadiusMedium: '8px',
        } as const;
        ```

---

### Step 3: Building the `MoodSelector` Component

**Why this step is important:**
This component allows users to select a mood. We'll use `html.<element>`, define styles with `css.create()`, apply them with the `style` prop, handle clicks, and pass data to the parent.

1.  **Create Component File (`src/components/MoodSelector.tsx`):**
    *   Create `src/components` folder.
    *   Inside, create `MoodSelector.tsx`.
    *   Add:
        ```tsx
        // src/components/MoodSelector.tsx
        import React from 'react';
        import { html, css } from 'react-strict-dom';
        import { Mood } from '../types/mood';
        import { theme } from '../styles/theme';

        interface MoodSelectorProps {
          onMoodSelect: (mood: Mood) => void;
          currentMood: Mood | null;
        }

        const styles = css.create({
          container: {
            marginBottom: theme.spacingLarge,
            paddingTop: theme.spacingSmall,
          },
          title: {
            textAlign: 'center',
            color: theme.textColorDark,
            fontSize: '1.5rem',
            marginBottom: theme.spacingMedium,
            fontWeight: 500,
          },
          buttonContainer: {
            display: 'flex',
            gap: theme.spacingMedium,
            justifyContent: 'center',
            flexWrap: 'wrap',
          },
          moodButton: (currentButtonMood: Mood, isActive: boolean) => ({
            paddingTop: theme.spacingSmall,
            paddingBottom: theme.spacingSmall,
            paddingLeft: theme.spacingMedium,
            paddingRight: theme.spacingMedium,
            fontSize: '1rem',
            borderRadius: theme.borderRadiusMedium,
            borderWidth: '2px',
            borderStyle: 'solid',
            cursor: 'pointer',
            transitionProperty: 'transform, box-shadow, background-color, color',
            transitionDuration: '0.2s',
            transitionTimingFunction: 'ease-in-out',
            minWidth: '120px',
            textAlign: 'center',
            backgroundColor: isActive ? {
              [Mood.Happy]: theme.happyColor,
              [Mood.Neutral]: theme.neutralColor,
              [Mood.Sad]: theme.sadColor,
              [Mood.Excited]: theme.excitedColor,
              [Mood.Tired]: theme.tiredColor,
            }[currentButtonMood] : theme.cardBackgroundColor,
            color: isActive ? theme.textColorLight : {
              [Mood.Happy]: theme.happyColor,
              [Mood.Neutral]: theme.neutralColor,
              [Mood.Sad]: theme.sadColor,
              [Mood.Excited]: theme.excitedColor,
              [Mood.Tired]: theme.tiredColor,
            }[currentButtonMood],
            borderColor: {
              [Mood.Happy]: theme.happyColor,
              [Mood.Neutral]: theme.neutralColor,
              [Mood.Sad]: theme.sadColor,
              [Mood.Excited]: theme.excitedColor,
              [Mood.Tired]: theme.tiredColor,
            }[currentButtonMood],
            // Note: Complex :hover effects defined here might not be fully applied
            // by style={...}. For robust pseudo-classes, css.props() is standard.
            // A simple CSS :hover (e.g., changing opacity) might work via browser defaults
            // on the button element itself if not overridden.
          }),
        });

        const MoodSelector: React.FC<MoodSelectorProps> = ({ onMoodSelect, currentMood }) => {
          const moodOptions = Object.values(Mood);

          return (
            <html.div style={styles.container}> {/* Using style prop */}
              <html.h2 style={styles.title}>How are you feeling today?</html.h2> {/* Using style prop */}
              <html.div style={styles.buttonContainer}> {/* Using style prop */}
                {moodOptions.map((moodValue) => (
                  <html.button
                    key={moodValue}
                    style={styles.moodButton(moodValue, currentMood === moodValue)} // Using style prop
                    onClick={() => onMoodSelect(moodValue)}
                  >
                    {moodValue}
                  </html.button>
                ))}
              </html.div>
            </html.div>
          );
        };

        export default MoodSelector;
        ```

---

### Step 4: Building the `MoodLog` Component

**Why this step is important:**
This component displays mood history, showing how to render lists and format data.

1.  **Create Component File (`src/components/MoodLog.tsx`):**
    ```tsx
    // src/components/MoodLog.tsx
    import React from 'react';
    import { html, css } from 'react-strict-dom';
    import { MoodEntry, Mood } from '../types/mood';
    import { theme } from '../styles/theme';

    interface MoodLogProps {
      moodHistory: MoodEntry[];
    }

    const styles = css.create({
      container: {
        marginTop: theme.spacingLarge,
        padding: theme.spacingMedium,
        backgroundColor: theme.cardBackgroundColor,
        borderRadius: theme.borderRadiusMedium,
        boxShadow: '0 2px 4px rgba(0,0,0,0.05)',
        maxHeight: '300px',
        overflowY: 'auto',
      },
      title: {
        color: theme.textColorDark,
        marginTop: 0,
        marginBottom: theme.spacingMedium,
        borderBottomWidth: '1px',
        borderBottomStyle: 'solid',
        borderBottomColor: theme.borderColor,
        paddingBottom: theme.spacingSmall,
        fontSize: '1.25rem',
        fontWeight: 500,
      },
      list: {
        listStyle: 'none',
        padding: 0,
        margin: 0,
      },
      listItem: (itemMood: Mood) => ({
        paddingTop: theme.spacingSmall,
        paddingBottom: theme.spacingSmall,
        borderBottomWidth: '1px',
        borderBottomStyle: 'solid',
        borderBottomColor: theme.lightGray,
        display: 'flex',
        justifyContent: 'space-between',
        alignItems: 'center',
        color: {
          [Mood.Happy]: theme.happyColor,
          [Mood.Neutral]: theme.neutralColor,
          [Mood.Sad]: theme.sadColor,
          [Mood.Excited]: theme.excitedColor,
          [Mood.Tired]: theme.tiredColor,
        }[itemMood],
        // Note: :last-child behavior for removing border needs css.props() or manual JS logic.
      }),
      moodText: {
        fontWeight: 'bold',
        fontSize: '0.95rem',
      },
      timestampText: {
        fontSize: '0.85em',
        color: theme.mediumGray,
      },
      noMoodsMessage: {
        color: theme.mediumGray,
        textAlign: 'center',
        paddingTop: theme.spacingMedium,
        paddingBottom: theme.spacingMedium,
        fontStyle: 'italic',
      },
    });

    const MoodLog: React.FC<MoodLogProps> = ({ moodHistory }) => {
      if (moodHistory.length === 0) {
        return (
          <html.div style={styles.container}>
            <html.h3 style={styles.title}>Mood History</html.h3>
            <html.p style={styles.noMoodsMessage}>
              No moods logged yet. Select a mood above to start!
            </html.p>
          </html.div>
        );
      }

      return (
        <html.div style={styles.container}>
          <html.h3 style={styles.title}>Mood History</html.h3>
          <html.ul style={styles.list}>
            {moodHistory.slice().reverse().map((entry) => (
              <html.li key={entry.id} style={styles.listItem(entry.mood)}>
                <html.span style={styles.moodText}>{entry.mood}</html.span>
                <html.span style={styles.timestampText}>
                  {entry.timestamp.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })} -{' '}
                  {entry.timestamp.toLocaleDateString()}
                </html.span>
              </html.li>
            ))}
          </html.ul>
        </html.div>
      );
    };

    export default MoodLog;
    ```

---

### Step 5: Building the `MotivationalQuote` Component

**Why this step is important:**
This component uses `useEffect` for simulated data fetching and `useState` for local state. It also shows `css.keyframes()`.

1.  **Create Component File (`src/components/MotivationalQuote.tsx`):**
    ```tsx
    // src/components/MotivationalQuote.tsx
    import React, { useState, useEffect } from 'react';
    import { html, css } from 'react-strict-dom';
    import { Mood } from '../types/mood';
    import { getRandomQuote } from '../utils/quotes';
    import { theme } from '../styles/theme';

    interface MotivationalQuoteProps {
      currentMood: Mood | null;
    }

    const fadeInAnimation = css.keyframes({ // Define animation
      '0%': { opacity: 0, transform: 'translateY(10px)' },
      '100%': { opacity: 1, transform: 'translateY(0px)' },
    });

    const styles = css.create({
      container: {
        marginTop: theme.spacingLarge,
        paddingTop: theme.spacingMedium,
        paddingBottom: theme.spacingMedium,
        paddingLeft: theme.spacingLarge,
        paddingRight: theme.spacingLarge,
        backgroundColor: theme.textColorDark,
        color: theme.textColorLight,
        borderRadius: theme.borderRadiusMedium,
        textAlign: 'center',
        minHeight: '80px',
        display: 'flex',
        alignItems: 'center',
        justifyContent: 'center',
        boxShadow: '0 2px 6px rgba(0,0,0,0.1)',
      },
      quoteText: {
        fontStyle: 'italic',
        fontSize: '1.1em',
        margin: 0,
        // Animation properties are generally compatible with inline style prop
        animationName: fadeInAnimation,
        animationDuration: '0.5s',
        animationTimingFunction: 'ease-out',
      },
      loadingText: {
        color: theme.mediumGray,
        fontStyle: 'italic',
      },
    });

    const MotivationalQuote: React.FC<MotivationalQuoteProps> = ({ currentMood }) => {
      const [quote, setQuote] = useState<string>('');
      const [isLoading, setIsLoading] = useState<boolean>(true);

      useEffect(() => {
        setIsLoading(true);
        const quoteFetchTimeoutId = setTimeout(() => {
          setQuote(getRandomQuote(currentMood));
          setIsLoading(false);
        }, 700);
        return () => clearTimeout(quoteFetchTimeoutId);
      }, [currentMood]);

      return (
        <html.div style={styles.container}> {/* Using style prop */}
          {isLoading ? (
            <html.p style={styles.loadingText}>{/* Using style prop */}
                Finding the perfect words...
            </html.p>
          ) : (
            <html.p style={styles.quoteText}>{/* Using style prop */}
                "{quote}"
            </html.p>
          )}
        </html.div>
      );
    };

    export default MotivationalQuote;
    ```

---

### Step 6: Assembling the Application in `App.tsx`

**Why this step is important:**
The `App.tsx` component is the main container, managing overall state and rendering child components.

1.  **Modify `src/App.tsx`:**
    Replace its content with:
    ```tsx
    // src/App.tsx
    import React, { useState } from 'react';
    import { html, css } from 'react-strict-dom';
    import { Mood, MoodEntry } from './types/mood';
    import { theme } from './styles/theme';

    import MoodSelector from './components/MoodSelector';
    import MoodLog from './components/MoodLog';
    import MotivationalQuote from './components/MotivationalQuote';

    const appStyles = css.create({
      appContainer: {
        maxWidth: '700px',
        marginRight: 'auto',
        marginLeft: 'auto',
        marginTop: theme.spacingLarge,
        marginBottom: theme.spacingLarge,
        padding: theme.spacingLarge,
        backgroundColor: theme.cardBackgroundColor,
        borderRadius: theme.borderRadiusMedium,
        boxShadow: '0 4px 12px rgba(0, 0, 0, 0.1)',
      },
      appHeader: {
        color: theme.primaryColor,
        textAlign: 'center',
        marginBottom: theme.spacingXl,
        fontSize: '2.5rem',
        fontWeight: 'bold',
        letterSpacing: '-0.5px',
      },
    });

    function App() {
      const [currentMood, setCurrentMood] = useState<Mood | null>(null);
      const [moodHistory, setMoodHistory] = useState<MoodEntry[]>([]);

      const handleMoodSelect = (selectedMood: Mood) => {
        setCurrentMood(selectedMood);
        const newMoodEntry: MoodEntry = {
          id: new Date().toISOString() + Math.random(),
          mood: selectedMood,
          timestamp: new Date(),
        };
        setMoodHistory((prevHistory) => [...prevHistory, newMoodEntry].slice(-10));
      };

      return (
        <html.div style={appStyles.appContainer}> {/* Using style prop */}
          <html.h1 style={appStyles.appHeader}>🧪 Mood Tracker</html.h1> {/* Using style prop */}

          <MoodSelector onMoodSelect={handleMoodSelect} currentMood={currentMood} />
          <MotivationalQuote currentMood={currentMood} />
          <MoodLog moodHistory={moodHistory} />
        </html.div>
      );
    }

    export default App;
    ```

---

### Step 7: Running and Testing Your Mood Tracker

**Why this step is important:**
It's time to see your creation in action! Testing helps you find bugs and verify that features work as expected.

1.  **Start the Development Server (if it's not already running):**
    In your terminal, from the `mood-tracker` directory, run:
    ```bash
    npm run dev
    ```

2.  **Open Your Application in a Web Browser:**
    Your terminal will show a local URL (usually `http://localhost:5173/`). Open this URL in your browser.

3.  **Thoroughly Test All Features:**
    *   **Mood Selection:** Click on the mood buttons. Does the selected button highlight? Does the quote update? Does the log add an entry?
    *   **Mood Log:** Select several moods. Are they displayed correctly (newest first)? Is the 10-entry limit working?
    *   **Motivational Quotes:** Do quotes vary with moods? Is the loading message shown?
    *   **Styling and Layout:** Does the app look as intended? Is it reasonably responsive?

---

## 🎉 Congratulations! You've Built a Mood Tracker!

You have successfully created a complete React application using `react-strict-dom` for your UI elements and its `css` object for styling. You've practiced fundamental React concepts like components, props, state, and hooks, and learned how to set up a modern Vite project with TypeScript.

**Remember the Note on Styling:** While we used `style={...}` in this guide, if you encounter issues with complex styles like `:hover` or media queries not working, try switching to `css.props()`:
`<html.div {...css.props(styles.yourStyle)}>...</html.div>`. This is the standard way to leverage all of StyleX's capabilities.

**Possible Next Steps & Challenges (Optional):**

*   **Persistence:** Use `localStorage` to save mood history.
*   **Data Visualization:** Add a simple chart for mood frequency.
*   **Edit/Delete Log Entries.**
*   **Advanced Theming:** Explore `stylex.defineVars` for CSS Custom Property-based theming.
*   **Accessibility (a11y) Review.**

Keep building, keep learning, and don't be afraid to experiment!
