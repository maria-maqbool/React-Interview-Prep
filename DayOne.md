
# What is jsx? how babel compiles it?
JSX (JavaScript XML) is a syntax extension for JavaScript used in React.

It lets you write HTML-like code inside JavaScript.

**Example:**
```const element = <h1>Hello, World!</h1>;```

**Without JSX, you would write:**
```const element = React.createElement('h1', null, 'Hello, World!');```

So, JSX makes your React code more readable and expressive by letting you write UI markup directly inside JS.

**JSX and React are two separate things. They’re often used together, but you can use them independently of each other. JSX is a syntax extension, while React is a JavaScript library.**

**Important: Browsers cannot understand JSX directly — that’s where Babel comes in.**

**Q1: What is JSX?
Q2: Is JSX a part of React?
Q3: Why can't we write class inside our JSX markup**

## How does Babel compile JSX?
Babel is a JavaScript compiler that converts modern JavaScript (ES6+) and JSX into code that browsers can understand.


✅ Step 1 — You write JSX:
```const element = <h1>Hello, World!</h1>;```

✅ Step 2 — Babel transforms it into React code:
```const element = React.createElement('h1', null, 'Hello, World!');```

✅ Step 3 — React creates a virtual DOM object:
```
{
  type: 'h1',
  props: {
    children: 'Hello, World!'
  }
}
```

✅ Step 4 — React renders it into the actual DOM.

## JSX Rules:
JSX looks simple, but it has some important rules:

**1️⃣ Return only one parent element**
JSX must have one root element wrapping everything:
```
// ✅ Correct
return (
  <div>
    <h1>Hello</h1>
    <p>World</p>
  </div>
);
```

```
// ❌ Incorrect
return (
  <h1>Hello</h1>
  <p>World</p>
);
```

If you don’t want extra ```<div>```, you can use React fragments:
```return (
  <>
    <h1>Hello</h1>
    <p>World</p>
  </>
);
```

**2️⃣ Use className instead of class**
In JSX, class is a reserved JS word, so you write:
```<div className="container">Hello</div>```


**3️⃣ Expressions go inside {}**
You can put JavaScript expressions inside JSX using curly braces:

```
const name = 'John';
return <h1>Hello, {name}</h1>;
```

**4️⃣ Self-close empty tags**
JSX tags must be closed:
```
<img src="image.png" />
```


# Virtual DOM
The Virtual DOM is a lightweight JavaScript representation (or copy) of the real DOM in the browser.

Instead of directly manipulating the real DOM when your app’s data changes, React first updates this virtual DOM. Once the changes are figured out, React calculates the minimum number of real DOM updates needed and applies them efficiently.


**Q1: What makes React so powerful?
 Q2: What is virtual DOM?
 Q3: What is the difference between virtual DOM and shadow DOM?**



### Why do we need the Virtual DOM?
The real DOM is slow to update because:

✅ It’s a complex tree of elements
✅ Every change can trigger reflow, repaint, or layout recalculations
✅ Manipulating it frequently (especially in large apps) can hurt performance

The virtual DOM helps minimize expensive DOM operations, making apps faster and smoother.

### 🔧 How does the Virtual DOM work?
Here’s the typical process:

**1️⃣ Render the virtual DOM**
React calls your component functions and creates a virtual DOM tree — just plain JS objects describing the UI.
Example virtual DOM object:
```
{
  type: 'h1',
  props: { children: 'Hello, World!' }
}
```

**2️⃣ Detect changes (diffing)**
When your app’s state changes, React:
Creates a new virtual DOM tree
Compares (diffs) the new tree with the previous one

**3️⃣ Compute minimal updates (reconciliation)**
React figures out what exactly changed — which elements are new, updated, or removed.
Example:
<li>Text changed → update text node.</li>
<li>List item added → insert a new </li>

<br>

**4️⃣ Update the real DOM efficiently**
Finally, React applies only the necessary changes to the actual DOM, instead of re-rendering everything.


**⚡ Simple analogy**
Imagine the real DOM as a giant to-do list on paper.
If you erase and rewrite the whole list every time, it’s slow.

But if you first make edits in a notebook (virtual DOM) and then only change what’s necessary on the paper, you save time and work more efficiently.

**🔑 Benefits of the Virtual DOM**
✅ Faster UI updates
✅ Better performance for large or frequently updating apps
✅ Declarative code (React decides how to update the UI)

# How React reconciles updates?
Reconciliation is the process React uses to figure out what changed in the UI when the state or props change — so it knows what minimal changes to make in the real DOM.

Here’s how it works:

**1️⃣ New virtual DOM is created**
When your component state/props change, React renders a new virtual DOM tree.

**2️⃣ React compares old vs. new virtual DOM (diffing algorithm)**
React walks through both trees and compares nodes.
To do this fast:

It compares elements by type (div vs. span, Button vs. Input).
If types are the same → React updates the props and recurses on the children.
If types are different → React replaces the whole subtree.

**3️⃣ Uses the key prop to detect list changes**
For lists (``<li>``), React needs help to track which items moved, were added, or were removed.

**Example:**
```items.map(item => <li key={item.id}>{item.text}</li>)```

The key lets React know:

If the item stayed in place
If it moved
If it’s new or removed

Without keys, React just re-renders the whole list → slower.

**4️⃣ Calculates minimal DOM updates**
React builds a set of instructions for how to update the real DOM efficiently.

## How React batches updates
Batching means React groups multiple state updates together so they only trigger one re-render, not multiple.

Example without batching:
```
setCount(1);
setName('John');
setVisible(true);
```

Without batching → React would re-render after each setState → 3 renders.

But React batches updates automatically:

Inside React event handlers (onClick, onChange)
During lifecycle methods (useEffect, componentDidMount)
With hooks (useState, useReducer)

So the 3 updates above → 1 combined render.

**✅ Before React 18 →** batching only worked inside React events.
**✅ In React 18+ →** React automatically batches updates even inside promises, timeouts, or native event handlers.