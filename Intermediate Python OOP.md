## Object-Oriented Programming Paradigm

**Encapsulation** allows you to bundle data (attributes) and behaviors (methods) within a class to create a cohesive unit. By defining methods to control access to attributes and its modification, encapsulation helps maintain data integrity and promotes modular, secure code.

**Inheritance** enables the creation of hierarchical relationships between classes, allowing a subclass to inherit attributes and methods from a parent class. This promotes code reuse and reduces duplication.

**Abstraction** focuses on hiding implementation details and exposing only the essential functionality of an object. By enforcing a consistent interface, abstraction simplifies interactions with objects, allowing developers to focus on what an object does rather than how it achieves its functionality.

**Polymorphism** allows you to treat objects of different types as instances of the same base type, as long as they implement a common interface or behavior. _**Python’s duck typing**_ make it especially suited for polymorphism, as it allows you to access attributes and methods on objects without needing to worry about their actual class.

```python


class Dog:
    species = "Canis familiaris" # class Attributes

    def __init__(self, name, age): # constructor
        self.name = name # Instance Attributes
        self.age = age
    
    # Instance method
    def description(self):
        return f"{self.name} is {self.age} years old"

    # Another instance method
    def speak(self, sound):
        return f"{self.name} says {sound}" 
```

Class attributes are shared across all instances of a class, while instance attributes are unique to each instance, allowing individual objects to have their own attribute values.

### Why don't we use the new keyword for creating an instance of a class in Python?

---

### 🧩 **1. Python Uses `__new__()` and `__init__()` Internally**
- When you create an object like `obj = MyClass()`, Python internally calls:
  - `__new__()` → allocates memory and returns the instance.
  - `__init__()` → initializes the instance with given arguments.
- You don’t need to explicitly call `__new__()` unless you're doing something advanced (like customizing object creation in metaclasses).

---

### 🧠 **2. Simplicity and Readability**
- Python emphasizes **clean and readable syntax**.
- Using `MyClass()` is intuitive and consistent with Python’s philosophy of simplicity.

---

### 🏗️ **3. Dynamic and Flexible Object Model**
- Python is dynamically typed and doesn’t require explicit memory management.
- Object creation is abstracted away to keep the language high-level and flexible.

---


**How to Access the values**
```python
dog1 = Dog()

// Accessing Instance attribute

dog1.age
gog1.speak('Hello')

// Accessing Class Attributes

Dog.species

# Strange thing in Python (We can update the values):-

dog1.age = 10
dog1.age


dog1.species = "Felis silvestris"
dog1.species

```

### Q. Do we have private, public, and protected attributes like Java or not in Python?

Python **does not have strict access modifiers** like `private`, `protected`, and `public` as in Java or C++. Instead, it uses **naming conventions** to indicate the intended level of access:

---

### 🔓 **1. Public Attributes**
- **Default behavior**: All attributes and methods are public by default.
- You can access them freely from outside the class.

```python
class MyClass:
    def __init__(self):
        self.name = "Ashutosh"  # public attribute

obj = MyClass()
print(obj.name)  # ✅ Accessible
```

---

### 🛡️ **2. Protected Attributes**
- Indicated by a **single underscore** prefix: `_attribute`
- This is a **convention**, not enforcement. It signals: “This is for internal use.”
- Still accessible from outside, but discouraged.

```python
class MyClass:
    def __init__(self):
        self._salary = 5000  # protected attribute

obj = MyClass()
print(obj._salary)  # ⚠️ Accessible, but not recommended
```

---

### 🔒 **3. Private Attributes**
- Indicated by a **double underscore** prefix: `__attribute`
- Python performs **name mangling** to make it harder to access from outside.

```python
class MyClass:
    def __init__(self):
        self.__password = "secret"  # private attribute

obj = MyClass()
# print(obj.__password)  # ❌ AttributeError
print(obj._MyClass__password)  # ✅ Accessible via name mangling
```

---

### Q. Can we extend a child class from more than 1 parent class?

---

### 🧬 **What is Multiple Inheritance?**
It allows a class to inherit attributes and methods from **multiple base classes**.

