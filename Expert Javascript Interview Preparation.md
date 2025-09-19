**Q. What are the tradeoffs in Event Delegation, Event Bubbling, and event capturing**

## 🔁 Event Propagation Phases

When an event occurs in the DOM, it goes through **three phases**:

1. **Capturing Phase** (a.k.a. "capture"):
   - The event travels from the root (`document`) **down to the target element**.
2. **Target Phase**:
   - The event reaches the **target element**.
3. **Bubbling Phase**:
   - The event bubbles **back up** from the target to the root.

---

## 🔄 Event Delegation

**Event delegation** is a technique where you attach a single event listener to a **parent element** instead of multiple children. It relies on **event bubbling**.

### ✅ Pros:
- Better **performance** (fewer listeners).
- Easier to manage **dynamic elements** (e.g., items added via JS).
- Cleaner, more maintainable code.

### ❌ Cons:
- Only works with events that **bubble** (e.g., `click`, not `focus` or `blur`).
- Can be tricky with **event.target** vs. **event.currentTarget**.

**Example:**
```javascript
document.getElementById('list').addEventListener('click', (e) => {
  if (e.target.tagName === 'LI') {
    console.log('Clicked:', e.target.textContent);
  }
});
```

---

## 🔼 Event Bubbling (Default)

- Events **bubble by default** in JavaScript.
- Most common events like `click`, `input`, `submit` bubble.

**Example:**
```javascript
document.body.addEventListener('click', () => {
  console.log('Body clicked (bubbling)');
});
```

---

## 🔽 Event Capturing

- You can listen during the **capturing phase** by passing `true` as the third argument to `addEventListener`.

**Example:**
```javascript
document.body.addEventListener('click', () => {
  console.log('Body clicked (capturing)');
}, true);
```

---

## 🧪 `addEventListener` Syntax

```javascript
element.addEventListener(type, listener, options);
```

- `options` can be:
  - `true` → use capturing
  - `false` (default) → use bubbling
  - or an object: `{ capture: true, once: false, passive: false }`

---

**Q. What are Workers and Service Worker, PWA Back ground Sync**
     - https://dev.to/ashutoshsarangi/web-worker-vs-service-worker-5h50
**Q. Web Storage**

- **Web Storage (localStorage & sessionStorage)**
- **Cookies**
- **IndexedDB**
- **HTTP-only cookies**

---

## 🗂️ 1. Web Storage

### ✅ **localStorage**
- Stores key-value pairs.
- Persistent (until manually cleared).
- Accessible via JavaScript.
- **Client-side only**.

### ✅ **sessionStorage**
- Similar to `localStorage`, but scoped to the browser tab/session.
- Cleared when the tab is closed.
- **Client-side only**.

---

## 🍪 2. Cookies

### ✅ **Regular Cookies**
- Can be read/written via JavaScript (`document.cookie`).
- Sent with every HTTP request to the server.
- Can be scoped by domain/path/expiration.

### 🚫 **HTTP-only Cookies**
- **Not accessible via JavaScript**.
- Set by the server using the `Set-Cookie` header with the `HttpOnly` flag.
- Used for sensitive data like session tokens.
- **Server-side only** (client can store but not read/write).

**Example:**
```http
Set-Cookie: sessionId=abc123; HttpOnly; Secure; SameSite=Strict
```

---

## 🧠 3. IndexedDB

- A low-level API for storing large amounts of structured data.
- Supports transactions and complex queries.
- Asynchronous and event-driven.
- **Client-side only**.

**Example:**
```javascript
const request = indexedDB.open("MyDatabase", 1);
request.onsuccess = (event) => {
  const db = event.target.result;
  console.log("DB opened:", db);
};
```

---

## 🔐 Summary Table

| Storage Type       | Accessible via JS | Persistent | Size Limit | Server Access | Use Case |
|--------------------|-------------------|------------|------------|---------------|----------|
| `localStorage`     | ✅ Yes            | ✅ Yes     | ~5MB       | ❌ No          | Simple key-value storage |
| `sessionStorage`   | ✅ Yes            | ❌ No      | ~5MB       | ❌ No          | Per-tab/session data |
| `Cookies`          | ✅ Yes            | ✅ Yes     | ~4KB       | ✅ Yes         | Auth, preferences |
| `HTTP-only Cookies`| ❌ No             | ✅ Yes     | ~4KB       | ✅ Yes         | Secure session tokens |
| `IndexedDB`        | ✅ Yes            | ✅ Yes     | ~50MB+     | ❌ No          | Complex structured data |

