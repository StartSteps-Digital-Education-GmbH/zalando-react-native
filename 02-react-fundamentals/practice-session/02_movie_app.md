# Practical Project Guide 2: Build a Movie Search App

**Stack:** React + TypeScript + React Strict DOM  
**Duration:** 1 practical session (4 hours)  
**Skills:** JSX, functional components, props, state (`useState`), side-effects (`useEffect`), event handling, conditional rendering, list rendering, RSD’s `html` & `css` APIs.

---

## Step 1: Scaffold & Configure Your Project

1. **Create** a new React+TS app with Vite:  
   ```bash
   npm create vite@latest movie-search -- --template react-ts
   cd movie-search
   npm install
   ```  
2. **Add** React Strict DOM:  
   ```bash
   npm install react-strict-dom
   ```  
3. **Configure** your bundler (Vite) to alias `react-dom` and `react-native` to RSD where needed—follow RSD’s “Getting Started” guide on their homepage.  
4. **Import** RSD’s base CSS reset (if provided) or include your global styles before any component.

> **Hint:** Check the RSD README for the exact Vite plugin or alias configuration.

---

## Step 2: Plan Your Component Structure

Organize under `src/`:

```
src/
├─ App.tsx
├─ services/
│  └─ movieApi.ts         # Encapsulate OMDB fetch logic
└─ components/
   ├─ SearchBar.tsx      # html.form, html.input, html.button
   ├─ MovieCard.tsx      # html.div, html.img, html.span
   └─ MovieList.tsx      # html.div grid of MovieCards
```

> **Hint:** Keep `movieApi.ts` free of UI concerns—only fetch, parse, and type-map your API data.

---

## Step 3: Build the SearchBar Component

- **Use** RSD’s `html.form`, `html.input`, `html.button`.  
- **Manage** a controlled input with `value` and `onChange` props.  
- **On submit**, prevent default, then call an `onSearch()` callback.  
- **Style** with `css.create`, defining base styles and a `:focus` or `:hover` variant for the button.

> **Hint:** Wrap everything in a single RSD form element so that pressing Enter triggers submit.

---

## Step 4: Build the MovieCard Subcomponent

- **Receive** a `movie` prop with `title`, `year`, `posterUrl`.  
- **Render**:
  - An image (`html.img`) or placeholder (`html.div`) when no poster.  
  - A title (`html.span`) and year (`html.span`).  
- **Use** `css.create` to define:
  - A container with border, radius and shadow.  
  - Image sizing and `objectFit` fallback.  
  - Text styles for title vs. year.

> **Hint:** Conditional rendering inside RSD elements works exactly like React DOM—use a ternary or logical AND.

---

## Step 5: Build the MovieList Component

- **Accept** a `movies: Movie[]` prop.  
- **If** `movies` is empty, render a “No results” message via `html.div`.  
- **Else**, render a grid container (`html.div`) that maps each movie to `<MovieCard key={…} />`.  
- **Grid** styling via `css.create`—define responsive columns using media queries in your style object.

> **Hint:** Leverage RSD’s atomic CSS extraction on web and inline styles on native without writing platform-specific code.

---

## Step 6: Encapsulate API Calls in `movieApi.ts`

- **Export** a `searchMovies(query: string): Promise<Movie[]>` function.  
- **Fetch** from OMDB using `fetch()`; build the URL with your `VITE_OMDB_API_KEY`.  
- **Check** `response.ok` and the API’s `Error` field.  
- **Map** the raw JSON to your `Movie` type, rejecting on failures.

> **Hint:** Use `import.meta.env.VITE_OMDB_API_KEY` and `encodeURIComponent(query)` for safety.

---

## Step 7: Wire Everything in `App.tsx`

1. **Import** RSD’s `html` & `css`, React hooks, your components, and `searchMovies`.  
2. **State**:
   - `searchTerm` (string)  
   - `query` (string)  
   - `movies` (Movie[])  
   - `loading` (boolean)  
   - `error` (string | null)  
3. **Event**:  
   - `handleSearch()` sets `query = searchTerm.trim()` if nonempty.  
4. **Effect**:
   - `useEffect` watches `[query]`, toggles `loading`, clears `error`, calls `searchMovies`, then updates `movies`/`error`/`loading`.  
5. **Render**:
   - Outer container: `html.div` styled for max-width and centering.  
   - `<SearchBar …/>` always visible.  
   - Conditionally render:
     - `html.div` “Loading…”
     - `html.div` error message in red
     - `<MovieList movies={movies}/>`
   - Use early returns or inline ternaries for clarity.

> **Hint:** Use RSD’s `css.create` for container styles and any error/warning variants.

---

## Step 8: Enhance & Polish

- **Validation**: Disable the search button when `searchTerm` is empty—use RSD’s `disabled` prop and styling variant.  
- **Debounce**: Wrap `handleSearch` in a `useCallback` with a timeout to prevent rapid API calls.  
- **Theming**: Replace hard-coded colors with your design tokens via RSD’s CSS API (e.g. `{ default: '$primary', ':hover': '$primaryDark' }`).  
- **Accessibility**: Ensure all `html.*` elements include `aria-label`, `alt`, and keyboard focus styles.

> **Hint:** RSD’s strict HTML components automatically enforce valid props—mistyped or unsupported attributes will trigger a type error.

---

- Verify TypeScript compiles with `tsc --noEmit`.  
- Run the app and manually test searching, empty queries, no-results, and error scenarios.  

Good luck!