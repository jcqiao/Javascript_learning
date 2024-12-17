## Have you worked with React

Yes I worked with react so far since 2019

## What's the React

React is a JavaScript library developed by Facebook for building user interfaces, particularly for single-page applications. It uses a component-based architecture to create modular and reusable code, making it easier to build and maintain complex UIs. React's declarative approach lets developers focus on what the UI should look like, while the Virtual DOM, a lightweight representation of the real DOM, improves performance by efficiently updating only the neccessary changes in real DOM . It also follows a unidirectional data flow, which makes state management predictable and debugging easier.

### Components

Components are the building blocks of React applications, representing reusable pieces of UI like buttons, inputs, or even entire pages. In React, a component is essentially a JavaScript function that returns JSX, a syntax similar to HTML but with JavaScript capabilities. Unlike static HTML, JSX allows you to embed dynamic values using curly braces. Components make it easy to break an application into smaller, manageable parts, promoting reusability and consistency.

### Key props

The key prop in React is used to help React identify and differentiate components, especially when rendering lists. It provides a unique identifier for each component or element in a list, allowing React to efficiently track changes such as additions, removals, or reordering of items. Ensure proper updates and avoid unnecessary re-renders.

### Why react uses classname instead of class

As we know, React is a javascript libary and components are functions return jsx. To avoid conflicts or errors with HTML, React uses className, which works seamlessly in JSX while still representing the same thing as the class attribute in regular HTML.

### How does rendering work

Rendering in React revolves around the Virtual DOM, which is essentially a JavaScript object representing the structure of the UI. As we know, components return JSX which is converted into this Virtual DOM by Babel.

When state or props change, React creates a new Virtual DOM tree to represent the updated UI. It then compares the new tree with the old one using a diffing algorithm to identify the differences. The algorithm is based on two key assumptions:

- Different element types builds different trees.
- The key prop is crucial for efficiently identifying list items.

This comparison process is called 'Reconciliation.' After detecting changes, React calculates the minimal set of updates required to modify the real DOM, such as adding, updating, or removing elements. It also optimizes performance by batching updates to avoid unnecessary re-renders.

Finally, in the commit phase, React applies the calculated updates to the real DOM, and the browser reflects these changes on the screen.

## What's the pure component in React?

A **Pure Component** in React is a component that uses a shallow comparison of its props and state to decide whether to re-render. If the props or state haven’t changed, it skips re-rendering, improving performance. However, since the comparison is shallow, it might miss updates to complex objects or arrays if their references don't change—so you need to manage state and props carefully.

Nowadays, Pure Components are less commonly used directly because functional components paired with **React.memo** and hooks like **useMemo** and **useCallback** offer similar or better optimization. However, they remain useful in class-based components or older projects. Pure Components help make apps faster by preventing unnecessary renders, but it's important to use them wisely!

For example, when a parent component re-renders, React will re-run all its child components by default. However, if you use React.memo for function components or PureComponent for class components, you can avoid unnecessary child re-renders. On the other hand, if a child re-renders, it won’t trigger a re-render of the parent unless it explicitly changes the parent’s state, like through a callback.

In short, Pure Components are a great way to optimize performance, especially in class-based components, but in modern React, React.memo is often the go-to tool for this purpose.

## What's the pure functions in React?

In React, pure functions are just functions that always give the same output if you give them the same input, and they don’t mess with anything outside of themselves. They don’t change variables, make API calls, or touch the DOM—they’re predictable and self-contained.

For example:

```javascript
function add(a, b) {
  return a + b;
}
```

This is a pure function because if you give it the numbers 2 and 3, it’ll always return 5. It doesn’t depend on anything else, and it doesn’t change anything outside itself.

Pure functions are important in React because:

- They’re predictable: It’s easy to understand and debug them since their behavior is consistent.
- They help with performance: Skipping unnecessary updates when nothing changes with React.memo. For example, with React.memo, you can make a component re-render only when its props change.

In short, pure functions keep things clean, predictable, and efficient, which fits perfectly with React’s philosophy of building maintainable UI.

### What's the side effects in React

In React, side effects refer to any operations or actions that affect something outside the component’s scope, such as:

- Fetching data from an API
- Updating the DOM manually
- Setting up event listeners
- Modifying global variables
- Interacting with third-party libraries

### What's the Suspense Component and why we need it

The Suspense component in React is a special tool that helps manage loading states for things like fetching data or lazy-loading components. It improves the user experience by allowing you to show something like a loading spinner or a placeholder while waiting for content to load. Ikt makes your app feel more polished and seamless by handling delays in rendering without showing a blank screen.

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
