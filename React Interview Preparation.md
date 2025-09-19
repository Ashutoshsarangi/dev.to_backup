**1. What is Difference between useState & useRef ?**

Ans:- 
- **useState** is used to declare a state variable in a functional component. When the state changes, the component will re-render.

- **useRef**, on the other hand, returns a mutable ref object whose **.current** property is initialized with the passed argument (initialValue).
-  The returned object will persist for the full lifetime of the component.
- A common use case for useRef is to access the properties of a child component imperatively. It's important to note that changes to a ref's **.current** property do not cause the component to re-render.

**2. What are portals in React?**

- Let's say in some scenarios we need to render a component outside of the root DOM node, Here we can use portal.

- We can use it for Modal / some Pop-up components.


**3. Why we need super in class component ?**

Ans:-

- A child class constructor can't make use of **this** reference until the **super()** has been called.

- If you don't call super(), JavaScript will **throw an error** because this is not initialized. This is because this in the context of the child class is uninitialized until super() has been called.

``` Javascript
class Parent {
  constructor() {
    this.name = 'Parent';
  }
}

class Child extends Parent {
  constructor() {
    super(); // Must call super() here
    this.name = 'Child';
  }
}
```

**4. useCallback vs useMemo vs React.memo**

Ans:-

- **useCallback** is a hook that will return a memoized version of a callback function that only changes if one of the dependencies has changed.
- It's useful when passing callbacks to optimized child components that rely on reference equality to prevent unnecessary renders.

``` Javascript
import React, { useState, useCallback } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={increment}>
        Click me
      </button>
    </div>
  );
}

```

- **useMemo** is a hook that will return a memoized value, that only recomputes if one of the dependencies has changed. It's useful for expensive calculations. 

``` Javascript
 import React, { useState, useMemo } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  const expensiveValue = useMemo(() => {
    // Perform expensive calculation here
    return computeExpensiveValue(count);
  }, [count]);

  return (
    <div>
      <p>Expensive value: {expensiveValue}</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
🧠 What Happens When You Add [] in useCallback?
When you pass an empty array [] as the second argument to useCallback, it means:

"Only create this callback once, when the component mounts. Never recreate it again."

- **React.memo** is a higher order component that memoizes the result of a function component and renders it only when the props change.
- It's useful to prevent unnecessary renders for components that render the same result given the same props.

```Javascript
import React from 'react';

const MyComponent = React.memo(function MyComponent(props) {
  // render logic here
});

export default MyComponent;
```

**NOTE:-**
 useCallback is used to memoize functions, useMemo is used to memoize values, and React.memo is used to memoize components.

- `React.memo` is a **higher-order component (HOC)** that wraps a **functional component** to memoize its output.
- Class components already have built-in lifecycle methods like `shouldComponentUpdate` that serve a similar purpose.

---

### ✅ For Functional Components

```tsx
const MyComponent = React.memo(function MyComponent(props) {
  return <div>{props.name}</div>;
});
```

---

### 🏛️ For Class Components

If you're using class components and want to optimize rendering, you can use:

#### 1. **`PureComponent`**

```tsx
class MyComponent extends React.PureComponent {
  render() {
    return <div>{this.props.name}</div>;
  }
}
```

- `PureComponent` automatically implements a shallow comparison of props and state.

#### 2. **`shouldComponentUpdate`**

```tsx
class MyComponent extends React.Component {
  shouldComponentUpdate(nextProps) {
    return nextProps.name !== this.props.name;
  }

  render() {
    return <div>{this.props.name}</div>;
  }
}
```

---

### 🔍 Summary

| Optimization Tool | Applicable To |
|-------------------|----------------|
| `React.memo`       | Functional Components |
| `PureComponent`    | Class Components |
| `shouldComponentUpdate` | Class Components |

---

### 📝 **Note on Object References and Dependency Arrays in React**

When passing an object as a prop from a parent to a child component in React, it's important to understand how object references behave during re-renders. Even if the contents of the object remain unchanged, a new reference is created every time the parent re-renders. This means that:

- **The child component receives a new object reference**, even though the actual data might be the same.
- **If this object is used in a dependency array** (e.g., in `useEffect`, `useMemo`, or `useCallback`), the hook will re-trigger because the reference has changed.

Similarly, when using `setState` to update an object in a component, React treats it as a new object—even if the values inside are identical—resulting in a new reference. This behavior can lead to **unintended recalculations or re-renders** if not handled carefully.

To avoid unnecessary updates:
- Consider **memoizing objects** using `useMemo` or `useCallback`.
- Use **primitive values** in dependency arrays whenever possible.
- For deeply nested objects, consider using **stable references** or **custom comparison logic** if optimization is critical.

---

####  For deeply nested objects, consider using **stable references** or **custom comparison logic** if optimization is critical.

Absolutely! Here's a revised example using a **deeply nested object** to demonstrate how to stabilize references with `useMemo` for use in a `useEffect`:

---

### ✅ **Handling Deeply Nested Objects in `useEffect` with `useMemo`**

When working with deeply nested objects, passing them directly into a `useEffect` dependency array can cause unnecessary re-renders due to reference changes—even if the nested values haven't changed. To avoid this, you can use `useMemo` to create a stable reference based on specific nested properties.

#### 🔧 Example:

```jsx
import { useEffect, useMemo } from 'react';

