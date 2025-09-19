**Introduction:**
As we all know we use Node.js mostly for Servers for our applications, Which use javascript. but how it is connected to Network Of the Server section to get HTTP Object (information).

In this case, v8 came into the picture, We all know V8 is made out of C++, which has many features that can directly interact with the OS features.

Javascript does not, so it has to work with the c++ to control these computer features.

**This combination is known as Node.js**


**Node.js**

It is a language that does 3 things 

- Saves data and functionality (code)
- uses that data by running functionality (code) on it.
- has a ton of built-in labels that trigger node features that are built in C++ to use our computer's Internals

**Executing Node Code:-**

- we can set up with a javascript label, a Node.js features (and so Computer internals) to wait for requests for html/css/js tweets from our users

- How? The most powerful built-in Node feature of all: **http**
(and its associated built-in label in js -also HTTP conveniently)



**Using HTTP feature of Node (c++) to set up an open socket**

``` javascript
const server = http.createServer()
server.listen(80) 
```

inbound web request -> run code to send back the message 

**Q. if in bound message --> send back data but at what moment ?**

Ans:- We need to send a callback method that auto called from the v8 / (node & C++) features.

in next article we will have a diagram and detail explanation how it open Socket and port how it has automated Objected passed as an argument to the function.

Link to detail Discussion via diagram:- <W.I.P>


Reference:-
1. https://frontendmasters.com/courses/servers-node-js
