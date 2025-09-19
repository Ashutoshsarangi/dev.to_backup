## What Is Functional Programming?

- A pure function is a function whose output value follows solely from its input values without any observable side effects.
- In functional programming, a program consists primarily of the evaluation of pure functions. 
- Computation proceeds by nested or composed function calls without changes to state or mutable data.

In Python, functions are **first-class citizens**.

- This means that functions have the same characteristics as values like strings and numbers. 
- Anything you would expect to be able to do with a string or number, you can also do with a function.

```python
>>> def func():
...     print("I am function func()!")
...

>>> func()
I am function func()!

>>> another_name = func
>>> another_name()
I am function func()!

**>>> def func():
...     print("I am function func()!")
...

>>> print("cat", func, 42)
cat <function func at 0x7f81b4d29bf8> 42**
```

## function composition / Higher order functions

- When you pass a function to another function, the passed-in function is sometimes referred to as a **callback**.
- function can also specify another function as its return value

```python
>>> def outer():
...     def inner():
...         print("I am function inner()!")
...     # Function outer() returns function inner()
...     return inner
...

>>> function = outer()
>>> function
<function outer.<locals>.inner at 0x7f18bc85faf0>
>>> function()
I am function inner()!

>>> outer()()
I am function inner()!
```

## Closure and bag Pack

- Python also supports closure and its bag pack concept (Lexical Persistent Reference value) L.P.R.V

```python
def outer():
    x = 23
    def inner():
        print(x, ' Inner')
    return inner;
    

inner_fun = outer()


inner_fun() 
```

## Defining an Anonymous Function With lambda

- Functional programming is all about calling functions and passing them around, so it naturally involves defining a lot of functions. 
- Sometimes, it’s convenient to be able to define an anonymous function on the fly without having to give it a name. In Python, you can do this with a **lambda expression**.

```python
lambda <parameter_list>: <expression>
(lambda x1, x2, x3: (x1 + x2 + x3) / 3)(9, 6, 6) # Self-invoking fun
(lambda x: "even" if x % 2 == 0 else "odd")(2)

>>> reverse = lambda s: s[::-1]
>>> reverse("I am a string")
'gnirts a ma I'
```

## Applying a Function to an Iterable With map()

```python
def reverse(s):
    return s[::-1]

animals = ["cat", "dog", "hedgehog", "gecko"]
x = list(map(reverse, animals))

print(x)
```
### Calling map() With Multiple Iterables

map(<f>, <iterable₁>, <iterable₂>, ..., <iterableₙ>)

```python


def add_three(a, b, c):
    return a + b + c


y = list(map(add_three, [1, 2, 3], [10, 20, 30], [100, 200, 300]))
print(y)

#[111,222,333] (1, 10, 100), (2, 20, 200)
```

## Selecting Elements From an Iterable With filter()

```python 
>>> def greater_than_100(x):
...     return x > 100
...
>>> list(filter(greater_than_100, [1, 111, 2, 222, 3, 333]))
[111, 222, 333]
```

## Reducing an Iterable to a Single Value With reduce()

reduce() applies a function to the items in an iterable two at a time, progressively combining them to produce a single result.

```python
def f(x, y):
...     return x + y
...

>>> from functools import reduce
>>> reduce(f, [1, 2, 3, 4, 5])
# 15
```

#### Calling reduce() With an Initial Value

```python 
>>> def f(x, y):
...     return x + y
...

>>> from functools import reduce
>>> reduce(f, [1, 2, 3, 4, 5], 100)  # (100 + 1 + 2 + 3 + 4 + 5)
115
```
