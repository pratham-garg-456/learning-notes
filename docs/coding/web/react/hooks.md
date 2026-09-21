---
title: Hooks
---

# Hooks

## What are React Hooks/

Hooks let you “hook into” React state and lifecycle features from function components. The most commonly used hooks are:

1. **useState**: Lets you add state to a functional component.
2. **useEffect**: Lets you perform side effects (like data fetching, subscriptions, etc.) in your function components.
3. **useContext**: Lets you access the value of a React context.
4. **useRef**: Lets you persist values across renders without causing re-renders.
5. **useMemo** and **useCallback**: Optimize performance by memoizing values or functions.
6. **Custom Hooks**: You can create your own hooks by combining existing ones.

### useState

Allows you to add state to a function component.

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // 0 is the initial state

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

### **useEffect**

Allows you to perform side effects in function components (like fetching data, updating the DOM, timers, etc.).

```jsx
import React, { useState, useEffect } from "react";

function GithubUser({ username }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetch(`https://api.github.com/users/${username}`)
      .then(res => res.json())
      .then(setUser);
  }, [username]); // Re-run when username changes

  if (!user) return <div>Loading...</div>;
  return (
    <div>
      <img src={user.avatar_url} width={60} alt="avatar" />
      <p>{user.name}</p>
      <p>{user.public_repos} Repos</p>
    </div>
  );
}
```

- The second argument `[count]` is a dependency array. The effect runs whenever `count` changes.

### **useContext**

Access the value from a React context.

```jsx
import React, { useContext } from "react";

const ThemeContext = React.createContext("light");

function ThemeButton() {
  const theme = useContext(ThemeContext);
  return (
    <button style={{
      background: theme === "dark" ? "#222" : "#fff",
      color: theme === "dark" ? "#fff" : "#222"
    }}>
      I am styled by theme context!
    </button>
  );
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <ThemeButton />
    </ThemeContext.Provider>
  );
}
```

### useRef

Keeps a mutable value that does not cause a re-render when updated. Useful for accessing DOM elements directly.

```jsx
function MyComponent() {
  const inputRef = React.useRef();

  function focusInput() {
    inputRef.current.focus();
  }

  return (
    <div>
      <input ref={inputRef} />
      <button onClick={focusInput}>Focus the input</button>
    </div>
  );
}
```

### **useMemo and useCallback**

- `useMemo`: Memoizes a computed value.
- `useCallback`: Memoizes a function.

```jsx
import React, { useState, useMemo } from "react";

function ExpensiveComponent({ num }) {
  // Only recalculates when num changes
  const factorial = useMemo(() => {
    function fact(n) {
      return n <= 1 ? 1 : n * fact(n - 1);
    }
    return fact(num);
  }, [num]);

  return <div>Factorial of {num}: {factorial}</div>;
}

function App() {
  const [number, setNumber] = useState(5);
  return (
    <div>
      <input
        type="number"
        value={number}
        onChange={e => setNumber(Number(e.target.value))}
      />
      <ExpensiveComponent num={number} />
    </div>
  );
}
```

```jsx
import React, { useState, useCallback } from "react";

function Child({ onButtonClick }) {
  return <button onClick={onButtonClick}>Click me!</button>;
}

function Parent() {
  const [count, setCount] = useState(0);

  // useCallback prevents unnecessary re-renders of Child
  const handleClick = useCallback(() => {
    setCount(c => c + 1);
  }, []);

  return (
    <div>
      <Child onButtonClick={handleClick} />
      <p>Clicked {count} times</p>
    </div>
  );
}
```

### **Custom Hooks**

You can create your own hooks by combining built-in hooks.

```jsx
import { useState } from "react";

// Save state to localStorage and read back on page reload
function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    const stored = localStorage.getItem(key);
    return stored !== null ? JSON.parse(stored) : initialValue;
  });

  const setAndStore = newValue => {
    setValue(newValue);
    localStorage.setItem(key, JSON.stringify(newValue));
  };

  return [value, setAndStore];
}

// Usage
function PersistentInput() {
  const [name, setName] = useLocalStorage("name", "");
  return (
    <input
      value={name}
      onChange={e => setName(e.target.value)}
      placeholder="Type your name"
    />
  );
}
```

## Practice Questions

??? question "1. What are React Hooks?"

    Functions that let you hook into React state and lifecycle features from function components.

??? question "2. What does useState do?"

    It adds state to a function component. It returns the current value and a setter, for example `const [count, setCount] = useState(0)`.

??? question "3. What does the dependency array in useEffect do?"

    The effect re-runs only when a value in the array changes. Passing `[username]` re-fetches when `username` changes.

??? question "4. What is useRef for?"

    Keeping a mutable value that does not cause a re-render when updated, and accessing DOM elements directly (for example focusing an input).

??? question "5. What is the difference between useMemo and useCallback?"

    `useMemo` memoizes a computed value, and `useCallback` memoizes a function.

??? question "6. What does useContext do?"

    It reads the value from a React context, such as a theme provided by a `Provider` higher up the tree.
