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