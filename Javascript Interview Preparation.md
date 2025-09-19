## **_V24.08.03_**

**1. What is the difference between let, const and var?**

Ans:- In javascript these are used in declaring variables .
1. Var are function-scoped, meaning they are only accessible within the function they are declared in. If they are not declared inside any function, they are globally scope.
2. let and const are block scope

in const, we can't reassign the values for the same variable. 

**2. What is Hoisting ?**

Ans:- 
1. This is a behavior, which is happening in the compile phase. (memory allocation) Phase
2. Where the variable and function declarations are moved to the top of their containing scope.
3. it's important to note that only the declarations are hoisted, not initialization. 

NOTE:- 
let and const are hoist there variable but they are in a different Place. they are in an uninitialized zone. i.e called **Temporal Dead Zone **

**3. What is Closure?**
  
Ans:-
1. A function created inside another function has access to variables declared in its parent function, even after the parent function has finished execution.
2. This concept is called Closure.
3. This approach is used in Modular patterns in javascript (Functional Programming)

**4. What is persistance Lexical Scope Reference Data? (P.L.S.R.D) Lexical/static (BackPack) ?**

Ans:- 

1. As mentioned above the closure have the access of outer scope Variables, as because of this . 
2. Actually it takes the variables along with the return function.as like backpack

**5. What is Higher Order function**

Ans:- 

1. A function which takes or return a function is called higher order function,

Ex:- map, filter , reduce of Array, + closure 

**6. What is Currying?**

Ans:- 

1. Currying is a technique in JavaScript where a function with multiple arguments is transformed into a sequence of functions, each with a single argument. Each function returns another function that takes the next argument until all arguments are used.

``` javascript
function curryAdd(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    }
  }
}

const add = curryAdd(1)(2)(3); // Outputs: 6
```

Advantages:-

1. Function Composition: Curried functions are extremely useful in function composition. Since each function takes just one argument, it's easy to create a pipeline of functions where the output of one function is the input of the next.

2. Lazy Evaluation: Currying can be used to produce new functions for delayed computation. The evaluation of the function gets delayed until all the necessary arguments are available.  

**7. What is Scope and Lexical Scopeing?**

Ans:- 
1. In JavaScript, scope refers to the **context in which variables are declared, initialized, and accessed**. There are **three** types of scope: 
 
a. **Global Scope:** Variables declared outside of any function or block are in the global scope and can be accessed from anywhere in the code.
  
b. **Function Scope:** Variables declared within a function using the var keyword are in the function scope and can only be accessed within that function.  

c. **Block Scope:** Variables declared within a block (for example, within an if statement or for loop) using the let or const keyword are in the block scope and can only be accessed within that block.
  
2. **Lexical scoping,** also known as static scoping, is a **convention used by JavaScript to determine the accessibility of variables, functions, and objects based on their physical location in the source code**. In lexical scoping, a child scope always has access to the variables declared in its parent scope.

**8. What is this?**

Ans:- 
1. In JavaScript, **this** is a special keyword that refers to the context in which a function is called.
2. The value of this depends on how the function is called, not where the function is declared.  

3. In a regular function declaration, this is dynamically bound. This means that its value is determined by how the function is called.
Here's an example:

``` javascript
function myFunction() {
  console.log(this);
}

const myObject = { name: 'My Object' };

// Call myFunction as a method of myObject
myObject.myMethod = myFunction;
myObject.myMethod(); // Outputs: { name: 'My Object', myMethod: [Function: myFunction] }
```
4. However, **in an arrow function**, this is **lexically bound**. This means that its value is determined by the surrounding scope at the time the function is declared, not by how the function is called. 

Here's an example:

``` javascript
const myObject = {
  myMethod: () => {
    console.log(this);
  }
};

myObject.myMethod(); // Outputs: window (browser)
```
Depending on your need you can use the this 

**Call, apply and bind**
1. In JavaScript, call, apply, and bind are methods used to control the context of this in a function. 

