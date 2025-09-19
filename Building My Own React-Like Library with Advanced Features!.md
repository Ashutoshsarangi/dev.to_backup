I'm excited to share that I've finally managed to create my own React-like library with many features! 🎉 Here’s a glimpse of what it can do:

All the below features are achievable using Vanilla Javascript.

1. Global store management
2. Web component creation, using a component inside another component.
3. Browser routing
4. Shadow DOM integration for seamless updates
5. Observable pattern from Angular for action dispatching and more
6. Single Page Application

**_It’s been an incredible journey building this.🚀 _**

There are lots of Keynotes I would like to highlight

**1. Global store management**

``` javascript
const Store = {
    menu : null,
    cart : [],
};

const proxiedStore = new Proxy(Store, {
    set(target, prop, value) {
        target[prop] = value;
       ...
        return true;
    }
});
export default proxiedStore;
```
**2. Web component creation**

``` javascript
export class MenuPage extends  HTMLElement {
        constructor() {
          super();
       }
 connectedCallback() {} // It will trigger when It connected to the DOM
}
customElements.define("menu-page", MenuPage);
```
**3. Browser routing**

``` javascript
 // Event Handler when URL change directly in the browser
        window.addEventListener('popstate', e => {
            this.go(e.state.route);
        });
-----------------------
function (route, addToHistory = true) {
        console.log('Going to route --> ', route);
        if (addToHistory) {
            history.pushState({route}, '', route); 
            // This will add the route to the browser history
        }
switch (route) {
            case '/':
                pageElement = document.createElement('menu-page');
                break;
           ...
        }

}

        
```

**4. Shadow DOM integration for seamless updates**

// In a customeElement when we add this in side constructor we are saying to treat this as a shadow dom.

``` javascript
 this.root = this.attachShadow({mode: 'open'});

```
NOTE:-
The main reason to Adopt shadow dome, is because in a normal Custome Component let's say we inject style it will pollute our global style as well.

So when we have the Shadow DOM it will not Pollute. It maintains its own scope.

**5. Observable pattern from Angular for action dispatching**

``` javascript
// This will broadcast our event.
  window.dispatchEvent(new Event('appMenuUpdated'));
  window.addEventListener('appMenuUpdated', (e) => {});
```

**6. Single Page Application**

Here I use the routing technique which we discussed above along with Html Templates to update.


![Image "This is the landing page Where I added few Items in cart"](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mfp0gmc5vwwnh4xi4dpu.png)

![Image "I am Indide the cart"](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wdio3xbd7hzomt3evp4s.png)

![Image "Form Submission inside cart"](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tn3or09xbt9foqyid960.png)


After this, It broke a lot of my perspective, and the picture is clear now. How all the framework and Library work.


Reference:-
https://frontendmasters.com/courses/vanilla-js-apps/wrapping-up/
