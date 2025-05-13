# Q2: What is virtual DOM?
## Virtual DOM
The Virtual DOM is a lightweight JavaScript representation (or copy) of the real DOM in the browser.

Instead of directly manipulating the real DOM when your app’s data changes, React first updates this virtual DOM. Once the changes are figured out, React calculates the minimum number of real DOM updates needed and applies them efficiently.

---
## Q3: What is the difference between virtual DOM and shadow DOM?

Despite their similar names, the Shadow DOM and the Virtual DOM are fundamentally different concepts used for different purposes. The Shadow DOM is a browser-native feature (part of the Web Components standard) that provides DOM encapsulation, whereas the Virtual DOM is a JavaScript abstraction used by UI libraries to optimize rendering. In other words, Shadow DOM is about hiding and isolating a DOM subtree within an element, while Virtual DOM is about representing the UI in memory and minimizing real-DOM updates
legacy.reactjs.org
imperva.com
. For example, React’s documentation explicitly states that “the Shadow DOM is a browser technology designed primarily for scoping variables and CSS in web components,” while the “virtual DOM is a concept implemented by libraries in JavaScript”
legacy.reactjs.org.

---


## Why do we need the Virtual DOM?
The real DOM is slow to update because:

✅ It’s a complex tree of elements
✅ Every change can trigger reflow, repaint, or layout recalculations
✅ Manipulating it frequently (especially in large apps) can hurt performance

The virtual DOM helps minimize expensive DOM operations, making apps faster and smoother.

---
## 🔧 How does the Virtual DOM work?
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

---
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