``` javascript
//Call
function greet() {
  console.log(`Hello, ${this.name}`);
}

const user = { name: 'John' };
greet.call(user); // Outputs: "Hello, John"

//apply

function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const user = { name: 'John' };
greet.apply(user, ['Hello', '!']); // Outputs: "Hello, John!"

//bind will return a function

function greet() {
  console.log(`Hello, ${this.name}`);
}

const user = { name: 'John' };
const greetUser = greet.bind(user);

greetUser(); // Outputs: "Hello, John"

```

**9. What is prototype and prototype chain ?**
Ans:-
1. Every Object has a property called Prototype. 
2. It is a blue print Object that other objects inherit property and methods from.

example:- 

``` javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

Person.prototype.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};
const john = new Person('John', 'Doe');
console.log(john.getFullName()); // Outputs: "John Doe"

```

Prototype Chain:-

1. The prototype chain is a series of links between objects that determines where JavaScript looks for a property or method when it's used on a certain object. 
2. The chain starts with the object itself and follows the links from one prototype object to the next until it reaches null.

**10. What is Prototype inheritance ?**
Ans:- Prototype chain where we go to words parent prototype to find something. So we can access the parent prototype property.

**11. What is Class and Inheritance ?**
Ans:- 
Inheritance is a principle in object-oriented programming where one class can inherit properties and methods from another class. This is done using the extends keyword.

**12. When we create an class instance how much Memory it captures ?**
1. **Properties:** Each property on the object takes up some memory. The exact amount depends on the type and size of the property's value. For example, a number takes up less memory than a string, and a small string takes up less memory than a large string. 
 
2. Methods: class methods are shared between all instances and only stored once in memory.  

3. Overhead: There is some overhead associated with each object for JavaScript's internal use. This includes the memory needed to store the object's prototype link, property names, and other internal information. 

**13. What is Event Loop ?**
Ans:-
1. The Event Loop is a key component of JavaScript's concurrency model and is responsible for executing JavaScript code. 
2. It handles asynchronous callbacks and maintains a queue of tasks to be executed. 

**Here's a simplified explanation of how the Event Loop works:** 

a. When your JavaScript program makes an asynchronous call (like a network request or a setTimeout), this task is handled off to the browser's Web APIs. 
b. This allows your code to continue running without waiting for the asynchronous task to complete.  
c. Once the asynchronous task is complete, it gets added to a task queue (also known as the callback queue(macro task queue) / Micro task Queue).  
d. The Event Loop constantly checks if the call stack (where your synchronous code runs) is empty. If it is, it takes the first task from the (task queue/ micro task queue) and pushes it onto the call stack to be executed.  
e. This process continues in a loop, hence the name "Event Loop". It allows JavaScript to handle asynchronous operations, even though JavaScript is single-threaded.

``` javascript
console.log('Start');

(async fun1 => console.log('I will Execute as a synchronously'))()

new Promise((resolve, reject) => console.log('I must execute synchronously'));

setTimeout(() => {
  console.log('Timeout callback');
}, 0);

Promise.resolve().then(() => {
  console.log('Promise callback');
});

console.log('End');

/*
Output
Start
I will Execute as a synchronously
I must execute synchronously
End
Promise callback
Timeout callback
*/

```

**14. What is Macro task queue and Micro task queue ?**

1. **Macro Task Queue**: This queue includes tasks like setTimeout, setInterval, setImmediate (Node.js), and requestAnimationFrame. When the call stack is empty, the Event Loop checks the Macro Task Queue. If there are any tasks in the queue, the Event Loop takes the first one and pushes it onto the call stack to be executed.
  
2. **Micro Task Queue**: This queue includes tasks like process.nextTick (Node.js), Promises, MutationObserver, and queueMicrotask. Micro tasks are processed after callbacks as long as no other JavaScript is mid-execution, and at the end of each task. This means that if a micro task adds more micro tasks, the Event Loop will keep going until the Micro Task Queue is empty before moving on to the next task in the Macro Task Queue.  