```python
class Parent1:
    def greet(self):
        print("Hello from Parent1")

class Parent2:
    def farewell(self):
        print("Goodbye from Parent2")

class Child(Parent1, Parent2):
    pass

obj = Child()
obj.greet()     # Inherited from Parent1
obj.farewell()  # Inherited from Parent2
```

---

### ⚠️ **Things to Watch Out For**
Python uses the **Method Resolution Order (MRO)** to determine which method to call when there are conflicts (e.g., same method name in multiple parents).

You can check MRO using:
```python
print(Child.__mro__)
```

---

### 🧠 Behind the Scenes
Python uses the **C3 linearization algorithm** to resolve method calls in multiple inheritance. This ensures a consistent and predictable order.

---

### 🧪 **Example: Method Resolution Order (MRO)**

```python
class Parent1:
    def show(self):
        print("Parent1 show()")

class Parent2:
    def show(self):
        print("Parent2 show()")

class Child(Parent1, Parent2):
    pass

obj = Child()
obj.show()
```

#### 🔍 Output:
```
Parent1 show()
```

### ✅ Why?
Python uses **Method Resolution Order (MRO)** to decide which method to call. In this case, `Parent1` is listed first in the inheritance, so its `show()` method is used.

You can inspect MRO like this:
```python
print(Child.__mro__)
```

---

### 🧠 **Using `super()` in Multiple Inheritance**

Let’s modify the example to use `super()`:

```python
class Parent1:
    def show(self):
        print("Parent1 show()")
        super().show()

class Parent2:
    def show(self):
        print("Parent2 show()")

class Child(Parent1, Parent2):
    def show(self):
        print("Child show()")
        super().show()

obj = Child()
obj.show()
```

#### 🔍 Output:
```
Child show()
Parent1 show()
Parent2 show()
```

### ✅ Why?
- `super()` follows the MRO chain.
- In `Child`, `super().show()` calls `Parent1.show()`.
- In `Parent1`, `super().show()` calls `Parent2.show()`.

---

### 🔄 MRO Chain:
```python
Child → Parent1 → Parent2 → object
```

---

## 💎 Diamond Inheritance Problem

### 🧬 Structure:
```python
class A:
    def show(self):
        print("A")

class B(A):
    def show(self):
        print("B")

class C(A):
    def show(self):
        print("C")

class D(B, C):
    pass

obj = D()
obj.show()
```

### 🔍 Output:
```
B
```

### ✅ Why?
Python uses **C3 linearization** to determine the **Method Resolution Order (MRO)**. In this case, the MRO for class `D` is:

```python
D → B → C → A → object
```

So `D.show()` calls `B.show()` first.

---

## 🧠 C3 Linearization Algorithm Explained

C3 linearization is used to **compute the MRO** in a consistent and predictable way. It ensures:

1. **Preservation of local precedence order** (order in which base classes are listed).
2. **Monotonicity** (subclasses preserve the order of their parents).
3. **Consistency** (no ambiguity in method resolution).

### 🔧 How It Works (Simplified Steps):
For a class `D(B, C)`:
- Start with `D`'s parents: `[B, C]`
- Get MROs of `B` and `C`:
  - `B → [B, A, object]`
  - `C → [C, A, object]`
- Merge these lists with the direct parents `[B, C]` using the C3 algorithm:
  - Pick the first class that doesn’t appear later in any other list.
  - Repeat until all classes are merged.

### 📐 Result:
```python
D → B → C → A → object
```

---

## 🧪 Using `super()` in Diamond Inheritance

```python
class A:
    def show(self):
        print("A")

class B(A):
    def show(self):
        print("B")
        super().show()

class C(A):
    def show(self):
        print("C")
        super().show()

class D(B, C):
    def show(self):
        print("D")
        super().show()

obj = D()
obj.show()
```

### 🔍 Output:
```
D
B
C
A
```

### ✅ Why?
- `super()` follows the MRO.
- Each class calls the next one in the MRO chain.

---

## 🔍 View MRO Programmatically
```python
print(D.__mro__)
```


## Class Constructors: Control Your Object Instantiation

You trigger Python’s instantiation process whenever you call a Python class to create a new instance. This process runs 2 steps


1. Create a new instance of the target class
2. Initialize the new instance with an appropriate initial state


- To run the first step, Python classes have a special method called **.__new__()**, which is responsible for creating and returning a new empty object. 

