
## 0. What is OOP in Python?

**Definition (interview):**
OOP (Object-Oriented Programming) is a programming paradigm that organizes code into **classes and objects** to model real-world entities and their behavior.

**Simple meaning:**
Instead of writing everything with functions and variables scattered around, we group related data and functions inside **classes**.

---

## 1. Class

**Definition (interview):**
A **class** is a blueprint or template that defines the structure and behavior (data and methods) that its objects will have.

**Simple meaning:**
Class = design / plan.

**Example:**

```python
class Student:
    pass
```

**Common questions:**

* **Q:** What is a class?
  **A:** A class is a blueprint or template for creating objects that defines attributes and methods.

---

## 2. Object / Instance

**Definition (interview):**
An **object** (or instance) is a concrete entity created from a class. It represents an individual example of the class.

**Simple meaning:**
Object = actual thing built from the plan.

**Example:**

```python
class Student:
    pass

s1 = Student()  # s1 is an object
```

**Common question:**

* **Q:** What is the relation between class and object?
  **A:** A class defines the structure; an object is an instance of that class in memory.

---

## 3. Attributes (Instance Variables) & Methods

### 3.1 Attributes (Instance Variables)

**Definition (interview):**
An **attribute** or **instance variable** is a variable defined inside a class and associated with a specific object.

**Simple meaning:**
Data stored **inside** the object.

**Example:**

```python
class Student:
    def __init__(self, name):
        self.name = name  # attribute / instance variable

s1 = Student("Rahul")
print(s1.name)  # Rahul
```

---

### 3.2 Methods

**Definition (interview):**
A **method** is a function defined inside a class that operates on the object’s data.

**Simple meaning:**
Action that the object can perform.

**Example:**

```python
class Student:
    def __init__(self, name):
        self.name = name

    def greet(self):      # method
        print("Hello, I am", self.name)
```

**Common question:**

* **Q:** What is the difference between attribute and method?
  **A:** Attribute is data of the object; method is behavior or function acting on that data.

---

## 4. `__init__` (Constructor)

**Definition (interview):**
`__init__` is a special method called a **constructor** that automatically runs when an object is created and is used to initialize the object’s attributes.

**Simple meaning:**
Setup code that runs once when you create the object.

**Example:**

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

s1 = Student("Amit", 20)
```

**Common questions:**

* **Q:** What is `__init__`?
  **A:** It is the constructor method in Python classes used to initialize object attributes.
* **Q:** Is `__init__` mandatory?
  **A:** No, but it is commonly used when you need to initialize data.

---

## 5. `self` keyword

**Definition (interview):**
`self` is a reference to the current object (instance) of the class and is used to access instance variables and methods.

**Simple meaning:**
`self` = “this object”.

**Example:**

```python
class Demo:
    def show(self):
        print("Current object is:", self)
```

**Common questions:**

* **Q:** Why do we use `self` in Python methods?
  **A:** To refer to the instance calling the method and access its attributes.

---

## 6. Class Variables vs Instance Variables

### 6.1 Instance Variable

**Definition (interview):**
An **instance variable** is a variable defined inside `__init__` (or methods using `self`) and is unique to each object.

**Example:**

```python
class Employee:
    def __init__(self, name):
        self.name = name   # instance variable
```

### 6.2 Class Variable

**Definition (interview):**
A **class variable** is a variable defined directly in the class body and is shared by all objects of that class.

**Example:**

```python
class Employee:
    company = "Google"  # class variable

    def __init__(self, name):
        self.name = name
```

**Common question:**

* **Q:** Difference between class variable and instance variable?
  **A:** Class variables are shared by all objects; instance variables are specific to each object.

---

## 7. Types of Methods: Instance, Class, Static

### 7.1 Instance Method

**Definition (interview):**
An **instance method** is a method that takes `self` as the first parameter and works with instance variables.

```python
class Demo:
    def instance_method(self):
        print("Instance method")
```

---

### 7.2 Class Method

**Definition (interview):**
A **class method** is a method that takes `cls` as the first parameter and works with class-level data. It is defined using the `@classmethod` decorator.

```python
class Demo:
    count = 0

    @classmethod
    def show_count(cls):
        print(cls.count)
```

---

### 7.3 Static Method

**Definition (interview):**
A **static method** is a method that does not take `self` or `cls` and does not depend on instance or class data. It is defined with the `@staticmethod` decorator.

```python
class Demo:
    @staticmethod
    def add(x, y):
        return x + y
```

**Common question:**

* **Q:** When do you use a static method?
  **A:** When the logic is related to the class but doesn’t need instance or class variables.

---

## 8. Encapsulation

**Definition (interview):**
Encapsulation is the concept of **bundling data and methods together** in a class and **restricting direct access** to some of the data.

**How in Python:**
We use:

* `_var` → convention for “protected”
* `__var` → name mangling, treated as “private”

**Example:**

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # private attribute

    def get_balance(self):
        return self.__balance
```

**Common question:**

* **Q:** What is encapsulation in Python?
  **A:** It is the practice of keeping data and methods inside a class and restricting direct access using private or protected attributes.

---

## 9. Inheritance

**Definition (interview):**
Inheritance is a mechanism where one class (child/derived) acquires the properties and behaviors of another class (parent/base).

**Simple meaning:**
Child class reuses code from parent class.

**Example (Single Inheritance):**

```python
class Parent:
    def show(self):
        print("Parent")

class Child(Parent):
    def display(self):
        print("Child")
```

### Types of Inheritance (just definitions):

* **Single:** One parent → one child
* **Multiple:** Child has more than one parent
* **Multilevel:** Parent → Child → GrandChild
* **Hierarchical:** One parent → multiple children
* **Hybrid:** Combination of above

**Common questions:**

* **Q:** Why is inheritance used?
  **A:** To reuse existing code and extend functionality without rewriting.

---

## 10. `super()` Function

**Definition (interview):**
`super()` is a built-in function used to call methods of the parent class in a child class.

**Simple meaning:**
Use `super()` when the child wants to use or extend the parent’s behavior.

**Example:**

```python
class Parent:
    def __init__(self):
        print("Parent init")

class Child(Parent):
    def __init__(self):
        super().__init__()  # calls Parent __init__
        print("Child init")
```

**Common question:**

* **Q:** Why do we use `super()` in Python OOP?
  **A:** To access parent class methods or constructors from the child class.

---

## 11. Polymorphism

**Definition (interview):**
Polymorphism means **one name, many forms** – the same operation or method name behaves differently in different classes.

### 11.1 Method Overriding (Supported in Python)

**Definition (interview):**
When a child class provides its own implementation of a method already defined in its parent class.

**Example:**

