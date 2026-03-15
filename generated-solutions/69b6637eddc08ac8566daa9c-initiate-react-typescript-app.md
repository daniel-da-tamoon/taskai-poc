```typescript
/**
 * Project Structure:
 * - .env                : Environment variables configuration
 * - vite.config.ts      : Vite configuration for port handling
 * - src/main.tsx        : Application entry point
 * - src/App.tsx         : Root component
 * - src/env.d.ts        : TypeScript definitions for environment variables
 * - package.json        : Project scripts and dependencies
 */

// --- .env ---
/*
PORT=3333
*/

// --- vite.config.ts ---
import { defineConfig, loadEnv } from 'vite';
import react from '@vitejs/plugin-react';

/**
 * Vite configuration to handle dynamic PORT from .env
 * TODO: Add support for HTTPS if required by the environment
 */
export default defineConfig(({ mode }) => {
  // Load env file based on `mode` in the current working directory.
  const env = loadEnv(mode, process.cwd(), '');

  return {
    plugins: [react()],
    server: {
      // Set the port from .env or default to 3333
      port: parseInt(env.PORT) || 3333,
    },
  };
});

// --- src/env.d.ts ---
/**
 * Type definitions for Vite environment variables
 */
interface ImportMetaEnv {
  readonly PORT: string;
  // TODO: Add other environment variable types here
}

interface ImportMeta {
  readonly env: ImportMetaEnv;
}

// --- src/App.tsx ---
import React from 'react';

/**
 * Main Application Component
 */
const App: React.FC = () => {
  return (
    <div className="app-container">
      <h1>React TypeScript Template</h1>
      <p>Running on port: {import.meta.env.PORT || '3333'}</p>
      {/* TODO: Implement base routing and layout components */}
    </div>
  );
};

export default App;

// --- src/main.tsx ---
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

/**
 * Mounting the React application to the DOM
 */
const rootElement = document.getElementById('root');

if (rootElement) {
  ReactDOM.createRoot(rootElement).render(
    <React.StrictMode>
      <App />
    </React.StrictMode>
  );
} else {
  // TODO: Implement fallback or error logging for missing root element
  console.error('Failed to find the root element');
}

// --- package.json (Partial) ---
/*
{
  "name": "react-ts-template",
  "private": true,
  "version": "0.1.0",
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "@types/react": "^18.2.0",
    "@types/react-dom": "^18.2.0",
    "@vitejs/plugin-react": "^4.0.0",
    "typescript": "^5.0.0",
    "vite": "^4.0.0"
  }
}
*/
```