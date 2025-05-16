# What is a Functional Component in React?
A functional component is a plain JavaScript (or TypeScript) function that returns JSX to render part of the UI.

It’s the simplest way to write a React component — no classes, no this, just a function.

## Q1: How to create functional components?
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




# 🌟 What is a Class Component in React?
A class component is a JavaScript class that extends React.Component and returns JSX to render the UI.

Before React introduced hooks in v16.8, class components were the main way to manage state and use lifecycle methods.

## Q1: How to create class components?
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

## ⚙ When to use class components?
<li>In legacy codebases that already use classes.</li>
<li>When you need to use old lifecycle methods.</li>
<li>But in modern React, functional components with hooks are now the recommended way.</li>


<br />

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