**_V24.08.03_**

**1. What is the difference between defer And async loading?**

defer:- 
1. download the JS file
2. And Done execution at the end of HTML parsing

async:-
1. download the file
2. continue the parsing
3. once it has the downloaded file it halts the parsing and starts executing it.

**2. What is the difference between addEventListener vs onClick (DOM event handler)?**

**DOM Event Handlers:-**
1. They are simple like functions
2. if I added same event handlers 2 times the last one will replace the 1st one.

**EventListner**

1. It follows the Observable / Subscribe pattern
2. Let's say the same element is attached to the same events multiple times, it will broadcast.

**Advance concept addEventListener**

``` javascript
const options= {
     once: true,
     passive: true
};

ele.addEventListener('load', callBack, options);
```

once:- It will remove the event listener after the first time the event is triggered.
passive:- It will not prevent the default behavior of the event.


**3. Why we need removeEventListener?**

``` javascript
ele.removeEventListener('load', callBack);

```
    1. When we have a single page application where we add/remove elements from the DOM.
    2. better to remove in this case.
    3. Other wise it will keep listening for the event and will keep the memory.

    When we close the browser it will clean everything

**4. How to dispatch a Dispatch Custome Event?**

1. Create a new event

``` javascript
const event = new Event('Ashu-Event');
ele.dispatchEvent(event);

ele.addEventlistner('Ashu-Event', callback);
```

**Note**

1. it should not be a shadow DOM; other wise we will not get the document object, as it has its own document and style property.
2. If it is a shadow dom, we can bind and listen the events from the window.

**5. what is the Difference between href attribute and getAttribute()**

Note: The href property returns the full URL while the getAttribute method will only return the pathname if that's what's in the attribute.

**6. What are the standards of Web Component**

Web Components

it has set of standards

1. Custom Elements
2. HTML Templates
3. Shadow DOM
4. Declarative Shadow DOM (New)

**7. Overview of Custome Element**

Syntax for web Component

``` javascript
class MyComponent extends HTMLElement {
    constructor() {
        super();
        this.dataset.languagen = 'en';
    }
}

customElements.define('my-component', MyComponent);

<body>
<my-component data-language='en'></my-component>
</body>
```

**8. What is the life cycle of the Custome Element?**

``` javascript
class MyComponent extends HTMLElement {
    constructor() {
        super();
    }

    connectedCallback() {
        console.log('Connected to the DOM');
    }

    disconnectedCallback() {
        console.log('Disconnected from the DOM');
    }

    adoptedCallback() {
        console.log('Adopted by a new parent');
        //
    }

    attributeChangedCallback(name, oldValue, newValue) {
        console.log('Attribute Changed', name, oldValue, newValue);
    }
}
```

**9. What is HTML Template?**

``` html
<!DOCTYPE HTML>
...
<template id='template1'>
    <span> Some Random String</span>
</template>
```

1. by default content inside the template are not rendered
2. We can use it only after cloning it, then we can use it

**10. What are the problems with CustomElement?**

1. Problem with template tag
let's say we have some style added to the template tag

``` html
<template id="my-template">
    <style>
        h1 {
            color: red;
        }
    </style>
    <h1>Hello World</h1>
</template>
```

Here it will affect the red color all across the page, but if we want to restrict the style to only the template tag, we can use Shadow dom

**11. What is Shadow DOM & Its Advantages?**

A private, isolated DOM tree within a web component that is separated from the main document's DOM tree.'

**Advantages of Shadow DOM:**

1. Allows more control over stylling and encapsulation of functionality of a custom Element;
2. By default, css declared in the main DOM won't be applied to the shadow DOM;'
3. It has its own dom
4. CSS declared in shadow dom applies only there
5. There are new Pseudo-classes and pseudo element to allow communication between Host and shadow DOM in styleSheet
6. It can be opened / closed defining visibility from the outer DOM. (Kind of Private / Public) private :- close


``` javascript
const host = document.querySelector("#host");
const shadow = host.attachShadow({ mode: "open" });// Open Shadow DOM

const span = document.createElement("span");
span.textContent = "I'm in the shadow DOM";
shadow.appendChild(span);
```

https://developer.mozilla.org/en-US/docs/Web/API/DOMParser

**12. What is Declarative Shadow DOM?**
1. A Way to define shadow DOM directly in HTML markup using a new set of attributes. and tags

**13. What are Proxies With Reactive Programming**

1. A Wrapper Object that lets you intercept and modify operations performed on the wrapped(object)
2. Allowing you t0 add custom behavior or validation to the object('s properties and methods)

Proxy is a kind of **decorator pattern**

``` javascript
const obj = {
     name: 'Ashu',
     age: 30;
}

const handler = {
     get: function(target, prop) {
          if (property === 'age') {
               return target[prop] + ' years old';
          } else {
               return target[prop];
          }
     }
};
const s = new Proxy(obj, handler);

console.log(s.age); //30 years old
```

**14. What are traps in the Proxy**
// Traps in Proxy
get, set, has, deleteProperty ....

**15. What Event Bubbling, capturing and Prevent Default**


**Reference**
1. https://frontendmasters.com/courses/vanilla-js-apps/
