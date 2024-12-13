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

We can't use an async function directly because useEffect expects the callback to return a cleanup function or undefined. However, an async function always returns a promise, which doesn’t fit this expectation. React doesn't know how to handle a promise for cleanup.

To handle async logic in useEffect, you can define the async function inside the effect and call it, instead of returning it directly. This way, useEffect can still return a cleanup function properly.
