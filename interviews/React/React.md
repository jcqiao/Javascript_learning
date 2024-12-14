## Have you worked with React

Yes I worked with react so far since 2019

## What's the pure component in React?

A **Pure Component** in React is a component that uses a shallow comparison of its props and state to decide whether to re-render. If the props or state haven’t changed, it skips re-rendering, improving performance. However, since the comparison is shallow, it might miss updates to complex objects or arrays if their references don't change—so you need to manage state and props carefully.

Nowadays, Pure Components are less commonly used directly because functional components paired with **React.memo** and hooks like **useMemo** and **useCallback** offer similar or better optimization. However, they remain useful in class-based components or older projects. Pure Components help make apps faster by preventing unnecessary renders, but it's important to use them wisely!

For example, when a parent component re-renders, React will re-run all its child components by default. However, if you use React.memo for function components or PureComponent for class components, you can avoid unnecessary child re-renders. On the other hand, if a child re-renders, it won’t trigger a re-render of the parent unless it explicitly changes the parent’s state, like through a callback.

In short, Pure Components are a great way to optimize performance, especially in class-based components, but in modern React, React.memo is often the go-to tool for this purpose.

## What's the ERROR BOUNDARY COMPONENT and what is it used for and why do we have it?

An Error Boundary Component is used in React to catch JavaScript errors in its child components during rendering, lifecycle methods, or in constructors. It helps you limit the impact of errors by localizing them.

For example, if a component fetching data encounters an error, wrapping it in an error boundary ensures the error doesn’t throw up and crash the entire app. Instead, the error boundary can display a fallback UI, like “Something went wrong.”

This makes your app more predictable and user-friendly, as it prevents layout shifts or a complete app crash, especially in cases where server or data errors might otherwise break the UI. Error boundaries improve the overall stability of your app.

## Are you familiar with useEffect hook

The useEffect hook in React is used to perform side effects in a functional component. Side effects are tasks like updating the DOM, fetching data, or interacting with APIs. For instance, if you change a state variable and need to call an analytics system or update local storage, useEffect is the right tool to handle that. The advantages like seperating and efficiently manage the side effects from the main logic and keep the component cleaner and more focus on rendering. And it has flexible dependencies management.

However, when useEffect was first introduced, many developers, including myself, used it too broadly. For example, we might trigger an effect every time a state variable changes, which could cause unnecessary re-renders. Since useEffect runs after the component renders, it can trigger another re-render, leading to performance issues if overused.

One of the challenges is that, by default, re-renders in a parent component will trigger re-renders in child components as well, unless you optimize with hooks like useMemo or useCallback.

So, while useEffect is powerful, it’s important to use it carefully to avoid performance bottlenecks caused by unnecessary re-renders.

## Why can't we use an async function as a callback to useEffect

useEffect expects its callback to return a cleanup function or undefined. Cleanup functions are used to handle things like unsubscribing from an event or canceling a timer when the component unmounts or the effect re-runs.

An async function, on the other hand, always returns a promise, even if you don't explicitly return one. Promises are not functions and cannot be used as cleanup logic. React would not know how to handle the promise as a return value, which is why it disallows the use of async functions directly in useEffect.

## What's the best solution to handle State Management in React and why?

The best solution for state management in React really depends on the type of state you're working with and the requirements of your app. From my experience, I manage state differently based on its purpose:

Backend data: I usually keep backend data in the local component state if it’s only used by that component. If it needs to be shared between two or three components, I lift it up to a common parent. Yes, this might involve some prop drilling, but for small-scale data sharing, it’s manageable and keeps things simple.

Authentication state: Authentication needs to be globally accessible since many components might rely on user information or permissions. For this, I find React Context to be a great solution because it can broadcast state across the entire component tree effectively.

Global settings or complex state transitions: If you have non-trivial state transitions, like handling user settings that impact multiple parts of the app (e.g., a premium user vs. a standard user), you might need something more robust. In such cases, I use a state management library like Redux or Recoil, or even a state machine, depending on the complexity. These tools are excellent for handling global states with clear and predictable state transitions.

So, my approach is to distribute state management based on the type of data and its scope, which keeps the app organized and efficient.

## What is the difference between essential and derived state

In React, essential state refers to the core data that your application directly depends on and controls, like user input, API responses, or application settings. This state is typically managed using hooks like useState or state management libraries, and it's the source of truth in your component.

Derived state, on the other hand, is data that can be computed or inferred from the essential state and does not need to be stored separately. For example, if you have a list of items in your essential state, a derived state might be a filtered version of that list. Since derived state can always be recalculated from the essential state, storing it separately is unnecessary and can lead to bugs, like data getting out of sync.

The key takeaway is: only store the minimal essential state in React, and compute derived state on-the-fly to keep your app's logic clean and predictable.

## What's the disadvantage of placing state in React.context

One major disadvantage of using React Context for state management is that when the state changes, all components that consume the context will re-render. This can lead to performance issues, especially if the context is managing state that frequently changes or if it's being consumed by many components.

To mitigate this, it's a good practice to:

Keep the state as close to where it's used as possible.
Split state into multiple contexts if different parts of the application need to consume independent pieces of state. This minimizes unnecessary re-renders by ensuring that only the components that depend on a specific piece of state are affected.
In general, lifting state too far up the component tree, whether in context or elsewhere, can make it harder to manage and optimize rendering. Context is powerful but should be used carefully for global or shared state.

```javascript
import React, { createContext, useContext, useState } from "react";

// Create a single context
const AppContext = createContext();

function App() {
  const [user, setUser] = useState({ name: "John Doe" });
  const [theme, setTheme] = useState("light");

  return (
    <AppContext.Provider value={{ user, setUser, theme, setTheme }}>
      <UserProfile />
      <ThemeSwitcher />
    </AppContext.Provider>
  );
}
```

optimized

```javascript
const UserContext = createContext();
const ThemeContext = createContext();

function App() {
  const [user, setUser] = useState({ name: "John Doe" });
  const [theme, setTheme] = useState("light");

  return (
    <UserContext.Provider value={{ user, setUser }}>
      <ThemeContext.Provider value={{ theme, setTheme }}>
        <UserProfile />
        <ThemeSwitcher />
      </ThemeContext.Provider>
    </UserContext.Provider>
  );
}
```
