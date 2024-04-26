
1. **Automatic Batching**
	1. React 18 extends the concept of batching beyond just React event handlers to include promises, `setTimeout`, and native event handlers.
```jsx
// In a React component
function MyComponent() {
  const [count, setCount] = useState(0);
  const [flag, setFlag] = useState(false);

  useEffect(() => {
    fetch("/api/data").then(() => {
      // These updates will be batched automatically in React 18
      setCount(c => c + 1);
      setFlag(f => !f);
    });
  }, []);

  // rest of the component
}

```

2. **Concurrency in React**

3. **Transitions**
	1. Transitions let you differentiate between urgent updates and those that can be deferred, like loading new content.
```jsx
import { useState, useTransition } from 'react';

function FilterComponent() {
  const [input, setInput] = useState('');
  const [data, setData] = useState([]);
  const [isPending, startTransition] = useTransition();

  function handleChange(e) {
    setInput(e.target.value);
    startTransition(() => {
      const filteredData = fetchData(e.target.value); // Assume fetchData is a function that fetches data based on input
      setData(filteredData);
    });
  }

  return (
    <div>
      <input type="text" value={input} onChange={handleChange} />
      {isPending ? "Loading..." : data.map(/* render your data */)}
    </div>
  );
}

```

4. **Suspense Enhancements**
	1. React 18 extends the use of Suspense to data fetching, allowing you to specify a fallback UI while waiting for data.
```jsx
import { Suspense } from 'react';

function MyComponent() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <DataFetchingComponent />
    </Suspense>
  );
}

function DataFetchingComponent() {
  const data = fetchData(); // fetchData uses React 18 Suspense internally
  return <div>{data}</div>;
}

```

5. **New Client and Server Rendering APIs**
```jsx
import { createRoot } from 'react-dom/client';

const container = document.getElementById('app');
const root = createRoot(container);
root.render(<App />);

```

6. **Strict Mode Enhancements**

7. **New Hooks**
```jsx
import { useId } from 'react';

function MyComponent() {
  const id = useId();
  return (
    <div>
      <label htmlFor={id}>Label</label>
      <input id={id} />
    </div>
  );
}

```