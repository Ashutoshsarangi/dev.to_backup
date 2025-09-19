**Performance impact on Context-API?**

- UI components where the context is consumed is going to be re-rendered.

**Example**
- If there are 5 components are there and out of 5, 1 component is responsible for showing the counter and updating the counter. The other 4 components are just showcasing message value came from context.
- So even though they are not using **counter** value, they will still re-render.

- This will slow down our application.


**When and how to use Context API?**

**case - 1**

- If the state updates are frequent we should go with redux. (Selector) (Caching)

**case - 2**
- If we have state which remains the same most of the time, we can go for use context

Ex:-
- theme
- language Preference

**case - 3**

- if we wanted to use context in other places, then split it with smaller multiple contexts. In this case, re-rendering going to be reduced.

Note:-

- we can combine context + useReduce, it will help us to update the value using dispatch.

---

### 🔧 Example: MessageContext and CounterContext

Let’s say you have two contexts:

```jsx
// MessageContext.js
export const MessageContext = React.createContext();

// CounterContext.js
export const CounterContext = React.createContext();
```

#### 🧩 Wrapping with Both Providers

You can nest them like this:

```jsx
<MessageContext.Provider value={messageValue}>
  <CounterContext.Provider value={counterValue}>
    <YourComponent />
  </CounterContext.Provider>
</MessageContext.Provider>
```

Or vice versa—**order doesn’t matter** unless one depends on the other.

#### 🧠 Consuming Both Contexts

Inside `YourComponent`, you can use:

```jsx
const message = useContext(MessageContext);
const counter = useContext(CounterContext);
```
