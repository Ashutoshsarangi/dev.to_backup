**Introduction**

Node.js is widely celebrated for its non-blocking, asynchronous architecture, making it an ideal choice for scalable and performant web applications. One of the key reasons behind this capability is its event-driven model and efficient handling of tasks via its event loop. Understanding the asynchronicity of Node.js requires delving into the queues that power this system. Interestingly, Node.js employs six different queues for task management, compared to the two primary queues found in browsers. Let’s explore these in detail.

---

### **The Six Queues in Node.js**

Node.js has a sophisticated mechanism to handle tasks using six queues:

1. **Timer Queue**
   - **Purpose**: Handles tasks scheduled with `setTimeout` and `setInterval`.
   - **Example**:
     ```javascript
     setTimeout(() => {
       console.log('Timer task executed');
     }, 1000);
     ```
   - Tasks in the Timer Queue are executed after the specified delay, but not before the current phase of the event loop is complete.

2. **I/O Queue (Callback Queue)**
   - **Purpose**: Processes I/O-related tasks, such as reading files or handling network requests.
   - **Example**:
     ```javascript
     const fs = require('fs');

     fs.readFile('file.txt', 'utf8', (err, data) => {
       if (err) throw err;
       console.log(data);
     });
     ```
   - The I/O Queue ensures callbacks are executed once the I/O operation completes.

3. **Check Queue**
   - **Purpose**: Executes tasks scheduled using `setImmediate()`.
   - **Example**:
     ```javascript
     setImmediate(() => {
       console.log('Check Queue task executed');
     });
     ```
   - **Note**: The Check Queue has one of the lowest priorities in the event loop. Tasks in this queue are processed after the I/O phase.

4. **Microtask Queue**
   - **Purpose**: Executes high-priority tasks, primarily related to promises and other microtasks.
   - **Subcategories**:
     - **a. process.nextTick Queue**:
       - Handles tasks scheduled with `process.nextTick()`.
       - Tasks in this queue are given the **highest priority** and are executed before any other microtasks.
     - **b. Separate Queue for Other Promises**:
       - Handles tasks related to resolved promises.

```javascript
process.nextTick(() => {
           console.log('process.nextTick task executed');
         });
Promise.resolve().then(() => {
           console.log('Promise resolved task executed');
         });
```
         

   - The Microtask Queue always runs to completion before moving on to the next phase of the event loop.

5. **Close Queue**
   - **Purpose**: Handles tasks related to closing operations, such as `socket.on('close')` events.
   - **Example**:
     ```javascript
     const net = require('net');

     const server = net.createServer((socket) => {
       socket.on('close', () => {
         console.log('Connection closed');
       });
     });
     server.listen(8080);
     ```
   - Tasks in the Close Queue are executed when a resource is explicitly closed.

---

### **How the Event Loop Prioritizes Queues**

The event loop in Node.js follows a specific order of phases for executing tasks. Here is the priority sequence:

1. **Microtask Queue (process.nextTick)**: Tasks in this queue are always executed first.
2. **Microtask Queue (Promises)**: Once `process.nextTick` tasks are complete, tasks in the Promises queue are executed.
3. **Timer Queue**: Tasks scheduled with `setTimeout` or `setInterval` are processed in this phase.
4. **I/O Queue**: Handles completed I/O operations.
5. **Check Queue**: Executes tasks from `setImmediate`.
6. **Close Queue**: Processes close callbacks for resources.

---

### **Comparison with Browsers**

In contrast, browsers have a simpler event loop model with only two primary queues:

1. **Macro Task Queue**: Handles tasks like `setTimeout`, `setInterval`, and DOM events.
2. **Microtask Queue**: Similar to Node.js, this queue handles tasks like resolved Promises and `MutationObserver` callbacks.

Node.js’s additional queues enable it to handle a wider variety of tasks, making it more suitable for server-side applications.

---

### **Key Insights**

- **SetImmediate vs setTimeout**:
  - While `setTimeout` adds tasks to the Timer Queue, `setImmediate` queues tasks in the Check Queue.
  - Tasks in the Check Queue (via `setImmediate`) are executed **after** the current I/O phase, while `setTimeout` waits for the timer phase.

- **Microtask Dominance**:
  - Tasks in the Microtask Queue, particularly `process.nextTick`, always take precedence, enabling high-priority execution.

- **Concurrency Without Chaos**:
  - The separate queues ensure that different types of tasks are handled in an organized and predictable manner, preventing starvation of lower-priority tasks.

---

Reference:-
1. https://frontendmasters.com/courses/servers-node-js/