---
**Q. HTTP methods**

## 🌐 Common HTTP Methods

| Method   | Description |
|----------|-------------|
| **GET**  | Retrieves data from the server. Used for reading resources. |
| **POST** | Sends data to the server, often used for creating resources or submitting forms. |
| **PUT**  | Replaces a resource entirely with new data. |
| **PATCH**| Partially updates a resource. |
| **DELETE** | Removes a resource from the server. |
| **HEAD** | Similar to GET, but only retrieves headers (no body). Useful for checking metadata. |
| **OPTIONS** | Describes the communication options for the target resource (e.g., allowed methods). |
| **CONNECT** | Establishes a tunnel to the server, often used for HTTPS. |
| **TRACE** | Echoes the received request, used for debugging.

---

**Q. Browser Apis**

## 🧠 Core Categories of Browser APIs

### 1. 🕒 **Timer APIs**
Used to schedule code execution.

- `setTimeout(fn, delay)` – runs once after delay.
- `setInterval(fn, delay)` – runs repeatedly.
- `requestAnimationFrame(fn)` – optimized for animations.
- `queueMicrotask(fn)` – schedules a microtask (runs before next render).

---

### 2. 📦 **Storage APIs**
Used to store data on the client side.

- `localStorage` – persistent key-value storage.
- `sessionStorage` – per-tab/session key-value storage.
- `IndexedDB` – structured, large-scale storage.
- `Cookies` – small key-value pairs, sent with requests.
- `Cache API` – stores request/response pairs for offline use (used in service workers).

---

### 3. 🌐 **Navigation & History APIs**
Used to interact with the browser's navigation stack.

- `window.location` – read/write URL and redirect.
- `history.pushState()` / `history.replaceState()` – manipulate browser history without reload.
- `popstate` event – detect back/forward navigation.

---

### 4. 👀 **DOM & Event APIs**
Used to interact with the page structure and user actions.

- `document.querySelector`, `getElementById`, etc.
- `addEventListener` – handle events.
- `MutationObserver`, `IntersectionObserver`, `ResizeObserver` – observe DOM changes.

---

### 5. 📡 **Network APIs**
Used to make HTTP requests and handle responses.

- `fetch()` – modern way to make requests.
- `XMLHttpRequest` – legacy method.
- `WebSocket` – real-time communication.
- `navigator.sendBeacon()` – send data asynchronously (e.g., analytics).

---

### 6. 🔐 **Security & Identity APIs**
Used for authentication and permissions.

- `document.cookie` (with HttpOnly restrictions).
- `Credential Management API`
- `Permissions API` – check/request permissions (e.g., geolocation, camera).

---

### 7. 📍 **Device & Sensor APIs**
Used to access hardware features.

- `navigator.geolocation`
- `DeviceOrientationEvent`, `DeviceMotionEvent`
- `Battery API`, `Clipboard API`, `Vibration API`

---

### 8. 🧭 **Service Workers & Offline APIs**
Used for background tasks and offline support.

- `ServiceWorker`
- `CacheStorage`
- `Background Sync`

---
**Q. Types of Observer**
In JavaScript, **observers** are objects that watch for changes or events in the DOM or other browser APIs.

---

## 👀 Types of Observers in JavaScript

### 1. **Intersection Observer**
- Watches when an element enters or exits the viewport (or a parent container).
- Great for lazy loading images, infinite scrolling, or triggering animations.

**Example:**
```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      console.log('Element is in view:', entry.target);
    }
  });
});

const target = document.querySelector('#myElement');
observer.observe(target);
```

---

### 2. **Mutation Observer**
- Watches for changes in the DOM (e.g., added/removed nodes, attribute changes).
- Useful for reacting to dynamic content updates.

**Example:**
```javascript
const observer = new MutationObserver((mutations) => {
  mutations.forEach(mutation => {
    console.log('Mutation detected:', mutation);
  });
});

observer.observe(document.body, { childList: true, subtree: true });
```

---

### 3. **Resize Observer**
- Watches for changes in the size of an element.
- Useful for responsive design or layout adjustments.