```python
class Animal:
    def sound(self):
        print("Some sound")

class Dog(Animal):
    def sound(self):
        print("Bark")
```

### 11.2 Method Overloading (Not true overloading)

Python doesn’t support **true** method overloading by signature, but we can simulate using default arguments or `*args`.

**Common questions:**

* **Q:** What is method overriding?
  **A:** When a subclass defines a method with the same name as in the parent class but with a different implementation.

* **Q:** Does Python support method overloading?
  **A:** Not in the traditional way; the last defined method with the same name overrides previous ones. We usually use default parameters or `*args` instead.

---

## 12. Abstraction

**Definition (interview):**
Abstraction means **hiding internal details** and showing only the essential features to the user. In Python, this is implemented using **abstract classes** and **abstract methods** from the `abc` module.

**Simple meaning:**
Show what it does, hide how it does.

**Example:**

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, r):
        self.r = r

    def area(self):
        return 3.14 * self.r * self.r
```

**Common question:**

* **Q:** How is abstraction implemented in Python?
  **A:** Using abstract classes and `@abstractmethod` from the `abc` module.

---

## 13. Composition (Has-a Relationship)

**Definition (interview):**
Composition is a design principle where one class **contains** an object of another class, representing a **“has-a”** relationship.

**Simple meaning:**
A car **has a** engine.

**Example:**

```python
class Engine:
    def start(self):
        print("Engine start")

class Car:
    def __init__(self):
        self.engine = Engine()

    def start(self):
        self.engine.start()
        print("Car started")
```

**Common question:**

* **Q:** Difference between inheritance and composition?
  **A:** Inheritance is "is-a" relationship (Dog is an Animal). Composition is "has-a" relationship (Car has an Engine).

---

## 14. Dunder / Magic Methods

**Definition (interview):**
Dunder (double underscore) methods are **special methods** in Python that start and end with `__`, used to define object behavior like printing, addition, length, etc.

**Examples:** `__init__`, `__str__`, `__len__`, `__add__`, etc.

**Example:**

```python
class Book:
    def __init__(self, pages):
        self.pages = pages

    def __len__(self):
        return self.pages

b = Book(300)
print(len(b))  # 300
```

**Common question:**

* **Q:** What are magic methods in Python?
  **A:** Built-in special methods with double underscores that define how objects behave with operators and built-in functions.



Below is the **complete, clean, interview-ready explanation** of all types of inheritance in Python — with **definitions + perfect examples + diagram-style explanation**.
This includes your first question:

---

# ✅ **Does Python Support Multiple Inheritance?**

**Yes. Python fully supports *multiple inheritance*.**

### **Definition (Interview):**

Multiple inheritance means a child class can inherit from **more than one parent class**.

### **How It Works:**

Python uses **Method Resolution Order (MRO)** to decide which parent class method is executed when multiple parents have the same method.
MRO follows the **C3 linearization algorithm**.

### ✔ Example: Multiple Inheritance

```python
class Father:
    def skills(self):
        print("Father: Coding")

class Mother:
    def skills(self):
        print("Mother: Cooking")

class Child(Father, Mother):  # multiple inheritance
    pass

c = Child()
c.skills()  
```

### **Output (important):**

```
Father: Coding
```

### **Why?**

Because Python searches in this order:
**Child → Father → Mother → Object**
This is called **MRO (Method Resolution Order)**.

---

# ✅ **Now All Types of Inheritance (Definitions + Examples)**

---

# 1️⃣ **Single Inheritance**

### **Definition:**

One parent class → one child class.

### ✔ Example:

```python
class Animal:
    def eat(self):
        print("Eating")

class Dog(Animal):  # single inheritance
    def bark(self):
        print("Barking")

d = Dog()
d.eat()
d.bark()
```

---

# 2️⃣ **Multiple Inheritance**

(Already explained above—but giving a simple version here)

### **Definition:**

One child class inherits from **multiple parent classes**.

### ✔ Example:

```python
class A:
    def f1(self):
        print("A")

class B:
    def f2(self):
        print("B")

class C(A, B):  # multiple inheritance
    pass
```

---

# 3️⃣ **Multilevel Inheritance**

### **Definition:**

Parent → Child → GrandChild
A chain of inheritance.

### ✔ Example:

```python
class A:
    def f1(self):
        print("A")

class B(A):  # child of A
    def f2(self):
        print("B")

class C(B):  # child of B
    def f3(self):
        print("C")

c = C()
c.f1()
c.f2()
c.f3()
```

---

# 4️⃣ **Hierarchical Inheritance**

### **Definition:**

One parent class → multiple child classes.

### ✔ Example:

```python
class Parent:
    def show(self):
        print("Parent")

class Child1(Parent):
    pass

class Child2(Parent):
    pass

c1 = Child1()
c2 = Child2()
c1.show()
c2.show()
```

---

# 5️⃣ **Hybrid Inheritance**

### **Definition:**

Combination of two or more types of inheritance.

Usually: Multiple + Multilevel + Hierarchical.

### ✔ Example (Simple Hybrid):

```python
class A:
    def f1(self):
        print("A")

class B(A):      # multilevel
    def f2(self):
        print("B")

class C(A):      # hierarchical
    def f3(self):
        print("C")

class D(B, C):   # multiple inheritance
    def f4(self):
        print("D")

d = D()
d.f1()
d.f2()
d.f3()
d.f4()
```

### ✔ Why Hybrid Inheritance is tricky?

Because:

* Two parents may have same methods
* Python must decide which to call
* So it uses **MRO** to resolve conflicts

---

# 🎯 FINAL QUICK REVISION TABLE (VERY IMPORTANT FOR INTERVIEW)

| Type of Inheritance | Definition                  | Example Structure |
| ------------------- | --------------------------- | ----------------- |
| **Single**          | One parent → one child      | A → B             |
| **Multiple**        | Child has multiple parents  | A → C ← B         |
| **Multilevel**      | Parent → Child → Grandchild | A → B → C         |
| **Hierarchical**    | One parent → many children  | A → B, A → C      |
| **Hybrid**          | Combination of above        | mix of all        |


---

---

# ✅ **1. How do you achieve Encapsulation in Python?**

### ⭐ **Definition (Interview-Ready)**

Encapsulation is the concept of **hiding data** inside a class and **controlling access** to it using methods.
In Python, encapsulation is achieved using:

* **Public attributes** → accessible everywhere
* **Protected attributes (`_variable`)** → convention: treat as protected
* **Private attributes (`__variable`)** → name-mangled, not directly accessible

### ⭐ **Important: Python does NOT enforce strict access control.**

It uses **name-mangling** for private attributes.

---

### ✔ **Example of Encapsulation**

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # private variable

    def deposit(self, amount):   # public method
        self.__balance += amount

    def get_balance(self):
        return self.__balance

acc = BankAccount(1000)
acc.deposit(500)
print(acc.get_balance())  # 1500
```

