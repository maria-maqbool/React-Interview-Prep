# ✅ **What is Conditional Rendering in React?**

Conditional rendering means **showing different UI (or components) based on some condition**.

It’s like using **`if`/`else` statements in JavaScript** — but inside your JSX to decide **what to render and when.**

For example:

👉 If a user is **logged in**, show a **"Welcome"** message.
👉 If not, show a **"Please log in"** message.

---

## 📝 **Basic Example**

```jsx
function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <h1>Welcome back!</h1>;
  } else {
    return <h1>Please log in.</h1>;
  }
}

export default Greeting;
```

✅ Here, `Greeting` shows a different message based on `isLoggedIn` prop.

---

## 🚀 **Different ways to do conditional rendering in React:**

### 1️⃣ **Using `if-else` (inside function)**

```jsx
if (condition) {
  return <ComponentA />;
} else {
  return <ComponentB />;
}
```

---

### 2️⃣ **Using **`&&` (Logical AND)** operator:**

Render something **only if the condition is true:**

```jsx
{isLoggedIn && <p>Welcome back!</p>}
```

👉 If `isLoggedIn` is `false`, **React ignores it** and shows nothing.

---

### 3️⃣ **Using **ternary operator `? :`**:**

```jsx
{isLoggedIn ? <h1>Welcome!</h1> : <h1>Please log in.</h1>}
```

✅ Good for **inline conditions**.

---

### 4️⃣ **Using variables to store elements:**

```jsx
let message;
if (isLoggedIn) {
  message = <h1>Welcome!</h1>;
} else {
  message = <h1>Please log in.</h1>;
}

return <div>{message}</div>;
```

---

## 🎯 **Why is conditional rendering useful?**

✅ To **control the UI** based on app state (like authentication, permissions, feature flags, etc.).

✅ To **show/hide components dynamically**.

✅ To avoid rendering unnecessary components.

---

## 🔍 **Example with button toggle:**

```jsx
import { useState } from 'react';

function App() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);

  return (
    <div>
      {isLoggedIn ? <h1>Welcome!</h1> : <h1>Please log in.</h1>}
      <button onClick={() => setIsLoggedIn(!isLoggedIn)}>
        {isLoggedIn ? 'Logout' : 'Login'}
      </button>
    </div>
  );
}

export default App;
```

👉 When you click the button, it toggles between **login/logout** and updates the message.

---

## 🏆 **In short:**

Conditional rendering in React is like saying:

✅ "**If this is true, show this. Otherwise, show that.**"

You can achieve it using:

* `if-else`
* `? :` ternary
* `&&` operator
* storing elements in variables