Here’s a breakdown of the key algorithms that power React:

### 1. **Diffing Algorithm**

- The diffing algorithm is crucial for React's efficiency.
- When a component's state or props change, React compares the current virtual DOM with the new virtual DOM using this algorithm.
- By examining the two trees node by node from top to bottom, it identifies differences and updates only the changed elements in the actual DOM.
- This targeted updating minimizes costly DOM manipulations, resulting in faster performance.

But to make it a more successful/optimized algorithm we need to add **keys** in list items. 

### 2. **Reconciliation**

- **Reconciliation is the process** React uses to update the DOM.
- Upon changes in a component’s state or props, React generates a new virtual DOM and compares it with the previous one.
- Leveraging the diffing algorithm, React calculates the minimal set of changes needed to synchronize the real DOM with the new virtual DOM, ensuring efficient updates.

### 3. **React Fiber**

- React Fiber is a **reimagined version** of React’s reconciliation algorithm, introduced in React 16.
- Fiber's primary objective is to enable incremental rendering, which allows rendering work to be broken down into smaller chunks and distributed across multiple frames.
- This capability lets React pause, abort, or reuse work as new updates come in, and assign priority to different types of updates, improving responsiveness.

### 4. **Context API**

- The Context API addresses the challenge of prop drilling by enabling data sharing across all levels of a React application.
- It uses a Provider-Consumer relationship to pass data down the component tree, simplifying the management of global state without the need to pass props manually through each level.

NOTE:- It has its own problems, will update more related to this in a separate article.

[Performance-impact-using-context-api](https://dev.to/ashutoshsarangi/performance-impact-using-context-api-2eka
)

Feel free to reach out to me if you have any queries/concerns.
