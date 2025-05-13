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
