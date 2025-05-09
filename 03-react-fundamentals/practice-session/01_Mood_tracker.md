## 🧪 Practical Project 1: **Mood Tracker**

### 🧭 Project Objective:

Build a simple **Mood Tracker** where users can select their current mood (Happy, Sad, Neutral, etc.), view a log of recent moods, and see a motivational quote based on their mood.

---

### ✅ Concepts Reinforced:

| Concept               | Application                                                                |
| --------------------- | -------------------------------------------------------------------------- |
| **React Concepts**    | Functional components, composition, component structure                    |
| **JSX**               | UI structure using JSX syntax                                              |
| **Props**             | Pass mood data and callbacks to child components                           |
| **State**             | Track current mood and mood history                                        |
| **React Strict DOM**  | All components are written using `html.deiv`, `html.p`, etc.         |
| **Styled Components** | Component-level styling with props-based styles                            |
| **Hooks**             | `useState` (for mood tracking), `useEffect` (for motivational quote fetch) |

---

### 🛠 Project Features

1. **MoodSelector**

   * Lets the user select from mood options like 🙂 😐 🙁
   * Uses props to pass selected mood to parent

2. **MoodLog**

   * Shows a log of previous moods with timestamps

3. **MotivationalQuote**

   * Displays a motivational quote fetched from a static list based on the selected mood (simulated fetch with `useEffect`)

---

### 📁 File Structure Proposal

```
/mood-tracker/
├── App.tsx
├── components/
│   ├── MoodSelector.tsx
│   ├── MoodLog.tsx
│   └── MotivationalQuote.tsx
├── styles/
│   └── theme.ts
├── types/
│   └── mood.ts
└── utils/
    └── quotes.ts
```

---

### 💡 New Concepts to Introduce

* **Type aliases/enums** in `types/mood.ts` for mood types
* **Props with types** for reusable components
* **Simulated async logic** using `setTimeout` inside `useEffect` (to mimic a quote fetch)

---