👉 You cannot access `__balance` directly:
`acc.__balance` will raise an `AttributeError`.

👉 But internally Python renames it to `_BankAccount__balance`.

---

### ⭐ **Interview Answer (Short)**

**Encapsulation is achieved using private (`__var`) and protected (`_var`) variables along with public getter/setter methods to control access to the data. Python uses name-mangling to internally protect private attributes.**

---

# ✅ **2. What is the difference between `__str__` and `__repr__`?**

### ⭐ **Definition (Interview-Ready)**

| Method     | Purpose                                                   | Used For           |
| ---------- | --------------------------------------------------------- | ------------------ |
| `__str__`  | Nice, readable, user-friendly string                      | end-users          |
| `__repr__` | Official, unambiguous representation (developer friendly) | debugging, logging |

### ⭐ Example:

```python
class Book:
    def __init__(self, pages):
        self.pages = pages

    def __str__(self):
        return f"Book with {self.pages} pages"

    def __repr__(self):
        return f"Book(pages={self.pages})"

b = Book(200)

print(str(b))   # Book with 200 pages
print(repr(b))  # Book(pages=200)
```

### ⭐ **Interview Answer (Short):**

* `__str__` is for **readable** output intended for **users**.
* `__repr__` is for **unambiguous** output intended for **developers**, ideally something that can recreate the object.
* If `__str__` is not defined, Python calls `__repr__`.

---

# 🎯 **Now Adobe-Level OOP + Python Tricky Questions with Answers**

These questions are asked to check **deep understanding**.

---

# ⚡ **Tricky OOP Questions (Adobe-Level)**

---

## **Q1: What happens if both parent classes have the same method in multiple inheritance?**

**Answer:**
Python resolves this using **MRO (Method Resolution Order)**.
The order is determined by **C3 Linearization**.

```python
class A:
    def show(self): print("A")

class B:
    def show(self): print("B")

class C(A, B):
    pass

c = C()
c.show()  # A
```

---

## **Q2: Can we access a private variable in Python?**

**Answer:**
Yes, indirectly using **name-mangling**:

```python
obj._ClassName__privateVar
```

But it’s **not recommended**. Private variables are meant to show intent.

---

## **Q3: Does Python support method overloading?**

**Answer:**
No traditional method overloading.
Python only keeps the **last defined method**.

But we simulate overloading using:

* default arguments
* `*args` and `**kwargs`

```python
def add(self, x, y=0, z=0):
    return x + y + z
```

---

## **Q4: What is the difference between `is` and `==` ?**

| Operator | Checks                            |
| -------- | --------------------------------- |
| `==`     | value equality                    |
| `is`     | reference identity (same memory?) |

```python
a = [1,2]
b = [1,2]
a == b  # True
a is b  # False
```

---

## **Q5: What will happen if you don’t write `__init__` in a class?**

**Answer:**
Python uses the **default constructor** that does nothing.
Object still gets created.

---

## **Q6: What is the purpose of the `super()` keyword with example?**

**Answer:**
To call the parent’s method or constructor.

---

## **Q7: What will happen? (Tricky)**

```python
class A:
    def __init__(self):
        print("A")

class B(A):
    pass

obj = B()
```

**Answer:**
Even though B has no constructor, it inherits A’s constructor → **prints A**.

---

## **Q8: Why is composition preferred over inheritance sometimes?**

**Answer:**
Because composition provides **loose coupling**, better flexibility, and avoids the complexity of deep inheritance trees.

**Example:**
A Car *has an* Engine → composition.

---

## **Q9: How does Python handle multiple constructors?**

```python
class A:
    def __init__(self):
        print("First")

    def __init__(self):
        print("Second")
```

**Answer:**
Python keeps only the **last** `__init__`.
Output: `Second`

---

## **Q10: What is duck typing in Python?**

**Answer:**
“If it looks like a duck and quacks like a duck, it is a duck.”
Python doesn’t check *type*, it checks *behavior*.

```python
class A:
    def sound(self): print("Meow")

class B:
    def sound(self): print("Bark")

def make_sound(obj):
    obj.sound()

make_sound(A())
make_sound(B())
```

Python doesn't care about the class, only the method.

---

# ⚡ **Even More Tricky Python (Core Basics + OOP) Questions for Adobe**

---

## **Q11: What is the output?**

```python
a = 10
b = a
a = 20
print(b)
```

**Answer:**
`10` (integers are immutable)

---

## **Q12: What will this print?**

```python
class Test:
    x = []

t1 = Test()
t2 = Test()

t1.x.append(1)

print(t2.x)
```

**Answer:**
`[1]`
Because `x` is a **class variable**, shared across all objects.

---

## **Q13: Output?**

```python
class A:
    y = 10

a1 = A()
a2 = A()

a1.y = 20
print(a2.y)
```

**Answer:**
`10`
Because `a1.y = 20` creates an **instance variable**, does not modify class variable.

---

## **Q14: What will this print?**

```python
class A:
    def __repr__(self):
        return "repr-called"

    def __str__(self):
        return "str-called"

obj = A()
print(obj)
```

**Answer:**
`str-called`
Because `print()` uses `__str__`.
`repr-called` would appear if we do:

```python
repr(obj)
```

---

## **Q15: Why doesn’t Python have true private variables?**

**Answer:**
Because Python follows **"we are all adults here" philosophy**.
It focuses on **name-mangling** instead of strict restrictions.

---




---

# 🐍 Python Interview Q&A (Beginner-Friendly + F2F Ready)

---

## 1️⃣ **What is the use of the `self` keyword in Python?**

`self` represents the **current instance of the class**.
Whenever we create an object, `self` helps Python understand **which object’s variables or methods** we want to access.

### Why is it used?

* To access **instance variables**
* To access **instance methods**
* To differentiate **class variables vs. object variables**

### Simple Explanation

“`self` is like saying *this object*.”

### Example:

```python
class Student:
    def __init__(self, name):
        self.name = name  # refers to this object's 'name'
```

---

## 2️⃣ **What is a lambda function in Python?**

A **lambda function** is a small, anonymous function created with the `lambda` keyword.

### When is it useful?

* When you need a quick function for a short time
* In places like sorting, filtering, mapping
* When writing one-line logic

### Example:

```python
square = lambda x: x * x
```

### Why use lambda?

* Saves time
* Makes code cleaner for short operations

---

## 3️⃣ **Difference between `range` and `xrange` in Python 2.x**

