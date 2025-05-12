---
title: CSS Theming
description: Light and dark theming with CSS Modules in React
layout: default
nav_order: 15
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/css-theming/
---
# 📚 Light/Dark Mode with CSS Modules

This tutorial teaches you how to:

1. Build a light/dark mode toggle using `useState` and CSS Modules
2. Understand and solve prop drilling using React Context

---

## ✅ Part 1: Light/Dark Mode using CSS Modules and `useState`

### 1. Project Setup

```bash
npm create vite@latest theme-toggle-demo --template react
cd theme-toggle-demo
npm install
npm run dev
```

### 2. Folder Structure

```plaintext
src/
├── App.jsx
├── App.module.css
├── ThemeToggle.jsx
├── ThemeToggle.module.css
```

### 3. `App.module.css`

```css
.app {
  font-family: sans-serif;
  padding: 2rem;
  min-height: 100vh;
  transition: background-color 0.3s, color 0.3s;
}

.light {
  background-color: #ffffff;
  color: #000000;
}

.dark {
  background-color: #1e1e1e;
  color: #f5f5f5;
}
```

### 4. `ThemeToggle.module.css`

```css
.button {
  padding: 0.5rem 1rem;
  border: 2px solid currentColor;
  background: transparent;
  color: inherit;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
}
```

### 5. `ThemeToggle.jsx`

```jsx
import styles from './ThemeToggle.module.css';

export default function ThemeToggle({ theme, toggleTheme }) {
  return (
    <button className={styles.button} onClick={toggleTheme}>
      Switch to {theme === 'light' ? 'Dark' : 'Light'} Mode
    </button>
  );
}
```

### 6. `App.jsx`

```jsx
import { useState } from 'react';
import styles from './App.module.css';
import ThemeToggle from './ThemeToggle';

function App() {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () => {
    setTheme((prev) => (prev === 'light' ? 'dark' : 'light'));
  };

  return (
    <div className={`${styles.app} ${styles[theme]}`}>
      <h1>Hello React</h1>
      <p>This app has a light/dark mode toggle using CSS Modules.</p>
      <ThemeToggle theme={theme} toggleTheme={toggleTheme} />
    </div>
  );
}

export default App;
```

---

## ⚠️ Problem: Prop Drilling

What if you need the `theme` in many nested components? Passing props through many layers becomes messy.

```jsx
<App>
  <Header theme={theme} />
    <Navbar theme={theme} />
      <UserMenu theme={theme} />
```

This is called **prop drilling**.

---

## 🔧 Part 2: Solving Prop Drilling with `useContext`

### 1. Create a context file `ThemeContext.jsx`

```jsx
import { createContext, useContext, useState } from 'react';

const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  const toggleTheme = () => {
    setTheme((prev) => (prev === 'light' ? 'dark' : 'light'));
  };

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

export function useTheme() {
  return useContext(ThemeContext);
}
```

### 2. Wrap your app in `ThemeProvider`

Edit `main.jsx`:

```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import { ThemeProvider } from './ThemeContext';

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <ThemeProvider>
      <App />
    </ThemeProvider>
  </React.StrictMode>
);
```

### 3. Use context in `App.jsx`

```jsx
import styles from './App.module.css';
import ThemeToggle from './ThemeToggle';
import { useTheme } from './ThemeContext';

function App() {
  const { theme } = useTheme();

  return (
    <div className={`${styles.app} ${styles[theme]}`}>
      <h1>Hello React</h1>
      <ThemeToggle />
    </div>
  );
}

export default App;
```

### 4. Update `ThemeToggle.jsx`

```jsx
import styles from './ThemeToggle.module.css';
import { useTheme } from './ThemeContext';

export default function ThemeToggle() {
  const { theme, toggleTheme } = useTheme();

  return (
    <button className={styles.button} onClick={toggleTheme}>
      Switch to {theme === 'light' ? 'Dark' : 'Light'} Mode
    </button>
  );
}
```

---

## 🚀 Summary

* CSS Modules keep styles **scoped** to each component.
* `useState` can toggle themes simply, but prop drilling becomes an issue.
* `useContext` is a clean and scalable way to share state across the app without manually passing props.

---