**Example:**
```javascript
const observer = new ResizeObserver((entries) => {
  for (let entry of entries) {
    console.log('Resized:', entry.target);
  }
});

observer.observe(document.querySelector('#resizableElement'));
```

---

### 4. **Performance Observer**
- Monitors performance-related events like resource loading, long tasks, etc.
- Useful for performance analytics.

**Example:**
```javascript
const observer = new PerformanceObserver((list) => {
  list.getEntries().forEach(entry => {
    console.log('Performance entry:', entry);
  });
});

observer.observe({ entryTypes: ['resource'] });
```

---

## 🧠 JavaScript Event Loop Overview

JavaScript has two main task queues:

### 1. **Macro Task Queue**
- Includes: `setTimeout`, `setInterval`, I/O, UI rendering.
- These tasks are executed one at a time after the current stack is clear.

### 2. **Microtask Queue**
- Includes: `Promise` callbacks, `queueMicrotask`, `MutationObserver` callbacks.
- These are executed **immediately after the current task**, before any macro tasks.

---

## 🔍 Where Do Observers Reside?

### ✅ **MutationObserver**
- **Microtask queue**
- Its callback is scheduled as a **microtask**, meaning it runs **before** any `setTimeout` or other macro tasks.

### ❌ **IntersectionObserver**
- **NOT in the microtask queue**
- Its callback is scheduled as a **task** (macro task), and may be **throttled** by the browser for performance.
- It runs **after rendering**, not immediately after DOM changes.

### ✅ **ResizeObserver**
- **Microtask queue**
- Runs after layout and style calculations but **before paint**.
- Can be batched and delayed slightly for performance.

### ❌ **PerformanceObserver**
- Depends on the type of entry:
  - Some entries (like `resource`) are delivered as **macro tasks**.
  - Others (like `longtask`) may be batched and delivered asynchronously.

---

**Q. [High Performance Browser Networking](https://hpbn.co/)**
- http1 vs http2
  - https://dev.to/ashutoshsarangi/http1-vs-http2-vs-http3-2ce6
- Server Send Events
- webRTC
- polling → long polling vs short polling
- WebSocket

**Q. debounce Vs Thruttling**

```Javascript
const debFun = (fn, delay = 200) => {
 let timeCounter;
 return (...args) => { 
   if (timeCounter) { 
     clearTimeout(timeCounter);
   }
   timeCounter = setTimeout(() => { 
           fn(...args);
           timeCounter = null;
   }, delay); 
 };
 };

const print = () => console.log('Hello');
const testFun = debFun(print);

setInterval(() => { testFun(); }, 300);
```

```Javascript
function throttle(fn, delay) {
  let lastCall = 0;
  return function(...args) {
    const now = new Date().getTime();
    if (now - lastCall < delay) {
      return;
    }
    lastCall = now;
    return fn(...args);
  };
}

const print = () => console.log('Hello');

const throttledPrint = throttle(print, 200);

setInterval(() => {
  throttledPrint();
}, 100);
```

### Q. What are decorators, and how to create a custom decorator?

### 🧠 What Are Decorators?

Decorators are a **special kind of declaration** that can be attached to classes, methods, accessors, properties, or parameters. They are used to **modify or enhance behavior** at runtime.

> Decorators are currently a **stage 3 proposal** in JavaScript and are available in **TypeScript** or via Babel plugins.

---

### 🎯 Why Use Decorators?

Decorators help with:

- **Code reuse**: Apply common logic across multiple classes or methods.
- **Separation of concerns**: Keep business logic separate from cross-cutting concerns (e.g., logging, authorization).
- **Meta-programming**: Modify behavior dynamically.

---

### ✅ Example: Method Decorator in TypeScript

Here’s a simple example of a decorator that logs method calls:

```ts
function Log(target: any, propertyKey: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;

  descriptor.value = function (...args: any[]) {
    console.log(`Calling ${propertyKey} with`, args);
    const result = originalMethod.apply(this, args);
    console.log(`Result:`, result);
    return result;
  };

  return descriptor;
}

class Calculator {
  @Log
  add(a: number, b: number) {
    return a + b;
  }
}

const calc = new Calculator();
calc.add(2, 3); // Logs method call and result
```

---

### 🧪 Output:
```
Calling add with [2, 3]
Result: 5
```