The main difference between the two queues is their priority in the Event Loop.

This leads to **Starvation in the callback Queue.**

**15. What is Event Delegation ?**
Ans:-
1. Event delegation is a technique in JavaScript where you delegate the handling of events to a parent element instead of handling events on individual child elements. This technique takes advantage of the fact that most DOM events bubble up through the DOM tree.

``` javascript
// Get the parent element
const parentElement = document.getElementById('parent');

// Add an event listener to the parent element
parentElement.addEventListener('click', function(event) {
  // Check if the clicked element is a child
  if (event.target.matches('.child')) {
    console.log('A child element was clicked');
  }
});
```
**The benefits of event delegation include:**
1. Performance: It can significantly improve performance for events on many elements, as you only need to set up one event listener on the parent element, rather than setting up an event listener on each child element.

2. Dynamic Elements: It allows you to handle events on elements that may not exist at the time the page loads. This is particularly useful for dynamic content where elements are added or removed after the page loads.

3. Simplicity: It simplifies your code by reducing the number of event listeners you need to manage.

**Disadvantages**

- **Not Suitable for All Events:** Not all events bubble up through the DOM. Some events, like focus, blur, and mouseenter, do not bubble. Therefore, event delegation cannot be used with these types of events.

- **Unwanted Event Triggering:** If child elements are not properly accounted for, events can be triggered by elements that you did not intend to trigger the event

**16. What is Pure function ?**
Ans:-
1. A pure function in JavaScript is a function that has the
**following characteristics:** 

a. Deterministic: Given the same input, the function will always produce the same output.  

b. No Side Effects: The function does not change any state or data outside of the function. It doesn't modify its input values, doesn't console log anything, doesn't make network requests, doesn't change any global variables, etc.

**17. Map, Set, week map and Week Set , What are these and What are the Benefit of it ?**

In JavaScript, Map, Set, WeakMap, and WeakSet are built-in objects that store collections of data.

1. **Map:** 
I. A Map object holds key-value pairs where any value (both objects and primitive values) may be used as either a key or a value.
II. Unlike regular objects, keys in Map can be of any type (not just strings or symbols). 
Also, Map maintains the insertion order of elements, which can be important in certain contexts.

``` javascript
let map = new Map();
map.set('name', 'John');
console.log(map.get('name')); // Outputs: "John"
```
2. **Set:** A Set object lets you store unique values of any type. It's similar to an array, but it doesn't allow duplicate values. This can be useful when you want to ensure that each value only appears once.

``` javascript
let set = new Set();
set.add('apple');
set.add('banana');
set.add('apple');
console.log(set.size); // Outputs: 2
```
3. **WeakMap:** 
I. A WeakMap is similar to a Map, but with some key differences. In a WeakMap, keys must be objects and they are held weakly, meaning if there are no other references to the object, they can be garbage collected. 

II. This makes WeakMap useful for privately storing data on objects, or for caching computed results for objects.

``` javascript
let weakMap = new WeakMap();
let obj = {};
weakMap.set(obj, 'hello');
console.log(weakMap.get(obj)); // Outputs: "hello"
```

4. **WeakSet:** A WeakSet is similar to a Set, but it only stores objects, and it doesn't prevent those objects from being garbage collected. Like WeakMap, WeakSet can be useful for tagging objects, or for storing objects that may or may not exist for a long time.


``` javascript
let weakSet = new WeakSet();
let obj = {};
weakSet.add(obj);
console.log(weakSet.has(obj)); // Outputs: true
```
**NOTE:**

1. The main benefits of these data structures are their ability to store non-string keys (Map and WeakMap), their ability to ensure uniqueness (Set), and their weak reference to keys (WeakMap and WeakSet), which allows for garbage collection when the keys are no longer in use elsewhere in your application.

**18. Disadvantages of Closure ?**

Ans:- memory leak, lets say there is a array reference in bacg pack but we are not using it any where . So It will keep on Hanging there.

