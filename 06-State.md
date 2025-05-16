# 🌟 What is state in React?

 State is a local, mutable data store inside a component
that determines how the component behaves or renders.
When the state changes → the component automatically re-renders.

<br />

**🔑 Key points about state:**
Lives inside the component (not passed from parent)
Mutable → you can update it using:
useState() in functional components
this.setState() in class components
Controls dynamic behavior (like toggles, counters, form inputs)


**💥 Example of state:**
```
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
}
```
Here, count is state → when you click the button, setCount updates it, and React re-renders the component.
