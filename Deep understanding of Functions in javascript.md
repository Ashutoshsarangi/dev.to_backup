
1. Functions are First class Objects why?

Ans:- 
a. we can treat functions like other variables in JavaScript. how this is possible
b. When the compiler sees a function declaration/expression
it keeps the function in the memory along with an attachment of Object reference.
and return the function store reference to the variable.

c. so basically functions are function + Object combo.

2. What is function declaration vs function expression?

Ans:- 

**function declaration**

``` javascript

function functionDeclaration () {
console.log('This is function declaration);
}
```

**Function Expression**

a. Named Function Expression
b. Anonymous Function Expression

IIFE:- Immediate invoke Function Expression 3 types of function expression

``` javascript

const item = function namedFunctionExpression () {}


const anonymousFunctionExpression= function () {}
//Here anonymousFunctionExpression is storing/Refering an anonymous function 

Arrow function

Const temp = () => {}
```

Very Important:- (Clear Ideas on When to use Arrow fun and call , apply and bind also this reference.)

``` javascript
const user1 = {
scope: 1,
increment : () => {
  this.scope++; // Here this would be window Object
}

increament1: function () {
  console.log(this); // here this is who called this function
}

increment2: function () {
     function nested() {
       console.log(this); // Here this will check for who called it as it has nothing so this will be window. to resolve this problem we need call / APPly / Bind this to this function see increment3 func
     }
     nested();
     
}

increment3: function () {
   function nested() {
      console.log(this); // now it will have the this which was bind  with call
   }
   nested.call(this);
}

increment4: function () {
  const nested = () => {
     console.log(this); // here we will get this as who called this.
  }
  nested(); // because in arrow function ewe don't have this so it picks from lexical scope. So here we don't need external bindings 

}

function add() {

}

user1.increment();

```

1. When we call user1.increment() here user1 is this (keyword). 
2. when we directly call add1() by default windowObject = this (keyword)unless it uses the arrow function.
3. Inside arrow function it took this reference from lexical scope.

Arrow function is the newer Form of call, apply and bind methods.

Rule :-
methods inside functions should not be arrow functions. If we do so

**Function hierarchy**

named function Declaration > named Function Expression > Anonymous Function Expression



**SO Important note (rule to be followed)**

in side Objects functions function should be arrow function not the Objects function named function expression anonymous function expression Arrow function, normal function how does this change in both function types parameter , argument

this keyword depends on how the function is being called

**there are 4 ways a function is being called.**

1. **implicit binding **obj.fun(); here **this is obj**

**Explicitly Binding this **

2. .call()/.apply() /.bind() (hard bound). -> return a function

3. with new keyword

4. default binding (Normal fun call)
this as global/window in strict mode by default this is undefined

very important note

use strict mode global this would be undefined.

``` javascript 
 "use strict"
function fun() {
    console.log(this); // undefined
}

fun()
```

Arrow function does not have this keyword, so it lexically check the parent.

As per this behaviour it is called Lexical this .

``` javascript
let obj = {
teacher: 'asd',
ask: () => {
console.log(this)
}
}

obj.ask(); 
```

Here this will be refere to window OBject

**Why?**

Think lexically it will not be found inside the ask function and then it will go to its parent scope and the parent scope is window.

It is not the Obj Object.

**new of the Arrow function fails because it does not have the prototype property.**

because of that it throughs error

``` javascript
const fun1 = () => {
    console.log(this);
}

let ob = new fun1(); // Type Error, fun1 is not a constructor
```