Because garbage collectors will always find the reference, which is closuree to its backpack.

**19. How is Javascript doing the garbage Collection, What algorithm it is using?**

Ans:- 
JavaScript uses a form of garbage collection known as **mark-and-sweep**. 

This algorithm works in three stages:  

1. **Marking:** 

I. The garbage collector marks all root variables in the call stack (local variables and parameters of the current function, variables and parameters for other functions on the current call stack, and global variables). 
II. It then identifies any variables that these root variables reference and marks those as well. This process continues recursively, marking all variables that are reachable from the roots.

2. **Sweeping:** 

I. The garbage collector then goes through all the variables in memory. Any variable that wasn't marked in the previous step is considered **garbage and gets removed**.  

3. **Memory Allocation:** 

I. The memory freed up by removing garbage is put back into the memory pool and can be allocated again to new variables.

**NOTE:-**
  
1. This process is automatic and generally efficient, but it can cause performance issues if a large amount of memory needs to be cleaned up all at once. 
2. To mitigate this, modern JavaScript engines try to run the garbage collector incrementally or in parallel with the program to minimize the impact on performance.

**20. How == and === are similar ?**

Asn:- When both values type is same the == internally calls ===

**21. What is difference between Object.create() and Object.assign() ?**

Ans:- 
**Object.create()** and **Object.assign()** are both used for creating new objects in JavaScript, but they serve different purposes:

1. **Object.create({anotherObject}):** 

I. This method creates a new object with **AnotherObject** as its prototype. 
II. This can be useful when you need to create a new object and set its prototype at the same time.

``` javascript
const animal = {
  speak: function() {
    console.log('Hello');
  }
};

const dog = Object.create(animal);
dog.speak(); // Outputs: "Hello"
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/brl1ig3i6f9cjva4pwix.png)


2. **Object.assign(target, ...sources):** 

I. This method is used to copy all enumerable own properties from one or more source objects to a target object. It returns the target object.

``` javascript
const target = { a: 1 };
const source1 = { b: 2 };
const source2 = { c: 3 };

const result = Object.assign(target, source1, source2);
console.log(result); // Outputs: { a: 1, b: 2, c: 3 }
```

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0cqt2kl2y70rfh9ycxkd.png)


**Summary:-**

In summary, Object.create() is used for setting up the prototype chain for objects, while Object.assign() is used for copying properties from one object to another.

**22. What is Difference between __proto__ && Prototype ?**

Ans:-
1. __proto__: This is a property of an object, pointing to the prototype of the constructor function that created the object.

``` javascript
 //For example, 
let obj = new SomeConstructor();
obj.__proto__ will point to SomeConstructor.prototype.

```
2. This property is used to climb up the prototype chain when accessing properties or methods, allowing objects to inherit features from their prototypes.


## **_V24.08.04_**


**23. Functions in Javascript ?**
Ans:- [Functions in Javascript](https://dev.to/ashutoshsarangi/wip-functions-in-javascript-3ehj)

**24. What is the use of new keyword ?**

New put in a function, it will do below 4 things

1. Create this(object)
2. It links the Object to another Object
3. Adding property associated with this
4. return this object

**25. javascript Primary patterns**
Ans:- 
Basically:- 3 types

**1. modular pattern**

``` javascript
function Wrapper() {
  let x = [];
  function a () {
  console.log(x)
  }

  function b () {
    c();
  }

  function c () {
  }

  return {
  a,
  c
  }
}

const wrap = Wrapper();
wrap.a();
```

**2. prototype Pattern**

``` javascript
function protoTypeFunpattern (name, age) {
  this.name = name;
  this.age= age;

  a () {
  this.c();
  }

  b() {
  }

  c() {
  }
}
const obj = new protoTypeFunpattern('Ashu', 12);
```

**3. observable Pattern**

``` javascript
class EventObserver {
  constructor() {
    this.observers = [];
  }

  subscribe(fn) {
    this.observers.push(fn);
  }