| Feature  | `range`             | `xrange`                         |
| -------- | ------------------- | -------------------------------- |
| Output   | Creates a full list | Creates values one by one (lazy) |
| Memory   | High                | Very low                         |
| Speed    | Slower              | Faster for loops                 |
| Python 3 | Exists              | Removed                          |

### F2F Explanation

In Python 2, `range()` loads the entire sequence into memory.
`xrange()` generates numbers **on demand**, so it is memory-efficient.

In Python 3, **only `range` exists**, and it works like `xrange`.

---

## 4️⃣ **Purpose of the `__init__` method in Python**

`__init__` is the **constructor** of a class.
It runs **automatically** when an object is created.

### Uses:

* Initialize object variables
* Setup default values
* Preparing the object for usage

### Example:

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model
```

**Simple Meaning:**
It is the **starting point** of every object.

---

## 5️⃣ **How to check the type of a variable in Python?**

Use the `type()` function.

### Example:

```python
x = 10
print(type(x))  # <class 'int'>
```

### Why useful in interviews?

* To debug
* To understand data type differences
* Used in dynamic typing languages like Python

---

## 6️⃣ **Difference between `is` and `==` in Python**

| Keyword | Meaning           | Checks                       |
| ------- | ----------------- | ---------------------------- |
| `==`    | Equality operator | Compares **values**          |
| `is`    | Identity operator | Compares **memory location** |

### Interview Example:

```python
a = [1, 2]
b = [1, 2]

a == b   # True → values are same  
a is b   # False →  different objects  
```

### Short Explanation

* Use `==` when comparing **values**.
* Use `is` when checking if **both references point to the same object**.

---

## 7️⃣ **What are decorators in Python and how are they used?**

A **decorator** is a function that **modifies or enhances** another function **without changing its actual code**.

### What can decorators do?

* Add logging
* Add authentication
* Measure execution time
* Reuse common functionality

### Example:

```python
def my_decorator(func):
    def wrapper():
        print("Before function")
        func()
        print("After function")
    return wrapper

@my_decorator
def greet():
    print("Hello")
```

### F2F Explanation

Decorators are widely used in frameworks like **Flask**, **FastAPI**, **Django** to handle routing, permissions, etc.

---

## 8️⃣ **What is Python, and how is Python useful?**

Python is a **high-level, interpreted, easy-to-learn language** widely used today.

### Why is Python so popular?

* Very simple syntax
* Huge standard library
* Massive community support
* Ideal for beginners and experts

### Where is Python used?

* Web development
* Machine Learning
* Generative AI
* Scripting and automation
* Data Science
* Backend development
* Cloud & DevOps

### F2F Note

Companies choose Python because it reduces development time and is flexible across many domains.

---

## 9️⃣ **How do you create a function in Python?**

Use the `def` keyword.

### Example:

```python
def greet(name):
    print("Hello, " + name)
```

### Why functions?

* Reusability
* Clean code
* Avoid repetition
* Better organization

---

## 🔟 **Difference between List and Tuple in Python**

| Feature     | List                 | Tuple                        |
| ----------- | -------------------- | ---------------------------- |
| Mutability  | Mutable (can change) | Immutable (cannot change)    |
| Performance | Slower               | Faster                       |
| Syntax      | `[ ]`                | `( )`                        |
| Use case    | When data changes    | When data must stay constant |

### Interview Example:

Use **tuple** for things like:

* Days of week
* Coordinates
* Config values

### Simple Explanation

A **tuple is like a locked list**.

---

## 1️⃣1️⃣ **What is a module in Python?**

A module is simply a **Python file** (.py) that contains **functions, variables, or classes**.

### Why use modules?

* Break large programs into smaller parts
* Reuse code
* Maintain clean structure

### Example:

File: `math_utils.py`

```python
def add(a, b):
    return a + b
```

Import it:

```python
import math_utils
```

---

## 1️⃣2️⃣ **Difference between `break` and `continue` in Python**

### `break`

* Immediately stops the **entire loop**
* Used when a certain condition is met and you don't want to continue looping

### `continue`

* Skips the **current iteration**
* Moves to the next iteration of the loop

### Example:

```python
for i in range(5):
    if i == 3:
        break   # stops at 3
```

```python
for i in range(5):
    if i == 3:
        continue   # skips 3
```

---

## **13️⃣ How do you iterate over a list in Python?**

You can iterate using a simple **for loop**, which reads each item one by one.

### Example:

```python
fruits = ["apple", "banana", "mango"]

for item in fruits:
    print(item)
```

### Why interviewers ask this:

To test your understanding of loops and sequences.

---

## **14️⃣ Write a Python factorial program without using if-else, for-loop, or ternary operators.**

We can calculate factorial using **recursion**.

### Example:

```python
def factorial(n):
    return 1 if n == 0 else n * factorial(n - 1)
```

Or using the built-in module:

```python
import math
print(math.factorial(5))
```

---

## **15️⃣ What is the difference between deep and shallow copying of an object in Python?**

| Copy Type        | What it Copies           | Behavior on Nested Objects           |
| ---------------- | ------------------------ | ------------------------------------ |
| **Shallow Copy** | Only top-level object    | Nested objects share references      |
| **Deep Copy**    | All objects (full clone) | Nested objects are fully independent |

### Example:

```python
import copy
shallow = copy.copy(obj)
deep = copy.deepcopy(obj)
```

---

## **16️⃣ How does garbage collection work in Python?**

Python uses:

1. **Reference Counting** – object deleted when reference count becomes zero
2. **Generational Garbage Collector** – handles circular references

### Simple Meaning:

Python automatically frees unused memory.

---

## **17️⃣ What is the difference between `append()` and `extend()` methods in Python lists?**

| Method             | Purpose             | Example Behavior               |
| ------------------ | ------------------- | ------------------------------ |
| `append(x)`        | Adds **one item**   | Adds item as a single element  |
| `extend(iterable)` | Adds multiple items | Adds each element individually |

### Example:

```python
a = [1, 2]
a.append([3, 4])   # [1, 2, [3, 4]]
a.extend([3, 4])   # [1, 2, 3, 4]
```

---

## **18️⃣ What is the purpose of the `yield` keyword in Python?**

`yield` turns a function into a **generator**, which:

* Returns values one at a time
* Saves memory
* Pauses and resumes execution

### Example:

```python
def gen():
    yield 1
    yield 2
```

---

## **19️⃣ What is the difference between a static method and a class method in Python?**

| Method Type       | First Argument      | Purpose                       |
| ----------------- | ------------------- | ----------------------------- |
| **Static Method** | No default argument | Utility function inside class |
| **Class Method**  | `cls`               | Access/modify class data      |

### Example:

```python
class A:
    @staticmethod
    def sm():
        return "static"

    @classmethod
    def cm(cls):
        return "class"
