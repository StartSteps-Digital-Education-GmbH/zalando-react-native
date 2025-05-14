### ✅ **Step 1: Create a New Project Directory**

```bash
mkdir my-typescript-project
cd my-typescript-project
```

---

### ✅ **Step 2: Initialize a New `package.json`**

```bash
npm init -y
```

This creates a `package.json` file with default values.

---

### ✅ **Step 3: Install TypeScript as a Dev Dependency**

```bash
npm install --save-dev typescript
```

---

### ✅ **Step 4: Create a TypeScript Configuration File**

```bash
npx tsc --init
```

This creates a `tsconfig.json` file. Now edit it to support **ES6 syntax and modules**:

#### `tsconfig.json` recommended settings:

```json
{
  "compilerOptions": {
    "target": "ES6",                         // Support ES6 features
    "module": "ES6",                         // Use ES6 module syntax
    "moduleResolution": "node",              // Resolve modules using Node's algorithm
    "outDir": "./dist",                      // Output directory for compiled JS
    "rootDir": "./src",                      // Root directory of your TS source
    "strict": true,                          // Enable all strict type-checking options
    "esModuleInterop": true,                 // Allow default imports from CommonJS modules
    "forceConsistentCasingInFileNames": true,
    "skipLibCheck": true
  },
  "include": ["src"],
  "exclude": ["node_modules"]
}
```

---

### ✅ **Step 5: Create Your Project Structure**

```bash
mkdir src
touch src/index.ts
```

Now write a sample file with ES6 features (e.g., arrow functions, imports):

#### `src/index.ts`

```ts
import { greet } from "./utils";

const name = "World";

console.log(greet(name));
```

#### `src/utils.ts`

```ts
export const greet = (name: string): string => {
  return `Hello, ${name}!`;
};
```

---

### ✅ **Step 6: Add Build and Start Scripts**

In your `package.json`, under `"scripts"`, add:

```json
"scripts": {
  "build": "tsc",
  "start": "node dist/index.js"
}
```

---

### ✅ **Step 7: Build the Project**

```bash
npm run build
```

This compiles TypeScript from `src/` into JavaScript in the `dist/` folder.

---

### ✅ **Step 8: Run the Compiled Code**

```bash
npm start
```

Expected output:

```
Hello, World!
```

---

### ✅ Optional: Add a `.gitignore` and `.eslint` (if needed)

#### `.gitignore`

```
node_modules/
dist/
```

