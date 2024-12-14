## Here's a more complete example to prevent unnecessary state updates:

### Derived State Without Updates

```js
function Example() {
  const [count, setCount] = useState(0);
  const [doubleCount, setDoubleCount] = useState(count * 2); // Derived state
  // fixed
  const doubleCount = count * 2; // Always up-to-date

  const increment = () => {
    setCount(count + 1);
    // Forgetting to update doubleCount here
  };

  return (
    <div>
      <p>Count: {count}</p>
      <p>Double Count: {doubleCount}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

### Race Conditions or Asynchronous Updates

```javascript
function Example() {
  const [data, setData] = useState({ items: [], timestamp: 0 });

  const fetchData = async () => {
    const response = await fetch("/api/data");
    const result = await response.json();
    setData(result); // State might be out of sync if multiple fetches are triggered
    // fixed
    setData((prevData) => {
      if (result.timestamp > prevData.timestamp) {
        return result; // Update only if newer
      }
      return prevData; // Do not update if not newer
    });
  };

  useEffect(() => {
    fetchData();
  }, []);

  return (
    <ul>
      {data.items.map((item) => (
        <li key={item.id}>{item.name}</li>
      ))}
    </ul>
  );
}
```