  unsubscribe(fn) {
    this.observers = this.observers.filter(subscriber => subscriber !== fn);
  }

  broadcast(data) {
    this.observers.forEach(subscriber => subscriber(data));
  }
}

const observer = new EventObserver();
```
**26. What is the difference between Object.setPrototypeOf() and Object.create()?**

Ans:- 
1. **Object.setPrototypeOf(obj, prototype):** This method sets the prototype (i.e., the internal [[Prototype]] property) of the obj object to prototype. 
2. It directly modifies the existing object's prototype. This can be useful when you need to change the prototype of an existing object, but it's generally not recommended for performance reasons.

``` javascript
let obj = { a: 1 };
let prototypeObj = { b: 2 };
Object.setPrototypeOf(obj, prototypeObj);
console.log(obj.b); // Outputs: 2
```

**Object.create(proto):** This method creates a new object with proto as its prototype. 
2. This can be useful when you need to create a new object and set its prototype at the same time.

``` javascript
let prototypeObj = { a: 1 };
let obj = Object.create(prototypeObj);
console.log(obj.a); // Outputs: 1
// a property present inside prototype of obj. Currently obj = {}
```
**27. generator and Iterator ?**

Iterators:-
For Of loop For in Loop

generators:- 

Yield is very powerful 
1. Not only returns the value but it can take a value as a parameter when it executes

Very Important 
1. When we Call a generic function, it immediately 
returns { next()} When we call x.next(). ---> Then the execution context of createFlow() started.

**28. Async generator ?**

1. In JavaScript, an async generator is a function that can generate a sequence of values over time. 
2. These values can be generated asynchronously, and the function can be paused between each one. 

This is done using the async function* syntax and the yield keyword.

example:-

``` javascript
async function* asyncGenerator() {
  let i = 0;
  while (i < 3) {
    // Simulate asynchronous operation
    await new Promise(resolve => setTimeout(resolve, 1000));
    yield i++;
  }
}

// Usage
(async () => {
  for await (let value of asyncGenerator()) {
    console.log(value); // Outputs: 0, 1, 2 (with a delay of 1 second between each output)
  }
})();
```

**29. mixin in Javascript**

1. In JavaScript, a mixin is a technique that allows you to share methods or properties between objects or classes, without using inheritance. 

2. A mixin is an object that contains methods that can be used by other objects. The methods from a mixin can be copied into another object, allowing that object to use the methods as if they were its own.

``` javascript
class Dog {
  constructor() {
    this.legs = 4;
  }
  speak() {
    console.log('Woof!');
  }
}

const robotMixin = {
  skin: 'metal',
  speak: function() { console.log(`I have ${this.legs} legs and am made of ${this.skin}`) },
}

let robotFido = new Dog();

Object.assign(robotFido, robotMixin);

robotFido.speak(); //

/*
code explanation

1. You've created a Dog class and a robotMixin object. 
2. Then you've created an instance of Dog and used Object.setPrototypeOf() to set the prototype of robotFido to robotMixin.
3. However, there's a caveat. When you set the prototype of robotFido to robotMixin, it will lose its connection to the Dog prototype.
4. This means that if you add methods to the Dog prototype later, robotFido won't have access to them.
5. f you want robotFido to have access to both Dog prototype methods and robotMixin methods, you can use Object.assign() to copy properties from robotMixin to robotFido:

**Object.assign(robotFido, robotMixin);**

6. In this code, Object.assign() is used to copy properties from robotMixin to robotFido. 
7. Now robotFido has access to both its own methods and the methods from robotMixin. 
8. Note that the speak method in robotMixin overrides the speak method in Dog because it's added later.
*/
```

**30. How many types of imports are there?**

these 2 are **named Imports**
import {} from '../
import ask from '../

**namespace import**

import * as workshop from '../

**30. How Promise Works internally**
Promise = { value: ...,
 ------- 
onFullFilled: []
onReject: []
 }
1. In JavaScript, a Promise is an object that represents the eventual completion or failure of an asynchronous operation and its resulting value.
2. State: A Promise is always in one of these states: 
 
  a. pending: initial state, neither fulfilled nor rejected.
  b. fulfilled: meaning that the operation completed successfully.
  c. rejected: meaning that the operation failed.
  d. Settling: A Promise is said to be settled if it’s either 
     fulfilled or rejected.  
3. Then and Catch: Promises implement methods called .then and .catch to handle fulfillment and rejection. **.then** takes two optional arguments: a callback for success and a callback for failure. 
  - A callback for success (when the promise is fulfilled).
  - A callback for failure (when the promise is rejected).

``` javascript