```

---

## **2️⃣0️⃣ How can you create a generator in Python?**

Two ways:

### ✔ Using `yield`:

```python
def my_gen():
    for i in range(5):
        yield i
```

### ✔ Using generator expression:

```python
gen = (x*x for x in range(5))
```

---

## **21️⃣ What is the difference between the `map` and `filter` functions in Python?**

| Function     | Purpose                         | Output                                |
| ------------ | ------------------------------- | ------------------------------------- |
| **map()**    | Transform each item             | Returns transformed items             |
| **filter()** | Select items based on condition | Returns items where condition is True |

### Example:

```python
map_result = list(map(lambda x: x*2, [1,2,3]))
filter_result = list(filter(lambda x: x%2==0, [1,2,3,4]))
```

---

## **22️⃣ How can you handle exceptions in Python?**

Using `try`, `except`, `else`, and `finally`.

### Example:

```python
try:
    x = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero")
finally:
    print("Execution complete")
```

---

## **23️⃣ What is the difference between a module and a package in Python?**

| Feature  | Module            | Package                   |
| -------- | ----------------- | ------------------------- |
| Meaning  | Single `.py` file | Folder containing modules |
| Contains | Code              | `__init__.py` file        |
| Examples | `math`, `os`      | `numpy`, `pandas`         |

---

## **24️⃣ What are some built-in data structures in Python, and how are they used?**

Python provides:

* **List** → Mutable, ordered collection
* **Tuple** → Immutable, ordered
* **Set** → Unique elements, unordered
* **Dictionary** → Key-value pairs

### When to use:

* List → general purpose
* Tuple → fixed data
* Set → avoid duplicates
* Dict → fast lookup

---

## **25️⃣ What is the difference between mutable and immutable data types in Python?**

| Type          | Can Change? | Examples               |
| ------------- | ----------- | ---------------------- |
| **Mutable**   | Yes         | list, dict, set        |
| **Immutable** | No          | int, str, tuple, float |

### Explanation:

Mutable objects change **in-place**.
Immutable objects create **new objects** on modification.

---

## **26️⃣ What is the difference between `==` and `is` in Python?**

* `==` → compares **values**
* `is` → compares **memory location**

### Example:

```python
a = [1,2]
b = [1,2]

a == b  # True
a is b  # False
```

---

## **27️⃣ What is the difference between a shallow copy and a deep copy in Python?**

(Repeated but required)

* **Shallow copy** → Only top-level copied
* **Deep copy** → Full independent clone including nested objects

Use `copy.copy()` and `copy.deepcopy()`.

---

## **28️⃣ How are arguments passed in Python — by value or by reference?**

Python uses **Pass-by-Object-Reference**.

### Meaning:

* Mutable objects → changes reflect outside
* Immutable objects → changes don’t reflect

---

## **29️⃣ How do you convert a list into a set?**

Use `set()` constructor.

### Example:

```python
my_list = [1,2,3,1]
my_set = set(my_list)
```

---

## **30️⃣ How can you create an empty NumPy array in Python?**

Using NumPy:

### 1. Completely empty array:

```python
import numpy as np
arr = np.array([])
```

### 2. Uninitialized empty array of given shape:

```python
arr = np.empty((3,3))
```

### 3. Zeros array:

```python
arr = np.zeros((3,3))
```

---
Here is the **next batch**, continuing numbering **from Question 31**, written in the **same GitHub-style, descriptive, and beginner-friendly format**, suitable for **face-to-face interviews**.

---


---

## **31️⃣ What are Pickling and Unpickling in Python?**

### ✔ Pickling

Pickling is the process of **converting a Python object into a byte stream** so it can be:

* stored in a file
* sent over a network
* saved for later use

### ✔ Unpickling

Unpickling is the reverse — **converting byte stream back into a Python object**.

### Example:

```python
import pickle

data = {"name": "John", "age": 30}

# Pickling
with open("data.pkl", "wb") as f:
    pickle.dump(data, f)

# Unpickling
with open("data.pkl", "rb") as f:
    loaded_data = pickle.load(f)
```

---

## **32️⃣ Code snippet to get, delete, and update an element in an array**

Using the built-in `array` module:

```python
import array

arr = array.array('i', [1, 2, 3, 4, 5])

# Get element
element = arr[2]      # → 3

# Update element
arr[2] = 30           # [1, 2, 30, 4, 5]

# Delete element
del arr[1]            # [1, 30, 4, 5]
```

---

## **33️⃣ What is a lambda function? How is it written in Python?**

A lambda function is a **small, anonymous function** written in a single line.

### Syntax:

```python
lambda arguments: expression
```

### Example:

```python
square = lambda x: x * x
print(square(5))  # 25
```

### When useful?

* For short operations
* In `map`, `filter`, `reduce`
* Inline functions

---

## **34️⃣ How can random numbers be generated in Python?**

Using the **random** module:

```python
import random

print(random.randint(1, 10))     # Random integer
print(random.random())           # Random float 0 to 1
print(random.uniform(1, 5))      # Random float between given range
```

---

## **35️⃣ How can you randomize the items of a list in place in Python?**

Use `random.shuffle()`.

### Example:

```python
import random

items = [1, 2, 3, 4, 5]
random.shuffle(items)
print(items)
```

This changes the list **in place**, meaning no new list is created.

---

## **36️⃣ What are generators in Python?**

Generators are **functions that return values one at a time using `yield`** instead of returning everything at once.

### Benefits:

* Memory efficient
* Useful for large datasets
* Lazy evaluation

### Example:

```python
def gen_nums():
    for i in range(5):
        yield i
```

---

## **37️⃣ What are iterators in Python?**

An iterator is an object that:

* Returns data **one element at a time**
* Implements `__iter__()` and `__next__()`

### Example:

```python
my_list = [1, 2, 3]
it = iter(my_list)

print(next(it))  # 1
print(next(it))  # 2
```

### Difference from Generators:

* Generators are a **simpler way** to create iterators
* Iterators require class methods

---

## **38️⃣ What does `*args` and `**kwargs` stand for in Python?**

### ✔ `*args`

Used to pass **variable number of positional arguments**.

```python
def func(*args):
    print(args)

func(1, 2, 3)
```

### ✔ `**kwargs`

Used to pass **variable number of keyword arguments**.

```python
def func(**kwargs):
    print(kwargs)

