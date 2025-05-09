**Prerequisites:**
*   Node.js and npm (or yarn) installed.
*   A code editor (like VS Code).

---

**Step 0: Project Setup and Dependency Installation**

1.  **Create Vite Project:**
    Open your terminal and run:
    ```bash
    npm create vite@latest mood-tracker -- --template react-ts
    ```
    This creates a new directory `mood-tracker` with a React + TypeScript project.

2.  **Navigate to Project Directory:**
    ```bash
    cd mood-tracker
    ```

3.  **Install Dependencies:**
    We need `styled-components` for styling and `react-strict-dom` as per your requirement.
    ```bash
    npm install styled-components react-strict-dom
    npm install --save-dev @types/styled-components
    ```

4.  **Initialize Git (Optional but Recommended):**
    ```bash
    git init
    git add .
    git commit -m "Initial project setup with Vite, React, TS, Styled Components, React Strict DOM"
    ```

5.  **Run the Development Server:**
    ```bash
    npm run dev
    ```
    Open your browser to the local address shown (usually `http://localhost:5173/`). You should see the default Vite React page.

---

**Step 1: Define Types and Utility Data**

1.  **Create `types/mood.ts`:**
    This file will define our mood types.
    *   Create the directory: `mkdir -p src/types`
    *   Create the file: `src/types/mood.ts`

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
      id: string; // For unique key in lists
      mood: Mood;
      timestamp: Date;
    };
    ```
    *   **Explanation:**
        *   `Mood`: An enum to represent the different selectable moods. Using string values makes them more readable.
        *   `MoodEntry`: A type alias for an object that will store a mood selection along with its timestamp and a unique ID.

2.  **Create `utils/quotes.ts`:**
    This file will hold our static list of motivational quotes.
    *   Create the directory: `mkdir -p src/utils`
    *   Create the file: `src/utils/quotes.ts`

    ```typescript
    // src/utils/quotes.ts
    import { Mood } from '../types/mood';

    type QuotesCollection = {
      [key in Mood]?: string[]; // Optional arrays for moods that might not have specific quotes
    } & { general: string[] }; // Mandatory general quotes

    const quotes: QuotesCollection = {
      [Mood.Happy]: [
        "Keep shining, the world needs your light!",
        "Happiness is not by chance, but by choice.",
        "The most wasted of days is one without laughter.",
      ],
      [Mood.Sad]: [
        "This too shall pass. Tough times don't last, tough people do.",
        "It's okay not to be okay. Reach out if you need to.",
        "Every storm runs out of rain.",
      ],
      [Mood.Neutral]: [
        "Even a quiet day can be a good day.",
        "Find beauty in the ordinary.",
        "Take a deep breath and center yourself.",
      ],
      [Mood.Excited]: [
        "Ride the wave of enthusiasm!",
        "Channel that energy into something amazing!",
        "Let your excitement fuel your passion!",
      ],
      [Mood.Tired]: [
        "Rest is not idleness. It's a vital part of progress.",
        "Listen to your body; it knows what it needs.",
        "Recharge so you can come back stronger.",
      ],
      general: [
        "Believe you can and you're halfway there.",
        "The best way to predict the future is to create it.",
        "You are stronger than you think.",
      ],
    };

    export const getRandomQuote = (mood: Mood | null): string => {
      const moodQuotes = mood ? quotes[mood] : undefined;
      const availableQuotes = moodQuotes && moodQuotes.length > 0 ? moodQuotes : quotes.general;
      return availableQuotes[Math.floor(Math.random() * availableQuotes.length)];
    };
    ```
    *   **Explanation:**
        *   `QuotesCollection`: A type for our quotes object, mapping each `Mood` to an array of strings, plus a `general` category.
        *   `quotes`: The actual collection of quotes.
        *   `getRandomQuote`: A function that takes a mood (or null) and returns a random quote, falling back to general quotes if specific ones aren't available or if no mood is selected.

---

**Step 2: Setup Basic Styling Theme**

1.  **Create `styles/theme.ts`:**
    This file will define a basic theme for `styled-components`.
    *   Create the directory: `mkdir -p src/styles`
    *   Create the file: `src/styles/theme.ts`

    ```typescript
    // src/styles/theme.ts
    export const theme = {
      colors: {
        primary: '#61dafb', // React blue
        secondary: '#282c34', // Dark background
        text: '#ffffff',
        textDark: '#333333',
        background: '#f0f2f5',
        happy: '#4CAF50', // Green
        neutral: '#FFC107', // Amber
        sad: '#2196F3', // Blue
        excited: '#FF5722', // Deep Orange
        tired: '#795548', // Brown
        lightGray: '#e0e0e0',
        mediumGray: '#9e9e9e',
      },
      spacing: {
        small: '8px',
        medium: '16px',
        large: '24px',
      },
      borderRadius: '4px',
      fontFamily: 'Arial, sans-serif',
    };

    export type ThemeType = typeof theme; // Exporting the theme type for styled-components
    ```
    *   **Explanation:**
        *   Defines common colors, spacing units, etc., for consistent styling.
        *   `ThemeType` is exported to help with type inference in styled components.

2.  **Create `styled.d.ts` for `styled-components` TypeScript support:**
    This is a declaration file that tells TypeScript about your theme structure.
    *   Create the file: `src/styled.d.ts` (in the `src` root)

    ```typescript
    // src/styled.d.ts
    import 'styled-components';
    import { ThemeType } from './styles/theme'; // Adjust path if your theme.ts is elsewhere

    declare module 'styled-components' {
      export interface DefaultTheme extends ThemeType {}
    }
    ```
    *   **Explanation:** This extends the `DefaultTheme` interface from `styled-components` with our custom `ThemeType`.

---

**Step 3: Create the `MoodSelector` Component**

1.  **Create `components/MoodSelector.tsx`:**
    *   Create the directory: `mkdir -p src/components`
    *   Create the file: `src/components/MoodSelector.tsx`

    ```tsx
    // src/components/MoodSelector.tsx
    import React from 'react';
    import styled from 'styled-components';
    import { html } from 'react-strict-dom';
    import { Mood } from '../types/mood';

    interface MoodSelectorProps {
      onMoodSelect: (mood: Mood) => void;
    }

    const MoodButtonContainer = styled(html.div)`
      display: flex;
      gap: ${(props) => props.theme.spacing.medium};
      margin-bottom: ${(props) => props.theme.spacing.large};
      justify-content: center;
      flex-wrap: wrap; /* Allow buttons to wrap on smaller screens */
    `;

    const StyledMoodButton = styled(html.button)<{ moodtype: Mood }>`
      padding: ${(props) => props.theme.spacing.small} ${(props) => props.theme.spacing.medium};
      font-size: 1rem;
      border-radius: ${(props) => props.theme.borderRadius};
      border: 2px solid transparent;
      cursor: pointer;
      transition: all 0.2s ease-in-out;
      background-color: #fff;
      color: ${(props) => {
        switch (props.moodtype) {
          case Mood.Happy: return props.theme.colors.happy;
          case Mood.Neutral: return props.theme.colors.neutral;
          case Mood.Sad: return props.theme.colors.sad;
          case Mood.Excited: return props.theme.colors.excited;
          case Mood.Tired: return props.theme.colors.tired;
          default: return props.theme.colors.textDark;
        }
      }};
      border-color: ${(props) => {
        switch (props.moodtype) {
          case Mood.Happy: return props.theme.colors.happy;
          case Mood.Neutral: return props.theme.colors.neutral;
          case Mood.Sad: return props.theme.colors.sad;
          case Mood.Excited: return props.theme.colors.excited;
          case Mood.Tired: return props.theme.colors.tired;
          default: return props.theme.colors.mediumGray;
        }
      }};

      &:hover {
        transform: translateY(-2px);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        background-color: ${(props) => {
          switch (props.moodtype) {
            case Mood.Happy: return props.theme.colors.happy;
            case Mood.Neutral: return props.theme.colors.neutral;
            case Mood.Sad: return props.theme.colors.sad;
            case Mood.Excited: return props.theme.colors.excited;
            case Mood.Tired: return props.theme.colors.tired;
            default: return props.theme.colors.lightGray;
          }
        }};
        color: ${(props) => props.theme.colors.text};
      }

      &:active {
        transform: translateY(0);
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      }
    `;

    const MoodSelector: React.FC<MoodSelectorProps> = ({ onMoodSelect }) => {
      const moods = Object.values(Mood); // Get all enum values

      return (
        <html.div>
          <html.h2 style={{ textAlign: 'center', color: '#333' }}>How are you feeling today?</html.h2>
          <MoodButtonContainer>
            {moods.map((mood) => (
              <StyledMoodButton
                key={mood}
                moodtype={mood} // Pass moodtype for styling
                onClick={() => onMoodSelect(mood)}
              >
                {mood}
              </StyledMoodButton>
            ))}
          </MoodButtonContainer>
        </html.div>
      );
    };

    export default MoodSelector;
    ```
    *   **Explanation:**
        *   Imports `React`, `styled`, `html` from `react-strict-dom`, and `Mood` enum.
        *   `MoodSelectorProps`: Defines that this component expects an `onMoodSelect` callback function.
        *   `MoodButtonContainer` and `StyledMoodButton`: Styled components using `html.div` and `html.button` respectively. Note the use of `styled(html.button)` which is crucial for `react-strict-dom`.
        *   The `StyledMoodButton` receives a `moodtype` prop to dynamically set its colors based on the theme.
        *   The component maps over all `Mood` enum values to create a button for each.
        *   When a button is clicked, it calls the `onMoodSelect` prop with the selected mood.

---

**Step 4: Create the `MoodLog` Component**

1.  **Create `components/MoodLog.tsx`:**
    *   File: `src/components/MoodLog.tsx`

    ```tsx
    // src/components/MoodLog.tsx
    import React from 'react';
    import styled from 'styled-components';
    import { html } from 'react-strict-dom';
    import { MoodEntry, Mood } from '../types/mood';

    interface MoodLogProps {
      moodHistory: MoodEntry[];
    }

    const LogContainer = styled(html.div)`
      margin-top: ${(props) => props.theme.spacing.large};
      padding: ${(props) => props.theme.spacing.medium};
      background-color: #fff;
      border-radius: ${(props) => props.theme.borderRadius};
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
      max-height: 300px;
      overflow-y: auto;
    `;

    const LogTitle = styled(html.h3)`
      color: ${(props) => props.theme.colors.secondary};
      margin-top: 0;
      margin-bottom: ${(props) => props.theme.spacing.medium};
      border-bottom: 1px solid ${(props) => props.theme.colors.lightGray};
      padding-bottom: ${(props) => props.theme.spacing.small};
    `;

    const LogList = styled(html.ul)`
      list-style: none;
      padding: 0;
      margin: 0;
    `;

    const LogItem = styled(html.li)<{ mood: Mood }>`
      padding: ${(props) => props.theme.spacing.small} 0;
      border-bottom: 1px solid ${(props) => props.theme.colors.lightGray};
      display: flex;
      justify-content: space-between;
      align-items: center;
      color: ${(props) => {
        switch (props.mood) {
          case Mood.Happy: return props.theme.colors.happy;
          case Mood.Neutral: return props.theme.colors.neutral;
          case Mood.Sad: return props.theme.colors.sad;
          case Mood.Excited: return props.theme.colors.excited;
          case Mood.Tired: return props.theme.colors.tired;
          default: return props.theme.colors.textDark;
        }
      }};

      &:last-child {
        border-bottom: none;
      }
    `;

    const MoodText = styled(html.span)`
      font-weight: bold;
    `;

    const TimestampText = styled(html.span)`
      font-size: 0.9em;
      color: ${(props) => props.theme.colors.mediumGray};
    `;

    const MoodLog: React.FC<MoodLogProps> = ({ moodHistory }) => {
      if (moodHistory.length === 0) {
        return (
          <LogContainer>
            <LogTitle>Mood History</LogTitle>
            <html.p style={{ color: '#555' }}>No moods logged yet. Select a mood above to start!</html.p>
          </LogContainer>
        );
      }

      return (
        <LogContainer>
          <LogTitle>Mood History</LogTitle>
          <LogList>
            {moodHistory.slice().reverse().map((entry) => ( // Show newest first
              <LogItem key={entry.id} mood={entry.mood}>
                <MoodText>{entry.mood}</MoodText>
                <TimestampText>
                  {entry.timestamp.toLocaleTimeString()} - {entry.timestamp.toLocaleDateString()}
                </TimestampText>
              </LogItem>
            ))}
          </LogList>
        </LogContainer>
      );
    };

    export default MoodLog;
    ```
    *   **Explanation:**
        *   Takes `moodHistory` (an array of `MoodEntry`) as a prop.
        *   Displays "No moods logged yet" if the history is empty.
        *   Otherwise, it maps over `moodHistory` (reversed to show newest first) and renders each entry.
        *   `toLocaleTimeString()` and `toLocaleDateString()` are used to format the timestamp.
        *   Styled components are used for the container, list, and items, again using `html.<tag>`.
        *   `LogItem` is styled based on the `mood` prop.

---

**Step 5: Create the `MotivationalQuote` Component**

1.  **Create `components/MotivationalQuote.tsx`:**
    *   File: `src/components/MotivationalQuote.tsx`

    ```tsx
    // src/components/MotivationalQuote.tsx
    import React, { useState, useEffect } from 'react';
    import styled from 'styled-components';
    import { html } from 'react-strict-dom';
    import { Mood } from '../types/mood';
    import { getRandomQuote } from '../utils/quotes';

    interface MotivationalQuoteProps {
      currentMood: Mood | null;
    }

    const QuoteContainer = styled(html.div)`
      margin-top: ${(props) => props.theme.spacing.large};
      padding: ${(props) => props.theme.spacing.medium};
      background-color: ${(props) => props.theme.colors.secondary};
      color: ${(props) => props.theme.colors.text};
      border-radius: ${(props) => props.theme.borderRadius};
      text-align: center;
      min-height: 80px; /* Ensure container doesn't jump too much during load */
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: 0 2px 4px rgba(0,0,0,0.2);
    `;

    const QuoteText = styled(html.p)`
      font-style: italic;
      font-size: 1.1em;
      margin: 0;
    `;

    const LoadingText = styled(html.p)`
      color: ${(props) => props.theme.colors.mediumGray};
      font-style: italic;
    `;

    const MotivationalQuote: React.FC<MotivationalQuoteProps> = ({ currentMood }) => {
      const [quote, setQuote] = useState<string>('');
      const [isLoading, setIsLoading] = useState<boolean>(true);

      useEffect(() => {
        setIsLoading(true);
        // Simulate an API call
        const fetchQuote = () => {
          setTimeout(() => {
            setQuote(getRandomQuote(currentMood));
            setIsLoading(false);
          }, 700); // Simulate network delay
        };

        fetchQuote();
      }, [currentMood]); // Re-fetch quote when currentMood changes

      return (
        <QuoteContainer>
          {isLoading ? (
            <LoadingText>Finding the perfect words...</LoadingText>
          ) : (
            <QuoteText>"{quote}"</QuoteText>
          )}
        </QuoteContainer>
      );
    };

    export default MotivationalQuote;
    ```
    *   **Explanation:**
        *   Takes `currentMood` as a prop.
        *   Uses `useState` to store the `quote` string and an `isLoading` flag.
        *   Uses `useEffect` to "fetch" a new quote:
            *   This effect runs when `currentMood` changes.
            *   `setTimeout` simulates an asynchronous API call.
            *   It calls `getRandomQuote` from `utils/quotes.ts` based on the `currentMood`.
            *   Updates the `quote` state.
        *   Displays a loading message while the "fetch" is in progress.

---

**Step 6: Assemble in `App.tsx`**

1.  **Modify `src/App.tsx`:**
    Replace the contents of `src/App.tsx` with the following:

    ```tsx
    // src/App.tsx
    import React, { useState } from 'react';
    import styled, { ThemeProvider, createGlobalStyle } from 'styled-components';
    import { html } from 'react-strict-dom';
    import { theme } from './styles/theme';
    import { Mood, MoodEntry } from './types/mood';
    import MoodSelector from './components/MoodSelector';
    import MoodLog from './components/MoodLog';
    import MotivationalQuote from './components/MotivationalQuote';

    const GlobalStyle = createGlobalStyle`
      body {
        margin: 0;
        font-family: ${(props) => props.theme.fontFamily};
        background-color: ${(props) => props.theme.colors.background};
        color: ${(props) => props.theme.colors.textDark};
        line-height: 1.6;
      }

      * {
        box-sizing: border-box;
      }
    `;

    const AppContainer = styled(html.div)`
      max-width: 700px;
      margin: ${(props) => props.theme.spacing.large} auto;
      padding: ${(props) => props.theme.spacing.large};
      background-color: white;
      border-radius: 8px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    `;

    const AppHeader = styled(html.h1)`
      color: ${(props) => props.theme.colors.primary};
      text-align: center;
      margin-bottom: ${(props) => props.theme.spacing.large};
      font-size: 2.5em;
    `;

    function App() {
      const [currentMood, setCurrentMood] = useState<Mood | null>(null);
      const [moodHistory, setMoodHistory] = useState<MoodEntry[]>([]);

      const handleMoodSelect = (mood: Mood) => {
        setCurrentMood(mood);
        const newEntry: MoodEntry = {
          id: new Date().toISOString() + Math.random(), // Simple unique ID
          mood: mood,
          timestamp: new Date(),
        };
        setMoodHistory((prevHistory) => [...prevHistory, newEntry]);
      };

      return (
        <ThemeProvider theme={theme}>
          <GlobalStyle />
          <AppContainer>
            <AppHeader>🧪 Mood Tracker</AppHeader>
            <MoodSelector onMoodSelect={handleMoodSelect} />
            <MotivationalQuote currentMood={currentMood} />
            <MoodLog moodHistory={moodHistory} />
          </AppContainer>
        </ThemeProvider>
      );
    }

    export default App;
    ```
    *   **Explanation:**
        *   Imports necessary components, types, theme, and `react-strict-dom`'s `html`.
        *   `GlobalStyle`: Injects global CSS styles using `styled-components`.
        *   `AppContainer` and `AppHeader`: Styled components for the main layout.
        *   **State:**
            *   `currentMood`: Stores the currently selected mood (or `null`).
            *   `moodHistory`: An array to store all `MoodEntry` objects.
        *   `handleMoodSelect`:
            *   This function is passed as a prop to `MoodSelector`.
            *   When a mood is selected, it updates `currentMood`.
            *   It creates a new `MoodEntry` with the selected mood and current timestamp.
            *   It appends this new entry to the `moodHistory` state.
        *   **Composition:**
            *   Wraps the entire application in `ThemeProvider` to provide the theme to all styled components.
            *   Renders `MoodSelector`, `MotivationalQuote`, and `MoodLog`, passing down the necessary state and callbacks as props.

2.  **Modify `src/main.tsx` (if necessary, usually fine by default):**
    Ensure it looks like this:

    ```tsx
    // src/main.tsx
    import React from 'react'
    import ReactDOM from 'react-dom/client'
    import App from './App.tsx'
    // import './index.css' // You can remove this if GlobalStyle handles all base styles

    ReactDOM.createRoot(document.getElementById('root')!).render(
      <React.StrictMode>
        <App />
      </React.StrictMode>,
    )
    ```
    You might have an `index.css` file created by Vite. If `GlobalStyle` in `App.tsx` covers all your base styling needs (like body margin, font-family), you can remove the `import './index.css'` line and delete the `src/index.css` file. Otherwise, keep it for any Vite-default or other global styles you want to preserve.

---

**Step 7: Run and Test**

1.  If your development server isn't running, start it:
    ```bash
    npm run dev
    ```
2.  Open your browser to the local address.
3.  **Test Features:**
    *   Click on mood buttons in `MoodSelector`.
        *   Verify the `MotivationalQuote` updates (with a slight delay) based on the selected mood.
        *   Verify the `MoodLog` shows the newly selected mood with a timestamp.
    *   Select multiple moods and see the log populate.
    *   Check the styling and responsiveness (though we haven't focused heavily on advanced responsiveness here).

---

This detailed guide should get your Mood Tracker project up and running, reinforcing all the concepts you outlined and introducing the new ones, all while adhering to the `react-strict-dom` requirement for HTML elements!