// Using .then with both success and failure callbacks
fetchData(true).then(
  (result) => {
    console.log("Success:", result);
  },
  (error) => {
    console.error("Error:", error);
  }
);

```
4. **.catch** takes one argument: a callback for failure, it's just syntactic sugar for .then(null, errorCallback).

``` javascript
let promise = new Promise((resolve, reject) => {
  // Asynchronous operation.
  if (/* operation successful */) {
    resolve(result);
  } else {
    reject(error);
  }
});
```

**31. Promise.all vs promise.allSettled**

1. Promise.all() will reject immediately upon any of the input promises reject.
 
2. In comparison, the promise returned by Promise.allSettled() will wait for all input promises to complete, regardless of whether or not one is rejected. 

3. Use allSettled() if you need the final result of every promise in the input iterable.

``` javascript

const fetchUser = () =>
  new Promise((resolve) => setTimeout(() => resolve("User data"), 1000));

const fetchOrders = () =>
  new Promise((resolve, reject) => setTimeout(() => reject("Orders failed"), 1500));

const fetchPayments = () =>
  new Promise((resolve) => setTimeout(() => resolve("Payments data"), 500));

Promise.allSettled([fetchUser(), fetchOrders(), fetchPayments()])
  .then((results) => {
    results.forEach((result, index) => {
      if (result.status === "fulfilled") {
        console.log(`Promise ${index + 1} fulfilled with:`, result.value);
      } else {
        console.log(`Promise ${index + 1} rejected with:`, result.reason);
      }
    });
  });

```

**32. functional programming key features**

principles:-

1. Pure Functions
2. Avoid Side Effects
    - Polluting outside the scope
    - doing Async Operations
    - even console.logs
3. Higher-Order Functional
    - map
    - filter
    - reduce 
4. Functional Composition
    - [array of Functions].reduce to do the Operation as like pipe
        - DisAdvantages:- Let's say a function needs 3 params and some need 1
5. Closure
    a. Very, very crucial + Backpack (P.L.S.R.D) (Persistence Lexical Scope Reference Data)
6. Function Decoration 
    a. Closure having a function as input and useing it inside the backpack/return function.
7. Partial Application (argument function arrangement)
8. Currying

**Function Decoration**:

1. Modifies or extends the behavior of a function.
2. Involves wrapping a function with another function that calls the original function and potentially alters its input, output, or side effects.
3. Useful for adding logging, caching, validation, or other cross-cutting concerns.

example:- closure


**Partial Application:** 

1. Pre-fixes some arguments of a function to create a new function with fewer arguments.

2. Involves creating a new function by fixing some arguments of an existing function, reducing the number of arguments the new function needs.
3. Useful for creating specialized functions from more general ones, improving code reusability and readability.

example:- Currying(1)(2)(3)

**33. Where to use new and where not to ?**

**Use New**

1. Object()
2. Array()
3. Function()
4. Date()
5. RegExp()
6. Error()

**Don't use New**

1. String()
2. Number()
3. Boolean()

const a = String('Anv')
const date = new Date(...)

**34. coercion Number and String ?**
coercion

Number + Number = Number
Number + String = String
String + Number = String
String + String = String

**35. Falsy and Truthy Values**

**Falsy values**

'', 0, -0, null, NaN, false, undefined

**Truthy Values:-** 

1, true, and other not falsy values

**Boolean () Same as !!**