func(name="John", age=25)
```

### Interview Note

Very important for building flexible functions.

---

## **39️⃣ What are modules and packages in Python?**

### ✔ Module

A **single Python file** (`.py`) containing functions, classes, or variables.

Example: `math.py`, `os.py`

### ✔ Package

A **collection of modules in a folder**, containing `__init__.py`.

Example: `numpy`, `pandas`

### Key Difference:

* Module → One file
* Package → Folder containing multiple modules

---

## **4️⃣0️⃣ How can one create classes in Python?**

Using the `class` keyword.

### Example:

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def start(self):
        print("Car started")
```

### Steps:

1. Define class
2. Initialize variables using `__init__`
3. Add methods

---

## **4️⃣1️⃣ How do you initialize an empty class in Python?**

Two ways:

### 1. Using `pass`

```python
class Empty:
    pass
```

### 2. Using `__init__` with no variables

```python
class Empty:
    def __init__(self):
        print("Empty class created")
```

---

## **4️⃣2️⃣ How are access specifiers used in Python?**

Python has **3 types of access modifiers**:

| Type      | Syntax      | Meaning                                           |
| --------- | ----------- | ------------------------------------------------- |
| Public    | normal_name | Accessible everywhere                             |
| Protected | `_name`     | Should not be accessed outside class (convention) |
| Private   | `__name`    | Name-mangled, not accessible directly             |

### Example:

```python
class A:
    def __init__(self):
        self.public = 1
        self._protected = 2
        self.__private = 3
```

### Note

Python does not enforce strict access control; it follows naming conventions.


---

## **43️⃣ Is it possible to call the parent class without creating its instance? How can parent members be accessed inside a child class?**

### ✔ Yes, you can call the parent class **without creating an instance** using:

* `super()`
* Direct class name, e.g., `Parent.method(self)`

### ✔ Accessing parent members:

1. Using `super()`

```python
class Parent:
    def show(self):
        print("Parent")

class Child(Parent):
    def display(self):
        super().show()   # calling parent method
```

2. Using the class name

```python
Parent.show(self)
```

### Why asked?

To test inheritance concepts and method resolution.

---

## **44️⃣ How can you check if a class is a child of another class in Python?**

Use the built-in function **`issubclass()`**.

### Example:

```python
class A: pass
class B(A): pass

issubclass(B, A)   # True
```

Or for objects:

```python
isinstance(obj, ClassName)
```

---

## **45️⃣ Write a one-liner to count the number of capital letters in a file. (Works for large files)**

Use a generator expression:

```python
sum(1 for line in open("file.txt") for ch in line if ch.isupper())
```

This does **not** load the entire file into memory.

---

## **46️⃣ What is the `main` function in Python? How do you invoke it?**

Python executes code **top to bottom**, but the `main` block is used to control script execution.

### Definition:

`if __name__ == "__main__":`
This block runs **only when the script is executed directly**, not when imported.

### Example:

```python
def main():
    print("Running main")

if __name__ == "__main__":
    main()
```

---

## **47️⃣ Are there any tools for identifying bugs and performing static analysis in Python?**

Yes, popular static analysis tools are:

* **pylint**
* **flake8**
* **pyflakes**
* **mypy** (type checking)
* **bandit** (security analysis)

These tools help detect errors **before** running the code.

---

## **48️⃣ What are unit tests in Python?**

Unit tests are **small tests written to check individual units** (functions/modules).

### Python provides:

`unittest` module (built-in) and tools like:

* `pytest`
* `nose2`

Unit tests ensure code correctness and stability.

---

## **49️⃣ What are decorators, and how are they used in Python?**

A decorator is a function that **wraps another function**, adding extra functionality without modifying its actual code.

### Example:

```python
def log(func):
    def wrapper():
        print("Before")
        func()
        print("After")
    return wrapper

@log
def hello():
    print("Hello")
```

Used in: authentication, routing (Flask, Django), logging, caching.

---

## **50️⃣ What are Python packages?**

A package is a **collection of modules** organized into a folder containing an **`__init__.py`** file.

Example:

```
numpy/
 ├── core/
 ├── linalg/
 └── __init__.py
```

Packages help organize large projects.

---

## **51️⃣ What is the difference between a generator and a coroutine in Python?**

| Feature      | Generator              | Coroutine                               |
| ------------ | ---------------------- | --------------------------------------- |
| Purpose      | Produce data           | Consume data, multitask                 |
| Uses `yield` | Yes                    | Yes, but can accept values via `send()` |
| Execution    | One-way (pause/resume) | Two-way (send/receive data)             |

Generators → data streams
Coroutines → asynchronous programming

---

## **52️⃣ Ways to improve Python application performance**

* Use built-in functions (optimized in C)
* Use **NumPy**, **Pandas** for data-heavy tasks
* Apply **caching** (`functools.lru_cache`)
* Use **multiprocessing** / **asyncio**
* Use generators instead of lists
* Avoid deep nesting
* Use PyPy interpreter

---

## **53️⃣ What is the purpose of the `asyncio` library in Python?**

`asyncio` is used for **asynchronous programming** → helps run tasks concurrently without blocking.

Used for:

* Networking
* Web scrapers
* Fast I/O operations
* Servers (FastAPI, aiohttp)

Example:

```python
import asyncio

async def task():
    print("Hello")
    await asyncio.sleep(1)
```

---

## **54️⃣ How can you optimize memory usage in Python?**

* Use **generators** instead of lists
* Use `__slots__` in classes
* Delete unused variables with `del`
* Use efficient data structures (`array`, `deque`)
* Use `gc.collect()` when needed
* Avoid creating unnecessary copies

---

## **55️⃣ Best practices for large-scale Python applications**

* Follow PEP8 conventions
* Use virtual environments
* Proper folder/package structure
* Write unit tests
* Apply logging instead of print
* Use type hints (`mypy`)
* Use design patterns (MVC, factory, singleton)
* Break the project into modules/packages

---

## **56️⃣ How to implement multithreading and multiprocessing in Python? (Definition first)**

### ✔ Multithreading

Multiple threads run **within the same process**.
Best for **I/O-bound** tasks (waiting for network, file, API calls).

### ✔ Multiprocessing

Multiple processes run in **separate memory spaces**.
Best for **CPU-bound** tasks (heavy computations).

### Example:

```python
from threading import Thread
from multiprocessing import Process
```

---

## **57️⃣ What is metaprogramming in Python?**

Metaprogramming means **writing code that modifies or creates other code**.

Examples:

* Decorators
* Metaclasses
* Dynamic class creation
* Using `type()` to modify classes

---

## **58️⃣ What is the Global Interpreter Lock (GIL)?**

GIL is a mechanism that **allows only one thread to run Python bytecode at a time**.

### Effects:

* Multithreading is limited for CPU-heavy tasks
* But works fine for I/O-bound tasks

Used in CPython for memory safety.

---