- Then another special method, **.__init__()**, takes the resulting object, along with the class constructor’s arguments.

- The **.__init__()** method takes the new object as its first argument, **self**. 
- Then it sets any required instance attribute to a valid state using the arguments that the class constructor passed to it.

In short, Python’s instantiation process starts with a call to the class constructor, which triggers the instance creator, .__new__(), to create a new empty object. The process continues with the instance initializer, .__init__(), which takes the constructor’s arguments to initialize the newly created object.

To explore how Python’s instantiation process works internally, consider the following example of a Point class that implements a custom version of both methods, .__new__() and .__init__(), for demonstration purposes:

point.py
class Point:
    def __new__(cls, *args, **kwargs):
        print("1. Create a new instance of Point.")
        return super().__new__(cls)

    def __init__(self, x, y):
        print("2. Initialize the new instance of Point.")
        self.x = x
        self.y = y

    def __repr__(self) -> str:
        return f"{type(self).__name__}(x={self.x}, y={self.y})"

Great questions! Let's break them down one by one:

---

## 🧠 **1. What does `super()` do when no parent class is explicitly defined?**

Even though your `Point` class doesn't explicitly inherit from another class, **all Python classes implicitly inherit from `object`**, which is the base class for all classes in Python.

So this line:
```python
return super().__new__(cls)
```
is equivalent to:
```python
return object.__new__(cls)
```

### ✅ Why use `super()` here?

- It ensures compatibility with inheritance and MRO (Method Resolution Order).
- If you later extend `Point` into a subclass, `super()` will correctly delegate to the next class in the MRO chain.

---

## 🧠 **2. Why use `__repr__()` instead of `__str__()`?**

Both `__repr__()` and `__str__()` are used to define how an object is represented as a string, but they serve **different purposes**:

### ✅ Why use `__repr__()` here?
- It's more useful for debugging and logging.
- It shows the class name and internal state clearly.
- If `__str__()` is not defined, `__repr__()` is used as a fallback.

### Example:
```python
p = Point(1, 2)
print(p)        # Uses __repr__ if __str__ is not defined
print(repr(p))  # Always uses __repr__
```
---

### Should You Define .__repr__() and .__str__() in a Custom Class?

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed

    def __repr__(self) -> str:
        # Developer-friendly representation, useful for debugging
        return f"Dog(name='{self.name}', breed='{self.breed}')"

    def __str__(self) -> str:
        # User-friendly representation, used in print() and str()
        return f"{self.name} is a {self.breed}"

# Example usage
dog = Dog("Buddy", "Golden Retriever")

print(dog)        # Uses __str__() → Buddy is a Golden Retriever
print(repr(dog))  # Uses __repr__() → Dog(name='Buddy', breed='Golden Retriever')

# If __str__() is not defined, print(dog) will fallback to __repr__()
```

---

### 🧠 Key Comment:
> If `__str__()` is not defined, Python will automatically use `__repr__()` when calling `print()` or `str()` on the object.

Here’s a **simple explanation and example** of using an **Abstract Base Class (ABC)** in Python.

---

## 🧠 What is an Abstract Base Class?

An **Abstract Base Class** is a class that **cannot be instantiated directly** and is meant to be **inherited by other classes**. It defines **abstract methods** that **must be implemented** by any subclass.

Python provides this feature via the `abc` module.

---

## ✅ Why Use ABCs?

- To enforce a **common interface** across multiple classes.
- To ensure that subclasses **implement required methods**.
- Useful in large applications, frameworks, and APIs.

---

## 🐶 Simple Example: Abstract Class for Animals

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

# animal = Animal()  # ❌ Error: Can't instantiate abstract class
dog = Dog()
cat = Cat()

print(dog.speak())  # Woof!
print(cat.speak())  # Meow!
```

---

### 🔍 What’s Happening Here?

- `Animal` is an abstract base class.
- `speak()` is an abstract method—**must be implemented** by subclasses.
- You **cannot create an instance of `Animal`** directly.
- `Dog` and `Cat` are concrete classes that implement `speak()`.

---

Reference:-

- https://realpython.com/python3-object-oriented-programming/
- https://realpython.com/python-class-constructor/
- https://realpython.com/ref/glossary/abstract-base-class/
