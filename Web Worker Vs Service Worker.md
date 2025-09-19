## Introduction

When I first heard about these terms I thought, okay they are doing around the same things with their separate thread. Then Why we need these 2 terms?

But to tell you the truth there are **huge differences** between these 2 terms and how they behave.

Will try to explain in detail.


**Common ground Between these 2 is**

1. They are running in a separate thread, with out blocking the main single thread of Javascript.

**Web Worker** 

- Here the worker thread can perform tasks without interfering the main thread.
- These are used for tasks that required significant amount of CPU, such as image manipulation/processing, heavy calculation and data processing .
- It don't have capabilities to access DOM, and they can't intersept the network requests.
- It does not have a life cycle 


**Service Worker**
- It is a type of web worker with additional capabilities.
- It can run separate from the Browser / even when the Browser is closed.
- It is a core component of PWA, Because they used to enable features like offline support, background sync and push notifications.
- It act like a proxy server that sits between the browser and the network.


**Life Cycle of Service Worker**

**1. Registration**

- Here we will tell the browser where our service worker javascript file exist.

``` javascript
if ('serviceWorker' in navigator) {
// wrap it in try/catch / promisses
   await navigator.serviceWorker.register('/service-worker.js')
}

```

**2. Installation**

- When the browser considers the service worker to be new, the install event is triggered.

the below code we need to write it in **service-worker.js**

``` javascript
self.addEventListener('install', (event) => {
// do your operations
})
```

**3. Activation**

- After the installation it will jump here

``` javascript
 self.addEventListener('activate', (event) => {
// Do your Operation
})
```

**4. Idle**

- When service worker is not doing anything, it is in idle state.

**5. fetch/Message**

- Whenever a network request / message is made, the service worker wakes up and takes control

```javascrip
  self.addEventListener('fetch', (event) => {
  // Do your Opeation
})
```


**6. Termination**

- If not in use, the browser will terminate the service worker to save the memory. But when we don't know.

It will keep the service workers for very long time.

**Example:-**

in chrome Open this link there you will see lots of service worker hanging, and you can do lot of stuff like, Inspecting/starting and sending a message.

```
chrome://serviceworker-internals/
```

![Service workers in Chrome](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8q05z4ug0aj9zwhqkh2f.png)

**How we can Wake Up Service workers even the Browser is closesed.**

Note:-
For this specific we can use push to wake up, but for this use must give Notification permission to the Browser, else there is no way.

Other ways are relevant when the browser is still open

**1. fetch Event**

- This event is fired whenever a fetch request is made.

``` javascript
  self.addEventListener('fetch', event => {
  // Handle fetch event
});
```

**2. Message**

- This Event is fired when a message is received from another script. (Communication happening Service Worker + Other Javascript files)

```javascript
   self.addEventListener('message', (event) => {
// Handle message Event
})
```

**3. Push**

- This event is fired when a push message is received

```javascript
  self.addEventListener('push', (event) => {
// Handle Push Event
})
```

**4. Sync Event**

- This Event is fired when a background Sync event is received.

```javascript
  self.addEventListener('sync', (event) => {
// handle background Sync Event
})
```
**Reference**

1. https://frontendmasters.com/courses/background-javascript
