# What is a Functional Component in React?
A functional component is a plain JavaScript (or TypeScript) function that returns JSX to render part of the UI.

It’s the simplest way to write a React component — no classes, no this, just a function.

✅ Example of a functional component:
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
Or using ES6 arrow functions:

```
const Welcome = ({ name }) => {
  return <h1>Hello, {name}</h1>;
};
```
You can then use it like:
```<Welcome name="John" />```

## 🔑 Key characteristics
✅ It’s just a function that:
<li>Takes props as an argument.</li>
<li>Returns JSX.</li>
✅ It has no state or lifecycle methods by default — but… <br>
✅ With React Hooks (useState, useEffect), functional components can manage state and side effects, making them just as powerful as class components.

<br />
<br />

**Q1: How to create functional components?
Q2: How to pass props to the components?**


# 🌟 What is a Class Component in React?
A class component is a JavaScript class that extends React.Component and returns JSX to render the UI.

Before React introduced hooks in v16.8, class components were the main way to manage state and use lifecycle methods.

✅ Basic example:
```
import React, { Component } from 'react';

class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
Usage:
```
<Welcome name="John" />
```
## 🔑 Key features of class components
✅ Extends React.Component
You must extend the React.Component class.

✅ Has a render() method
Inside the class, you must define a render() method that returns JSX.

✅ Can hold state
Class components can have local state:
```
class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  render() {
    return <p>Count: {this.state.count}</p>;
  }
}
```
✅ Can use lifecycle methods
Class components can define lifecycle methods like:
componentDidMount()
componentDidUpdate()
componentWillUnmount()

Example:
```
componentDidMount() {
  console.log('Component mounted!');
}
```

### ⚙ When to use class components?
<li>In legacy codebases that already use classes.</li>
<li>When you need to use old lifecycle methods.</li>
<li>But in modern React, functional components with hooks are now the recommended way.</li>


<br />

**Q1: How to create class components?
Q2: How to pass props to class components?
Q3: How state is working in class components?**


# ⚡ Difference between Functional Components vs Class Components

| Feature               | Functional Component                     | Class Component                                             |
| --------------------- | ---------------------------------------- | ----------------------------------------------------------- |
| **Definition**        | Plain JavaScript function                | ES6 class that extends `React.Component`                    |
| **Syntax**            | Simpler, shorter                         | More boilerplate code                                       |
| **State handling**    | Uses `useState` and other hooks          | Uses `this.state` and `this.setState()`                     |
| **Props access**      | Passed as function argument (`props`)    | Accessed with `this.props`                                  |
| **Lifecycle methods** | Uses hooks like `useEffect`              | Uses methods like `componentDidMount`, `componentDidUpdate` |
| **‘this’ keyword**    | No `this` needed                         | Requires `this` to access props, state                      |
| **Performance**       | Slightly faster and less memory overhead | Slightly heavier (due to class structure)                   |
| **Recommended use**   | Recommended in modern React apps         | Mostly legacy or special cases                              |


**✅ Example: Functional component**
```
import React, { useState, useEffect } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log('Mounted or updated');
  }, [count]);

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
};
```

✅ Example: Class component
```
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  componentDidMount() {
    console.log('Mounted');
  }

  componentDidUpdate() {
    console.log('Updated');
  }

  render() {
    return (
      <>
        <p>Count: {this.state.count}</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Increment
        </button>
      </>
    );
  }
}
```

### 🔑 Summary
✅ Use functional components + hooks in almost all modern React projects.
✅ Class components are mainly used in older codebases or when working with legacy libraries.
✅ Functional components are easier to test, read, and maintain.

# 🌟 What are props in React?
 Props (short for “properties”) are read-only inputs passed from a parent component to a child component.
They let you configure and reuse components.

**🔑 Key points about props:**
Passed from parent to child (<Child name="John" />)
Immutable inside the child → you can’t change props in the child
Accessible as:
<li>props argument in functional components
<li>this.props in class components
Help make components reusable and dynamic

<br />
<br />

**💥 Example of props:**
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

<Welcome name="John" />
```
Here, the name prop is passed into the Welcome component → it renders Hello, John.

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

# 🌟 What is event handling in React?
In React, event handling means writing code that responds to user actions like:

Clicking a button

Typing in an input

Submitting a form

Moving the mouse

Pressing a key

<br />
React uses a special synthetic event system that wraps around the browser’s native events to ensure consistent behavior across all browsers.

<br /> 
<br />

✅ How to handle events in React
1️⃣ Write a handler function (can be inline or separate)
2️⃣ Attach it to an element using onClick, onChange, onSubmit, etc.

**💥 Example: Button click**
```
function MyButton() {
  function handleClick() {
    alert('Button was clicked!');
  }

  return <button onClick={handleClick}>Click me</button>;
}
```

✅ onClick={handleClick} attaches the handler
✅ When the button is clicked → the function runs

<br />

**⚡With inline arrow function**
```
<button onClick={() => alert('Clicked!')}>Click me</button>
```
### 🔑 Key points
✅ Use camelCase for event names → onClick, onChange (not onclick)
✅ You pass a function reference, not the function call → onClick={handleClick} (❌ don’t do onClick={handleClick()})
✅ You can access the event object like this:
```
function handleClick(event) {
  console.log(event);  // Synthetic event object
}
```