## **59️⃣ What is the `swapcase()` function in Python?**

It converts uppercase letters → lowercase, and lowercase → uppercase.

### Example:

```python
"Hello World".swapcase()
# output: hELLO wORLD
```

---

## **60️⃣ Explain all file processing modes in Python**

| Mode        | Meaning             |
| ----------- | ------------------- |
| `r`         | read                |
| `w`         | write (clears file) |
| `a`         | append              |
| `r+`        | read + write        |
| `w+`        | write + read        |
| `a+`        | append + read       |
| `rb` / `wb` | binary modes        |

---

## **61️⃣ What are file-related modules in Python? Examples?**

Useful modules:

* `os` → file system operations
* `shutil` → copy, move files
* `pathlib` → modern file path handling
* `glob` → pattern matching
* `csv` → read/write CSV files
* `json` → read/write JSON

---

## **62️⃣ Difference between opening a file normally vs using `with` statement**

### Normal:

```python
f = open("data.txt")
# work
f.close()   # must manually close
```

### Using `with`:

```python
with open("data.txt") as f:
    data = f.read()
```

✔ Automatically closes file
✔ Prevents memory leaks
✔ Handles exceptions safely

---

## **63️⃣ How will you read a random line from a file?**

Approach:

```python
import random

lines = open("file.txt").read().splitlines()
print(random.choice(lines))
```

For huge files:

```python
import random
import linecache

line_number = random.randint(1, 10000)
print(linecache.getline("file.txt", line_number))
```

---

## **64️⃣ Why isn’t all memory deallocated after Python program ends?**

* Python uses **reference counting + garbage collector**
* Some objects are kept for **reuse (interning)**
* Memory allocated by C libraries may persist
* OS-level fragmentation

---

## **65️⃣ How are arguments passed in Python — by value or reference?**

Python uses **Pass-by-object-reference**.

Meaning:

* Mutable → changes affect original
* Immutable → changes do NOT affect original

---

## **66️⃣ Difference between `del` and `remove()` in Python lists**

| Operation     | What it does                          |
| ------------- | ------------------------------------- |
| `remove(x)`   | Removes first occurrence of value `x` |
| `del list[i]` | Deletes item at index `i`             |
| `del list`    | Deletes entire list                   |

---

## **67️⃣ How does multithreading work in Python?**

* Python supports threads using `threading` module
* Only **one thread executes at a time** due to GIL
* Good for **I/O-bound tasks**, not CPU-bound tasks

---

## **68️⃣ How does Flask handle database requests?**

Flask itself is lightweight, but database operations are handled using:

* **ORMs like SQLAlchemy**
* **DB connectors** (psycopg2, pymysql)
* **Flask extensions** (Flask-SQLAlchemy)

### Flask request → route → DB operation → response

Example:

```python
from flask_sqlalchemy import SQLAlchemy
db = SQLAlchemy(app)

user = User.query.filter_by(id=1).first()
```

---
Below is the **next batch**, continuing numbering from **69**, written in the same **GitHub-style, descriptive, face-to-face friendly** format.

---


---

## **69️⃣ How to save an image locally in Python when the URL is already known?**

You can use either **urllib** or **requests**.
The simplest method is using the `requests` module.

### ✔ Using `requests`

```python
import requests

url = "https://example.com/sample.png"
img_data = requests.get(url).content

with open("image.png", "wb") as f:
    f.write(img_data)
```

### ✔ Using `urllib`

```python
import urllib.request

url = "https://example.com/sample.png"
urllib.request.urlretrieve(url, "image.png")
```

### Interview Explanation

This shows your understanding of **HTTP requests, file I/O, and binary data handling**.

---

## **70️⃣ What is meant by functional programming? Does Python support it?**

### ✔ Functional Programming

A programming style where:

* Functions are treated as **first-class citizens**
* Code avoids changing state (no mutation)
* Focus is on **what to solve**, not **how to solve**
* Uses pure functions, higher-order functions, recursion

### ✔ Does Python support functional programming?

**Yes**, Python partially supports functional programming.

### ✔ Functional-style tools in Python:

* `map()`
* `filter()`
* `reduce()` (in `functools`)
* `lambda` functions
* List comprehensions
* Generator expressions
* Higher-order functions (functions returning functions)

### Example:

```python
numbers = [1, 2, 3, 4]
squared = list(map(lambda x: x*x, numbers))
```

Python is **multi-paradigm**: supports **OOP**, **procedural**, and **functional** styles.

---

## **71️⃣ How will you access the dataset of a publicly shared Google Drive spreadsheet in CSV format?**

To access a Google Sheet published as CSV:

### ✔ Convert Google Sheet link to CSV link

If your Google Sheet link is:

```
https://docs.google.com/spreadsheets/d/FILE_ID/edit?usp=sharing
```

Use this format:

```
https://docs.google.com/spreadsheets/d/FILE_ID/export?format=csv
```

### ✔ Python code to download CSV:

```python
import pandas as pd

csv_url = "https://docs.google.com/spreadsheets/d/FILE_ID/export?format=csv"
df = pd.read_csv(csv_url)

print(df.head())
```

### Important

* The sheet must be **shared publicly** or set to “Anyone with the link → Viewer”
* No login required for public CSV export

---

## **72️⃣ What is meant by the term "Regression"?**

### ✔ Regression (Definition)

Regression is a **statistical and machine learning method** used to:

* Predict **continuous numeric values**
* Understand the **relationship between variables**
* Identify how one variable changes with respect to another

### ✔ Examples:

* Predicting house prices
* Predicting salary
* Predicting temperature
* Predicting stock values (approx.)

### ✔ Common regression types:

* Linear Regression
* Multiple Regression
* Logistic Regression (classification)
* Polynomial Regression

### Interview Summary

Regression helps find a **best-fit line** or **mathematical model** that describes how variables influence each other.

---

Below is the **next batch**, continuing numbering from **73**, with clear, concise, face-to-face-interview-friendly answers in **GitHub-style formatting**.

---



## **73️⃣ Define `PYTHONPATH`.**

`PYTHONPATH` is an **environment variable** in Python that tells the interpreter **where to look for modules and packages** when you import them.

### Example use:

If you add a folder path to `PYTHONPATH`, Python will also search that folder while importing modules.

```bash
export PYTHONPATH="/my/custom/path"
```

### Interview Note

It works similarly to Java's CLASSPATH and helps in organizing or loading custom modules.

---

## **74️⃣ What is "Scope" in Python?**

Scope refers to **the region of a program where a variable is accessible**.

Python uses the **LEGB rule**:

* **L** → Local scope
* **E** → Enclosing scope
* **G** → Global scope
* **B** → Built-in scope

### Example:

