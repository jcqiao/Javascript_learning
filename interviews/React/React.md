## Have you worked with React

Yes I worked with react so far since 2019

## What's the pure component in React

A **Pure Component** in React is a component that uses a shallow comparison of its props and state to decide whether to re-render. If the props or state haven’t changed, it skips re-rendering, improving performance. However, since the comparison is shallow, it might miss updates to complex objects or arrays if their references don't change—so you need to manage state and props carefully.

Nowadays, Pure Components are less commonly used directly because functional components paired with **React.memo** and hooks like **useMemo** and **useCallback** offer similar or better optimization. However, they remain useful in class-based components or older projects. Pure Components help make apps faster by preventing unnecessary renders, but it's important to use them wisely!

For example, when a parent component re-renders, React will re-run all its child components by default. However, if you use React.memo for function components or PureComponent for class components, you can avoid unnecessary child re-renders. On the other hand, if a child re-renders, it won’t trigger a re-render of the parent unless it explicitly changes the parent’s state, like through a callback.

In short, Pure Components are a great way to optimize performance, especially in class-based components, but in modern React, React.memo is often the go-to tool for this purpose.
