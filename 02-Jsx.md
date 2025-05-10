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

---

## Q2: Is JSX a part of React?
No, JSX is not a part of React itself — it's a syntax extension for JavaScript that React uses.

## 💡 Explanation:

"JSX (JavaScript XML) is not part of React, but it's commonly used with React because it makes writing UI components more readable and declarative. It allows us to write HTML-like syntax directly in JavaScript.

Under the hood, JSX is transpiled by tools like Babel into standard JavaScript using React.createElement() calls. So technically, you can write React without JSX, but JSX makes development much more intuitive and closer to how the UI is structured."

✅ Example:
```
// With JSX
const element = <h1>Hello, world!</h1>;

// Without JSX
const element = React.createElement('h1', null, 'Hello, world!');
```
---

## Q3: Why can't we write class inside our JSX markup?
In JSX, we can't use class as an attribute because class is a reserved keyword in JavaScript used to define classes (like class MyComponent {}).

Instead, React uses className to apply CSS classes. JSX is just syntactic sugar for JavaScript function calls (React.createElement()), so it follows JavaScript rules — and class would cause a syntax conflict.

So, to avoid confusion with JS keywords, React adopted className as a special prop for setting CSS classes.

💡 Example:
```
// ❌ Invalid in JSX
<div class="container">Hello</div> // Error!

// ✅ Correct
<div className="container">Hello</div>
```

🔧 Bonus Tip:
React converts className="container" to class="container" in the actual DOM when rendered — so the result in the browser is the same as regular HTML.

---

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