```python
x = 10  # global

def func():
    x = 5  # local
```

---

## **75️⃣ What is PEP 8 and why is it important?**

**PEP 8** is Python’s **official style guide**, created to ensure:

* Consistent coding style
* Readability
* Maintainability
* Better collaboration

### It defines:

* Naming conventions
* Indentation rules
* Line length
* Spacing
* Best practices

Following PEP 8 makes code clean and professional.

---

## **76️⃣ What is `pass` in Python?**

`pass` is a **placeholder statement** that does nothing.
Used when you want to define a block of code syntactically but don’t want to implement logic yet.

### Example:

```python
def future_function():
    pass
```

Useful in empty functions, classes, loops, or conditional blocks during development.

---

## **77️⃣ What is the difference between Python arrays and lists? Why is `finalize` used?**

### ✔ Python Arrays

* Provided by the `array` module
* Store **only one type** of data (all ints, or all floats)
* More memory-efficient

### ✔ Lists

* Can store **different data types**
* More flexible, widely used

### ✔ `finalize`

`finalize` is used in **finalizers created with `weakref.finalize`**
It allows you to run cleanup code **after an object is destroyed** (alternative to `__del__`).

Example:

```python
import weakref
weakref.finalize(obj, cleanup_function)
```

Used to avoid memory leaks.

---

## **78️⃣ Differentiate between `new` and `override` modifiers.**

This question is more **OOP-concept related**, commonly asked in general programming:

### ✔ `new`

* Used in some languages (like C#/Java) to hide a parent method
* Creates **new implementation** unrelated to inheritance chain

### ✔ `override`

* Replace or modify the **parent class method**
* Maintains inheritance structure

### In Python:

* There is **no `new` modifier**
* Method overriding is done simply by redefining the method in the child class.

---

## **79️⃣ How is an empty class created in Python?**

Two ways:

### ✔ Using `pass`

```python
class Empty:
    pass
```

### ✔ Using `__init__`

```python
class Empty:
    def __init__(self):
        return
```

---

## **80️⃣ Is it possible to call the parent class without creating its instance?**

✔ Yes.

You can call parent methods using either:

### **1. `super()`**

```python
super().parent_method()
```

### **2. Class name directly**

```python
Parent.parent_method(self)
```

No need to create a parent object.

---

## **81️⃣ Are access specifiers used in Python?**

Python does **not** have strict access specifiers (like private, protected, public), but it follows conventions:

| Specifier | Syntax       | Meaning                                        |
| --------- | ------------ | ---------------------------------------------- |
| Public    | `variable`   | Accessible everywhere                          |
| Protected | `_variable`  | Internal use, not enforced                     |
| Private   | `__variable` | Name mangling applied → `_ClassName__variable` |

Python relies on **developer discipline**, not enforcement.

---

## **82️⃣ How do you access parent members in a child class?**

Two main ways:

### ✔ Using `super()`

```python
class Parent:
    def show(self):
        print("Parent")

class Child(Parent):
    def display(self):
        super().show()
```

### ✔ Using class name

```python
Parent.show(self)
```

Both work for methods and attributes.

---
Below is the **next batch of questions**, continuing numbering from **83**, with **clean Python programs**, written in a **simple, interview-friendly style**.

---



---

## **83️⃣ Write a program to convert date from `yyyy-mm-dd` format to `dd-mm-yyyy` format.**

```python
date = "2025-11-30"
yyyy, mm, dd = date.split("-")
new_format = f"{dd}-{mm}-{yyyy}"
print(new_format)
```

**Output:**
`30-11-2025`

---

## **84️⃣ Write a program to match a string that has the letter ‘a’ followed by 4 to 8 'b’s.**

Using regex:

```python
import re

pattern = r"ab{4,8}$"
string = "abbbbb"

if re.match(pattern, string):
    print("Match found")
else:
    print("No match")
```

Matches:

* `abbbbb`
* `abbbbbbbb`
* Any "a" followed by 4–8 "b"s.

---

## **85️⃣ Write a program to solve the given equation assuming a, b, c, m, n, o are constants.**

Since the equation is not specified, here is a generic template often asked in interviews:

Equation example:
**ax² + bx + c = 0**

```python
import math

def solve_quadratic(a, b, c):
    d = b*b - 4*a*c
    root1 = (-b + math.sqrt(d)) / (2*a)
    root2 = (-b - math.sqrt(d)) / (2*a)
    return root1, root2

print(solve_quadratic(1, -3, 2))
```

If you share the exact equation, I can give the exact code.

---

## **86️⃣ Write a program to add two integers >0 without using the plus (+) operator.**

Using bitwise operations:

```python
def add(x, y):
    while y != 0:
        carry = x & y
        x = x ^ y
        y = carry << 1
    return x

print(add(10, 20))
```

---

## **87️⃣ Write a program to find all pairs in array `A` whose sum equals a target value `N`.**

```python
def find_pairs(A, N):
    seen = set()
    pairs = []

    for num in A:
        diff = N - num
        if diff in seen:
            pairs.append((diff, num))
        seen.add(num)

    return pairs

print(find_pairs([2, 4, 3, 5, 7, 8], 9))
```

---

## **88️⃣ Write a program to count the number of every character in a given text file.**

```python
from collections import Counter

with open("data.txt", "r") as f:
    text = f.read()

freq = Counter(text)
print(freq)
```

---

## **89️⃣ Write a program that takes a sequence of numbers and checks if all numbers are unique.**

```python
def are_unique(numbers):
    return len(numbers) == len(set(numbers))

print(are_unique([1, 2, 3, 4]))     # True
print(are_unique([1, 2, 2, 3]))     # False
```

---

## **90️⃣ Write a Python function that accepts a variable number of arguments.**

```python
def variable_args(*args):
    for item in args:
        print(item)

variable_args(10, 20, 30)
```

---

## **91️⃣ How will you access a publicly shared Google Sheet in CSV format?**

Use its CSV export URL:

```
https://docs.google.com/spreadsheets/d/FILE_ID/export?format=csv
```

Python code:

```python
import pandas as pd

csv_url = "https://docs.google.com/spreadsheets/d/FILE_ID/export?format=csv"
df = pd.read_csv(csv_url)
print(df.head())
```

---

## **92️⃣ Write a program to combine two dictionaries and add values of the same keys.**

```python
dict1 = {"a": 1, "b": 2, "c": 3}
dict2 = {"a": 3, "b": 4, "d": 5}

result = {}

for key in dict1.keys() | dict2.keys():
    result[key] = dict1.get(key, 0) + dict2.get(key, 0)

print(result)
```

**Output:**
`{'a': 4, 'b': 6, 'c': 3, 'd': 5}`

---

---

