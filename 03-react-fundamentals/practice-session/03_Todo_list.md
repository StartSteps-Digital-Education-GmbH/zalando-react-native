 **Todo List** app using **React + TypeScript + React Strict DOM**


In this guide you will:

1. Create a React+TS project with Vite  
2. Install and configure React Strict DOM (RSD)  
3. Implement pages, components, and subcomponents using RSD’s `html` and `css` APIs  
4. Use `useState` for local state and `useEffect` for lifecycle side-effects  
5. Persist todos via `localStorage`

---

## 1. Project Initialization

### 1.1 Scaffold with Vite  
```bash
npm create vite@latest todo-app -- --template react-ts
cd todo-app
npm install
```
This bootstraps a React+TypeScript project with Vite’s fast HMR .

### 1.2 Install React Strict DOM  
```bash
npm install react-strict-dom
```
RSD provides strict HTML primitives and CSS-in-JS for web/native parity .

### 1.3 Configure Vite for RSD  
**vite.config.ts**  
```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  resolve: {
    alias: {
      'react-dom': 'react-strict-dom'
    }
  }
});
```
Aliasing ensures all `react-dom` imports use RSD under the hood .

### 1.4 Entry Point: main.tsx  
**src/main.tsx**  
```tsx
import 'react-strict-dom/reset.css';
import ReactDOM from 'react-dom';
import React from 'react';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```
Import RSD’s CSS reset before your app mounts .

---

## 2. Application Root

### 2.1 App.tsx  
**src/App.tsx**  
```tsx
import React from 'react';
import Home from './pages/Home';

export function App() {
  return <Home />;
}

export default App;
```
Entrypoint renders the `Home` page .

---

## 3. Data Persistence Service

### 3.1 todoService.ts  
**src/services/todoService.ts**  
```ts
export interface Todo {
  id: number;
  title: string;
  completed: boolean;
}

const STORAGE_KEY = 'todo_app';

export function loadTodos(): Todo[] {
  const json = localStorage.getItem(STORAGE_KEY);
  return json ? JSON.parse(json) : [];
}

export function saveTodos(todos: Todo[]) {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(todos));
}
```
Uses `localStorage` API to persist state across reloads .

---

## 4. Home Page

### 4.1 Home.tsx  
**src/pages/Home.tsx**  
```tsx
import React, { useState, useEffect } from 'react';
import { html, css } from 'react-strict-dom';
import TodoList from '../components/TodoList';
import AddTodoForm from '../components/AddTodoForm';
import { loadTodos, saveTodos, Todo } from '../services/todoService';

const pageStyles = css.create({
  container: {
    maxWidth: '600px',
    margin: '2rem auto',
    padding: '1rem'
  },
  heading: {
    fontSize: '2rem',
    marginBottom: '1rem'
  }
});

export default function Home() {
  const [todos, setTodos] = useState<Todo[]>([]);
  const [loading, setLoading] = useState(true);

  // Load on mount
  useEffect(() => {
    setTodos(loadTodos());
    setLoading(false);
  }, []); // empty deps → run once on mount 

  // Save whenever todos change (after initial load)
  useEffect(() => {
    if (!loading) saveTodos(todos);
  }, [todos, loading]); // watch both 

  const addTodo = (title: string) =>
    setTodos([...todos, { id: Date.now(), title, completed: false }]);

  const toggleTodo = (id: number) =>
    setTodos(
      todos.map(t =>
        t.id === id ? { ...t, completed: !t.completed } : t
      )
    );

  return (
    <html.div style={pageStyles.container}>
      <html.h1 style={pageStyles.heading}>Todo List</html.h1>
      <AddTodoForm onAdd={addTodo} />
      {loading ? (
        <html.div>Loading…</html.div>
      ) : (
        <TodoList todos={todos} onToggle={toggleTodo} />
      )}
    </html.div>
  );
}
```
- **useState** manages `todos` and `loading` .  
- **useEffect** for load/save lifecycles .

---

## 5. Components

### 5.1 AddTodoForm.tsx  
**src/components/AddTodoForm.tsx**  
```tsx
import React, { useState } from 'react';
import { html, css } from 'react-strict-dom';

const formStyles = css.create({
  form: {
    display: 'flex',
    gap: '0.5rem',
    marginBottom: '1rem'
  },
  input: {
    flex: 1,
    padding: '0.5rem',
    border: '1px solid #ccc',
    borderRadius: '0.25rem'
  },
  button: {
    padding: '0.5rem 1rem',
    backgroundColor: '#0070f3',
    color: 'white',
    border: 'none',
    borderRadius: '0.25rem',
    cursor: 'pointer'
  }
});

interface AddTodoFormProps {
  onAdd: (title: string) => void;
}

export default function AddTodoForm({ onAdd }: AddTodoFormProps) {
  const [value, setValue] = useState('');

  return (
    <html.form
      style={formStyles.form}
      onSubmit={e => {
        e.preventDefault(); // prevent page reload 
        if (value.trim()) {
          onAdd(value.trim());
          setValue('');
        }
      }}
    >
      <html.input
        style={formStyles.input}
        type="text"
        placeholder="Add new todo"
        value={value}
        onChange={e => setValue(e.currentTarget.value)}
      />
      <html.button style={formStyles.button} type="submit">
        Add
      </html.button>
    </html.form>
  );
}
```
Controlled form component, uses `html.form`, `html.input`, `html.button` .

### 5.2 TodoList.tsx  
**src/components/TodoList.tsx**  
```tsx
import React from 'react';
import { html, css } from 'react-strict-dom';
import TodoItem from './TodoItem';
import { Todo } from '../services/todoService';

const listStyles = css.create({
  list: {
    listStyle: 'none',
    padding: 0,
    margin: 0
  }
});

interface TodoListProps {
  todos: Todo[];
  onToggle: (id: number) => void;
}

export default function TodoList({ todos, onToggle }: TodoListProps) {
  if (todos.length === 0) {
    return <html.div>No todos yet</html.div>;
  }
  return (
    <html.ul style={listStyles.list}>
      {todos.map(todo => (
        <TodoItem key={todo.id} todo={todo} onToggle={onToggle} />
      ))}
    </html.ul>
  );
}
```
Renders a semantic list of `TodoItem` subcomponents .

### 5.3 TodoItem.tsx  
**src/components/TodoItem.tsx**  
```tsx
import React from 'react';
import { html, css } from 'react-strict-dom';
import { Todo } from '../services/todoService';

const itemStyles = css.create({
  item: {
    display: 'flex',
    alignItems: 'center',
    padding: '0.5rem',
    borderBottom: '1px solid #eee'
  },
  checkbox: {
    marginRight: '0.5rem'
  },
  title: {
    flex: 1
  },
  completed: {
    textDecoration: 'line-through',
    color: '#999'
  }
});

interface TodoItemProps {
  todo: Todo;
  onToggle: (id: number) => void;
}

export default function TodoItem({ todo, onToggle }: TodoItemProps) {
  return (
    <html.li style={itemStyles.item}>
      <html.input
        style={itemStyles.checkbox}
        type="checkbox"
        checked={todo.completed}
        onChange={() => onToggle(todo.id)}
      />
      <html.span
        style={todo.completed ? itemStyles.completed : itemStyles.title}
      >
        {todo.title}
      </html.span>
    </html.li>
  );
}
```
Handles event binding and conditional styling via RSD styles .

---

## 6. Run & Verify

```bash
npm run dev
```

- Navigate to `http://localhost:5173`  
- Add, toggle, and refresh todos—data persists via `localStorage`  
- Inspect elements to see `html.*` tags and generated atomic CSS classes

---