function MyComponent({ user }) {
  // Let's say user object looks like this:
  // {
  //   id: 1,
  //   profile: {
  //     name: 'Ashutosh',
  //     details: {
  //       age: 30,
  //       location: 'Cyprus'
  //     }
  //   }
  // }

  // Memoize only the nested values you care about
  const memoizedProfileDetails = useMemo(() => {
    return {
      name: user.profile.name,
      age: user.profile.details.age,
      location: user.profile.details.location
    };
  }, [user.profile.name, user.profile.details.age, user.profile.details.location]);

  useEffect(() => {
    console.log('Effect triggered due to change in profile details');
    // Perform side effects like API calls or logging
  }, [memoizedProfileDetails]);

  return (
    <div>
      <h2>{memoizedProfileDetails.name}</h2>
      <p>Age: {memoizedProfileDetails.age}</p>
      <p>Location: {memoizedProfileDetails.location}</p>
    </div>
  );
}
```

---

### ✅ You *can* directly write:
```js
useEffect(() => {
  // your effect logic
}, [user.profile.name, user.profile.details.age, user.profile.details.location]);
```

This is **perfectly valid** and React will correctly re-run the effect when **any of those primitive values change**.

---

### 💡 So why use `useMemo` then?

While directly listing nested values works fine, there are **specific cases** where `useMemo` becomes useful:

#### 1. **You need to pass a stable object reference**
If you're passing the object (e.g., `profileDetails`) to another hook or component, and you want to avoid unnecessary re-renders or recalculations, you need a **stable reference**. That’s where `useMemo` helps.

#### 2. **You want to encapsulate logic**
Sometimes, you want to group related values into a single object and treat them as one unit. `useMemo` lets you do that while keeping the reference stable.

#### 3. **Cleaner dependency management**
If you have many nested values, listing them all in the dependency array can get messy. `useMemo` lets you bundle them into one memoized object and use that in the dependency array.
---

**5. What will happen if we overdo useMemo, Memo, and useCallback above functionalities ?**

**Memory Usage:** 

- Overusing React.memo can increase the memory usage of your application, as it stores the previous version of a component in memory.

**Performance Issues:** 

- While these hooks and React.memo are meant to optimize performance, overusing them can actually have the opposite effect. 

- For instance, useMemo and useCallback have a cost, and if the computation they are preventing is not more expensive than the cost of using the hook, you can end up with slower performance.

**6. What is difference between react component vs react element ?**

Ans:-

**React Component:** 

- A React Component is a function or a class which optionally accepts input and returns a React element. Components can be reused and can also maintain a private state

``` Javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

**React Element:**

- A React Element is a plain object describing what you want to appear on the screen in terms of the DOM nodes or other components. Elements can contain other Elements in their props.
- Creating a React element is cheap. Once an element is created, it is never mutated.

``` Javascript
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

### 🛠️ `React.createElement` Overview

`React.createElement` is the low-level API that JSX compiles down to. It creates a React element, which is a plain JavaScript object describing what to render.

### 📦 What You Can Pass to `React.createElement`

```js
React.createElement(
  type,       // e.g., 'div' or a React component
  props,      // an object with props like className, onClick, etc.
  ...children // child elements or text
)
```

### Can You Add a State?

No, you **cannot directly add state** to a `React.createElement` call. Here's why:

- `React.createElement` is **not a component**—it's just a way to describe what should be rendered.
- State is managed **inside functional or class components**, using hooks like `useState`, `useReducer`, etc.
- You can **pass state as props** to a component created with `React.createElement`, but the state itself must be managed elsewhere.

#### Example:

```js
function MyComponent({ count }) {
  return React.createElement('div', null, `Count is ${count}`);
}

function Parent() {
  const [count, setCount] = useState(0);

  return React.createElement(MyComponent, { count });
}
```

In this example:
- `Parent` manages the state.
- `MyComponent` receives the state as a prop via `React.createElement`.

---

### 🧠 Summary

- ✅ You can pass **props** (including state values) to components via `React.createElement`.
- ❌ You cannot **define or manage state** directly inside `React.createElement`.
- 🧩 State must be handled inside a component using hooks or class state.

---

### **1. If JSX is just syntactic sugar for `React.createElement`, how can we access hooks like `useState`, `useEffect`?**

You're absolutely right that JSX compiles to `React.createElement`, but there's an important distinction:

- `React.createElement` is used to **describe what to render**.
- Hooks like `useState`, `useEffect`, etc., are used **inside functional components**, which are functions that React calls to render elements.

#### 🔍 Why This Works:
When you write a component like this:

```jsx
function MyComponent() {
  const [count, setCount] = useState(0);
  return <div>{count}</div>;
}
```

JSX inside `MyComponent` gets compiled to `React.createElement(...)`, but the **component itself is a function** where hooks are allowed. You **cannot use hooks inside `React.createElement` directly**, because it's not a component—it's just a way to create an element.

---

**7. Core Principle of Redux?**

Ans:-

- Single Source of Truth
- State is read-only (Never update directly)
- Changes are made in Pure Functions (Reducer)
- Only works for Serializable Objects.

**8. Diffing Algorithm, reconciliation, and React fiber?**

Ans:- Separate Article on the same
[A Deep Dive into React's Optimization Algorithms & Process](https://dev.to/ashutoshsarangi/a-deep-dive-into-reacts-optimization-algorithms-process-4k57)

**9. What are Synthetic events in react?**

Ans:- Events we are making sure should be consistent across different browsers.

Ex:- preventDefault(), stopPropagation()

**10. Lifting State up?**

Ans:- When Several component needs to share the same changing data then it is recommended to liftthe shared state up to their closest common ancestor.

