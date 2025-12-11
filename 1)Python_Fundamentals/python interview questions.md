
---

# ✅ **0. What is OOP in Python?**

“OOP is a programming technique that solves real-world problems by organizing code using classes and objects.”



Advantages of OOP
Provides a clear structure to programs
Makes code easier to maintain, reuse, and debug
Helps keep your code DRY (Don't Repeat Yourself)
Allows you to build reusable applications with less code
Tip: The DRY principle means you should avoid writing the same code more than once. Move repeated code into functions or classes and reuse it.

---
Class	| Objects
Fruit	| Apple, Banana, Mango
Car	    | Volvo, Audi, Toyota

---

# ⭐ **1. Class**

**Definition (interview):**
A **class** is a blueprint or template that defines the structure and behavior (data and methods) that its objects will have.

---

## 🔹 **Creating a Class**

Use the `class` keyword:

```python
class MyClass:
    x = 5   # class property
```

---

## 🔹 **The `pass` Statement**

A class cannot be empty. If you want an empty class, use `pass` to avoid errors:

```python
class Person:
    pass
```

---

# ⭐ **2. Object / Instance**

**Definition (interview):**
An **object** (or instance) is an actual thing created from a class blueprint.
It automatically gets access to all properties and methods inside the class.

---

## 🔹 **Creating an Object**

```python
p1 = MyClass()
print(p1.x)     # Output: 5
```

---

# ⭐ **3. Multiple Objects**

You can create multiple objects from the same class:

```python
p1 = MyClass()
p2 = MyClass()
p3 = MyClass()

print(p1.x)
print(p2.x)
print(p3.x)
```

📌 **Note:**
Each object is independent and gets its **own copy** of class/instance properties.

---

# ⭐ **4. Deleting an Object**

Use `del` to delete an object:

```python
del p1
```

After deletion, you can no longer use `p1`.

---

# ⭐ **5. Example with Class + Object (Simple)**

```python
class Student:
    pass

s1 = Student()   # creating object
```


---

# ✅ **3. Attributes (Data of the Object)**

Attributes are the variables inside a class that store data for objects.

They are of two types:

* **Instance Variables**
* **Class Variables**

---

# 🔥 **3.1 Instance Variable (Object Variable)**

### ✔ Definition

An instance variable is a variable that is **unique for every object**.

### ✔ Example

```python
class Student:
    def __init__(self, name, roll):
        self.name = name       # instance variable
        self.roll = roll       # instance variable

s1 = Student("Rahul", 1)
s2 = Student("Priya", 2)

print(s1.name)
print(s2.name)
```

### ✔ Output:

```
Rahul
Priya
```

### ✔ Key Point

Each object gets its **own copy** of instance variables.

---

# 🔥 **3.2 Accessing Instance Properties**

You can access an object's properties using **dot notation**.

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

car1 = Car("Toyota", "Corolla")

print(car1.brand)
print(car1.model)
```

### ✔ Output:

```
Toyota
Corolla
```

---

# 🔥 **3.3 Modify Instance Properties**

```python
p1 = Person("Tobias", 25)
print(p1.age)

p1.age = 26
print(p1.age)
```

### ✔ Output:

```
25
26
```

---

# 🔥 **3.4 Delete Instance Properties**

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

p1 = Person("Linus", 30)

del p1.age

print(p1.name)
# print(p1.age) → ERROR
```

### ✔ Output:

```
Linus
# print(p1.age) would cause:
AttributeError: 'Person' object has no attribute 'age'
```

---

# 🔥 **3.5 Adding New Properties to an Object**

```python
class Person:
    def __init__(self, name):
        self.name = name

p1 = Person("Tobias")

p1.age = 25
p1.city = "Oslo"

print(p1.name)
print(p1.age)
print(p1.city)
```

### ✔ Output:

```
Tobias
25
Oslo
```

⚠ **Note:** These new properties belong **ONLY** to `p1`, not to all objects.

---

# 🔥 **3.6 Class Variable (Static Variable)**

### ✔ Definition

A **class variable** is shared by **all objects** of the class.

### ✔ Example

```python
class Student:
    school = "DPS"      # class variable

    def __init__(self, name, roll):
        self.name = name
        self.roll = roll

s1 = Student("Rahul", 1)
s2 = Student("Priya", 2)

print(s1.school)
print(s2.school)
```

### ✔ Output:

```
DPS
DPS
```

### ✔ Key Point

Class variables belong to the **class itself**, not to objects.

---

# 🔥 **3.7 Class Properties vs Instance Properties**

```python
class Person:
    species = "Human"   # class property

    def __init__(self, name):
        self.name = name  # instance property

p1 = Person("Emil")
p2 = Person("Tobias")

print(p1.name)
print(p2.name)
print(p1.species)
print(p2.species)
```

### ✔ Output:

```
Emil
Tobias
Human
Human
```

---

# 🔥 **3.8 Modifying Class Properties**

Changes reflect in **all objects**.

```python
class Person:
    lastname = ""

    def __init__(self, name):
        self.name = name

p1 = Person("Linus")
p2 = Person("Emil")

Person.lastname = "Refsnes"

print(p1.lastname)
print(p2.lastname)
```

### ✔ Output:

```
Refsnes
Refsnes
```

---

# 🔥 **3.9 Difference Table: Instance Variable vs Class Variable**

| Instance Variable             | Class Variable                |
| ----------------------------- | ----------------------------- |
| Belongs to **object**         | Belongs to **class**          |
| Different for each object     | Same for all objects          |
| Created using `self.variable` | Created directly inside class |

---



# ✅ **4. Methods**

### ✔ Definition

A **method** is a function defined inside a class — the action an object can perform.

---

## ✔ Example

```python
class Student:
    def __init__(self, name):
        self.name = name

    def greet(self):
        print("Hello, I am", self.name)

s1 = Student("Amit")
s1.greet()
```

### **Output:**

```
Hello, I am Amit
```

---

# 🔥 **4.1 Methods with Parameters**

```python
class Calculator:
  def add(self, a, b):
    return a + b

  def multiply(self, a, b):
    return a * b

calc = Calculator()
print(calc.add(5, 3))
print(calc.multiply(4, 7))
```

### **Output:**

```
8
28
```

---

# 🔥 **4.2 Methods Accessing Properties**

```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def get_info(self):
    return f"{self.name} is {self.age} years old"

p1 = Person("Tobias", 28)
print(p1.get_info())
```

### **Output:**

```
Tobias is 28 years old
```

---

# 🔥 **4.3 Methods Modifying Properties**

```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def celebrate_birthday(self):
    self.age += 1
    print(f"Happy birthday! You are now {self.age}")

p1 = Person("Linus", 25)
p1.celebrate_birthday()
p1.celebrate_birthday()
```

### **Output:**

```
Happy birthday! You are now 26
Happy birthday! You are now 27
```

---

# 🔥 **4.4 `__str__()` Method**
"__str__() is a special method that returns a user-friendly string representation of an object. It is used by print() and str() to display meaningful information instead of the default memory address."
The __str__() method is a special method that controls what is returned when the object is printed:

## ❌ Without `__str__()`

```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

p1 = Person("Emil", 36)
print(p1)
```

### **Output (ugly internal object representation):**

```
<__main__.Person object at 0x000001A5C8E4BDF0>
```

---

## ✔ With `__str__()`

```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

  def __str__(self):
    return f"{self.name} ({self.age})"

p1 = Person("Tobias", 36)
print(p1)
```

### **Output:**

```
Tobias (36)
```

---

# 🔥 **4.5 Multiple Methods in a Class**

```python
class Playlist:
  def __init__(self, name):
    self.name = name
    self.songs = []

  def add_song(self, song):
    self.songs.append(song)

  def remove_song(self, song):
    if song in self.songs:
      self.songs.remove(song)

  def show_songs(self):
    for song in self.songs:
      print(song)

my_playlist = Playlist("Favorites")
my_playlist.add_song("Bohemian Rhapsody")
my_playlist.add_song("Stairway to Heaven")
my_playlist.show_songs()
```

### **Output:**

```
Bohemian Rhapsody
Stairway to Heaven
```

---

# 🔥 **4.6 Delete Methods**

```python
del Person.greet
```

After deleting:

```python
p1 = Person("Emil")
p1.greet()
```

### **Output:**

```
AttributeError: 'Person' object has no attribute 'greet'
```

---

### ✔ Attribute vs Method

* Attribute → data of the object
* Method → behavior of the object

---


---

# ✅ **5. `__init__` (Constructor)**

**Definition (interview):**
`__init__` is a special method called a **constructor**. It runs automatically when an object is created and initializes its attributes/ object variables.

---

### ✔ Simple Meaning

Setup code that runs once during object creation.

---

### ✔ Example

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

s1 = Student("Amit", 20)
```

---

# ⭐ **Why Use `__init__()`?**

Without the `__init__()` method, you would need to set properties manually for each object:

---

### ❌ Example

Create a class without `__init__()`:

```python
class Person:
  pass

p1 = Person()
p1.name = "Tobias"
p1.age = 25

print(p1.name)
print(p1.age)
```

---

Using `__init__()` makes it easier to create objects with initial values:

---

### ✔ Example

With `__init__()`, you can set initial values when creating the object:

```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age

p1 = Person("Linus", 28)

print(p1.name)
print(p1.age)
```

---



---

# ✅ **6. `self` Keyword**

`self` represents the **current instance(object) of the class**.
Whenever we create an object, `self` helps Python understand **which object’s variables or methods** we want to access.

### Why is it used?

* To access **instance variables**
* To access **instance methods**
* To differentiate **class variables vs. object variables**

### ✔ What is `self`?

`self` means **“this object”** — the current object calling the method.

Python automatically passes the object as the first argument to methods, and by convention we name it `self`.

---

### ✔ Why do we need `self`?

Because inside a class we must tell Python:

> “Which object's data am I referring to?”

Without `self`, Python doesn’t know which object's attribute to access.

---

### ✔ Example

```python
class Person:
    def __init__(self, name, age):
        self.name = name   # set name for THIS object
        self.age = age     # set age for THIS object
```


When you write:

```python
p1 = Person("Rahul", 20)
```

Python does this internally:

```
__init__(p1, "Rahul", 20)
```

So inside the class,

* `self` = `p1`
* `self.name` → p1.name
* `self.age` → p1.age

When you create another object:

```python
p2 = Person("Priya", 22)
```

Python calls:

```
__init__(p2, "Priya", 22)
```

Now `self = p2`.


When creating objects:

```python
p1 = Person("Rahul", 20)
p2 = Person("Priya", 22)
```

* In first call → `self = p1`
* In second call → `self = p2`

So each object stores **its own** name and age.

---

### ✔ Important Note

`self` is **NOT a keyword** — you can rename it, but everyone uses `self`.

---


---

# ✅ **7. Types of Methods in Python**

Methods define what actions an object or class can perform.

Python has **three types of methods**:

1. **Instance Method**
2. **Class Method**
3. **Static Method**

---

## 🔵 **7.1 Instance Method**

### ✔ Definition

An **instance method** is a method that takes `self` as the first parameter and works on **instance variables**.

### ✔ Example

```python
class Demo:
    def instance_method(self):
        print("Instance method")
```

### ✔ Key Point

Instance methods can access:

* instance variables
* class variables

Because they have access to `self`.

---

## 🟣 **7.2 Class Method**

### ✔ Definition

A **class method** takes `cls` as the first argument and works with **class-level data**.
It is created using **`@classmethod`**.

### ✔ Example

```python
class Demo:
    count = 0

    @classmethod
    def show_count(cls):
        print(cls.count)
```

### ✔ Key Point

Class methods can **access and modify class variables**, not instance variables.

---

## 🟢 **7.3 Static Method**

### ✔ Definition

A **static method** does NOT take `self` or `cls`.
It behaves like a normal function inside a class.

### ✔ Example

```python
class Demo:
    @staticmethod
    def add(x, y):
        return x + y
```

### ✔ Key Point

Used when the method logic does **not depend** on instance or class data.

---

# 🔥 **19️⃣ Difference Between Class Method & Static Method (Interview Style)**

## 🔵 **Class Method — 3 Points**

1. Takes **`cls`** as the first argument.
2. Can **access or modify class variables**.
3. Defined using the **`@classmethod` decorator**.

---

## 🟢 **Static Method — 3 Points**

1. Takes **neither `self` nor `cls`**.
2. Behaves like a normal helper function inside a class.
3. Defined using the **`@staticmethod` decorator**.

---


---

# ✅ **8. Encapsulation**

### ✔ **Definition (interview)**

Encapsulation means **bundling data + methods** inside a class and restricting direct access to internal data.

Python supports encapsulation using three levels:

| Type          | Prefix  | Meaning                               |
| ------------- | ------- | ------------------------------------- |
| **Public**    | `var`   | Accessible everywhere                 |
| **Protected** | `_var`  | Convention: “Don’t access directly”   |
| **Private**   | `__var` | Name-mangled, not directly accessible |

Encapsulation helps with:

✔ Data protection
✔ Validation before updating values
✔ Hiding internal implementation
✔ Cleaner & safer class design

---

# 🔥 **8.1 Private Properties (`__var`)**

Private attributes are created using **double underscore `__`**.
They **cannot be accessed directly** from outside the class.

### ✔ Example

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.__age = age   # private property

p1 = Person("Emil", 25)
print(p1.name)
print(p1.__age)   # ❌ ERROR — cannot access private attribute
```

⚠ **Important:** Private attributes are NOT truly hidden — Python applies **name-mangling**.

---

# 🔥 **8.2 Getter: Accessing Private Properties**

We create a **getter method** to safely read private values.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.__age = age

    def get_age(self):
        return self.__age
```

Usage:

```python
p = Person("Tobias", 25)
print(p.get_age())
```

---

# 🔥 **8.3 Setter: Modifying Private Properties (with Validation)**

Setter ensures **validated and controlled** updates to private data.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.__age = age

    def get_age(self):
        return self.__age

    def set_age(self, age):
        if age > 0:
            self.__age = age
        else:
            print("Age must be positive")
```

Usage:

```python
p = Person("Tobias", 25)
p.set_age(26)
print(p.get_age())
```

---

# 🔥 **8.4 Why Encapsulation? (Very important for interview)**

Encapsulation provides:

### ✔ **Data Protection**

Prevents accidental or unauthorized modification.

### ✔ **Validation**

Setter methods can check values before assigning.

### ✔ **Flexibility**

Internal implementation can change without affecting external code.

### ✔ **Control**

You decide *how* the data is accessed or modified.

### ✔ Example

```python
class Student:
    def __init__(self, name):
        self.name = name
        self.__grade = 0

    def set_grade(self, grade):
        if 0 <= grade <= 100:
            self.__grade = grade
        else:
            print("Grade must be between 0 and 100")

    def get_grade(self):
        return self.__grade

    def get_status(self):
        return "Passed" if self.__grade >= 60 else "Failed"
```

---

# 🔥 **8.5 Protected Properties (`_var`)**

A single underscore `_var` **does NOT enforce protection** — it’s just a **convention**:

> “This attribute is meant for internal use. Don’t touch it unless necessary.”

```python
class Person:
    def __init__(self, name, salary):
        self.name = name
        self._salary = salary   # protected property
```

Still accessible:

```python
p = Person("Linus", 50000)
print(p._salary)   # ⚠ Possible but not recommended
```

---

# 🔥 **8.6 Private Methods (`__method`)**

You can also hide methods the same way you hide variables.

```python
class Calculator:
    def __init__(self):
        self.result = 0

    def __validate(self, num):    # private method
        return isinstance(num, (int, float))

    def add(self, num):
        if self.__validate(num):
            self.result += num
        else:
            print("Invalid number")
```

Attempt to call private method directly:

```python
calc.__validate(5)   # ❌ ERROR
```

---

# 🔥 **8.7 Name Mangling (Very Important Concept)**

Python renames private attributes internally:

```
__age  →  _ClassName__age
```

### ✔ Example

```python
class Person:
    def __init__(self, name, age):
        self.__age = age

p = Person("Emil", 30)
print(p._Person__age)   # Works due to name-mangling (NOT recommended)
```

⚠ **Note:** Accessing private variables via name-mangling breaks encapsulation and must be avoided in real code.

---

# 🔥 **8.8 Pythonic Getters & Setters with `@property` (Advanced)**

This is the **recommended** modern Python style.
No need to call `get_age()` or `set_age()` manually.

```python
class Student:
    def __init__(self):
        self.__age = 18

    @property
    def age(self):       # getter
        return self.__age

    @age.setter
    def age(self, value):   # setter
        if value > 0:
            self.__age = value
        else:
            print("Invalid age")
```

Usage:

```python
s = Student()
print(s.age)   # getter
s.age = 25     # setter
```

✔ Cleaner
✔ More Pythonic
✔ Same encapsulation benefits

---

# 🎯 FINAL SUMMARY — Encapsulation in One Shot

* Use `__var` for **private** data
* Use `_var` for **protected** (soft restriction)
* Use **getter/setter** to access & modify private attributes
* Use `@property` for clean, Pythonic encapsulation
* Private members use **name-mangling** internally: `_Class__var`
* Encapsulation protects data and gives you full control

---



# ✅ **Python Inheritance

Inheritance allows us to define a class that **inherits all the methods and properties from another class**.

* **Parent class** → also called **base class**
* **Child class** → also called **derived class**, inherits from parent

---

# 🔵 **1. Create a Parent Class**

Any class can be a parent class.

### ✔ Example: Creating a `Person` class

```python
class Person:
  def __init__(self, fname, lname):
    self.firstname = fname
    self.lastname = lname

  def printname(self):
    print(self.firstname, self.lastname)
```

### ✔ Create an object and call method

```python
x = Person("John", "Doe")
x.printname()
```

---

# 🔵 **2. Create a Child Class**

To create a class that inherits from another class, pass the parent class as a parameter.

### ✔ Example: `Student` inherits from `Person`

```python
class Student(Person):
  pass
```

Now `Student` has all properties & methods of `Person`.

### ✔ Usage

```python
x = Student("Mike", "Olsen")
x.printname()
```

---

# 🔵 **3. Add `__init__()` in Child Class**

When you add your own `__init__()` in the child:

➡ The child **overrides** the parent’s `__init__()`
➡ Parent’s constructor is **not inherited automatically**

### ✔ Example: Child overriding constructor

```python
class Student(Person):
  def __init__(self, fname, lname):
    # add properties etc.
```

This removes the parent `__init__()`.

---

# 🔵 **4. Keeping Parent `__init__()`**

To keep the parent initialization, call it manually:

```python
class Student(Person):
  def __init__(self, fname, lname):
    Person.__init__(self, fname, lname)
```

Now child has both:

✔ Parent’s initialization
✔ Additional child logic

---

# 🔵 **5. Using `super()` (Recommended Method)**

`super()` automatically calls the parent class without naming it.

### ✔ Example:

```python
class Student(Person):
  def __init__(self, fname, lname):
    super().__init__(fname, lname)
```

Benefits of `super()`:

✔ Cleaner
✔ Works correctly with multiple inheritance
✔ Avoids hardcoding parent class name

---

# 🔵 **6. Add New Properties in Child Class**

### ✔ Example: Add `graduationyear`

```python
class Student(Person):
  def __init__(self, fname, lname):
    super().__init__(fname, lname)
    self.graduationyear = 2019
```

### Child with variable year:

```python
class Student(Person):
  def __init__(self, fname, lname, year):
    super().__init__(fname, lname)
    self.graduationyear = year

x = Student("Mike", "Olsen", 2019)
```

---

# 🔵 **7. Add New Methods in Child Class**

### ✔ Example: Add `welcome()` method

```python
class Student(Person):
  def __init__(self, fname, lname, year):
    super().__init__(fname, lname)
    self.graduationyear = year

  def welcome(self):
    print("Welcome", self.firstname, self.lastname, "to the class of", self.graduationyear)
```

---

# 🔵 **8. Method Overriding**

If a child class defines a method with the **same name** as a parent method:

➡ The parent method is **overridden (replaced)**
➡ The child’s implementation is used




## ⭐ **Types of Inheritance (Definitions)**

| Type             | Meaning                          |
| ---------------- | -------------------------------- |
| **Single**       | One parent → one child           |
| **Multiple**     | Child has *more than one* parent |
| **Multilevel**   | Parent → Child → GrandChild      |
| **Hierarchical** | One parent → multiple children   |
| **Hybrid**       | Combination of above             |

---

## ⭐ **Why is inheritance used?**

✔ Code reuse
✔ Reduces duplication
✔ Helps in overriding & polymorphism
✔ Clear relationship: *child is a type of parent*

---

---

# ⭐ **Multiple Inheritance (Important Concept)**

Python **fully supports** multiple inheritance.

### ✔ Definition

A child class can inherit from **more than one** parent class.

### ✔ Example (with comments)

```python
class Father:
    def skills(self):
        print("Father: Coding")

class Mother:
    def skills(self):
        print("Mother: Cooking")

class Child(Father, Mother):   # inherits from both
    pass

c = Child()
c.skills()     # which skills() is called?
```

### ✔ Output

```
Father: Coding
```

### ✔ Why father?

Python checks using **MRO order**:

```
Child → Father → Mother → Object
```

---

# ⭐ **Types of Inheritance with EXAMPLES + Comments**

---

# 1️⃣ **Single Inheritance**

```python
class Animal:
    def eat(self):
        print("Eating")

class Dog(Animal):       # Dog inherits Animal
    def bark(self):
        print("Barking")

d = Dog()
d.eat()   # parent method
d.bark()  # child method
```

---

# 2️⃣ **Multiple Inheritance**

```python
class A:
    def f1(self):
        print("A")

class B:
    def f2(self):
        print("B")

class C(A, B):     # inherits from A and B
    pass

c = C()
c.f1()
c.f2()
```

---

# 3️⃣ **Multilevel Inheritance**

```python
class A:
    def f1(self):
        print("A")

class B(A):       # B is child of A
    def f2(self):
        print("B")

class C(B):       # C is child of B
    def f3(self):
        print("C")

c = C()
c.f1()
c.f2()
c.f3()
```

---

# 4️⃣ **Hierarchical Inheritance**

```python
class Parent:
    def show(self):
        print("Parent")

class Child1(Parent):     # both inherit parent
    pass

class Child2(Parent):
    pass

Child1().show()
Child2().show()
```

---

# 5️⃣ **Hybrid Inheritance**

```python
class A:
    def f1(self):
        print("A")

class B(A):     # multilevel
    def f2(self):
        print("B")

class C(A):     # hierarchical
    def f3(self):
        print("C")

class D(B, C):   # multiple
    def f4(self):
        print("D")

d = D()
d.f1(); d.f2(); d.f3(); d.f4()
```

---

# ⭐ Quick Revision Table

| Type         | Structure       |
| ------------ | --------------- |
| Single       | A → B           |
| Multiple     | A → C ← B       |
| Multilevel   | A → B → C       |
| Hierarchical | A → B and A → C |
| Hybrid       | Mix of all      |

---

# ✅ **10. `super()` — Calling Parent Methods**

### **Definition (interview):**

`super()` is used to call **parent class methods** from a child class.

### ✔ Example with comments

```python
class Parent:
    def __init__(self):
        print("Parent init")

class Child(Parent):
    def __init__(self):
        super().__init__()     # calls Parent __init__
        print("Child init")

Child()
```

### ✔ Output

```
Parent init
Child init
```

---

# ⭐ extra — Why super() is important?

super():

✔ avoids confusion in multiple inheritance
✔ ensures proper MRO order
✔ prevents calling parent methods manually
✔ safer & cleaner than `Parent.method(self)`

---

# ✅ **11. MRO (Method Resolution Order)**

### **Definition (interview):**

MRO decides **the order in which Python searches parent classes** when calling a method in multiple inheritance.

Python follows **C3 Linearization Algorithm**.

### ✔ Check MRO of any class:

```python
print(ClassName.mro())
```

### ✔ Simple example

```
Child → Parent1 → Parent2 → Object
```

### ✔ Why important?

To know which parent’s method runs when multiple parents have the same method.

---

# ⭐ Extra concept (Important💡):

### **Attribute Lookup Flow**

When you access `obj.method()`, Python searches in this order:

```
1. Object’s class
2. Parent class (left to right)
3. Grandparents
4. ...
5. Object class
```

This is MRO in action.

---

# ✅ **12. Diamond Problem**

### **Definition (interview):**

Diamond problem occurs when two parent classes inherit from the same base class, and a child inherits from both parents.

### ✔ Visualization:

```
     A
    / \
   B   C
    \ /
     D
```

### ✔ Problem:

If **both B and C** have the same method, which one should D use?

### ✔ Python’s solution

Python uses **MRO** to ensure:

* the method runs **only once**
* order is predictable
* no repeated calls to A

---

# ⭐ Example (with comments)

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

class D(B, C):     # diamond shape
    pass

d = D()
d.show()   # which one?
```

### ✔ Output

```
B
```

### ✔ Why?

MRO for D is:

```
D → B → C → A → object
```

---


---

# ✅ **11. Polymorphism**

**Definition (interview):**
Polymorphism means **one name, many forms** – the same operation or method name behaves differently in different classes.

---

## **11.1 Method Overriding (Supported in Python)**

**Definition:**
A child class provides its **own version** of a method already defined in the parent.

**Example:**

```python
class Animal:
    def sound(self):
        print("Some sound")

class Dog(Animal):   # overriding
    def sound(self):
        print("Bark")
```

---

## **11.2 Method Overloading (Not real overloading)**

Python does NOT support true method overloading by signature.

We simulate it using:

* default arguments
* `*args`

---

## ✅ **11.3 Duck Typing (Python-style Polymorphism)** 🚀 *Missing earlier – now added*

**Definition:**
Python does not care about the *type* of an object.
It only cares whether the object has the required *method*.

> “If it walks like a duck and quacks like a duck — it’s a duck.”

**Example:**

```python
class Dog:
    def sound(self):
        print("Bark")

class Cat:
    def sound(self):
        print("Meow")

def make_sound(animal):
    animal.sound()   # works for both Dog and Cat

make_sound(Dog())
make_sound(Cat())
```

**Interview line:**
Duck typing allows polymorphism **without inheritance** in Python.

---

# 🔥 **11.4 Function Polymorphism (W3 Style Explanation)**

Polymorphism also appears in **built-in Python functions**.

The same function name → works differently on different data types.

### ✔ `len()` on **string**

For strings, `len()` returns the number of characters.

```python
x = "Hello World!"
print(len(x))       # 12
```

### ✔ `len()` on **tuple**

For tuples, `len()` returns the number of items.

```python
mytuple = ("apple", "banana", "cherry")
print(len(mytuple))     # 3
```

### ✔ `len()` on **dictionary**

For dictionaries, `len()` returns number of key–value pairs.

```python
thisdict = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

print(len(thisdict))     # 3
```

**Why is this polymorphism?**
Because the **same function name** behaves differently depending on the type of object.

---

# 🔥 **11.5 Class Polymorphism (W3 Style Explanation)**

Polymorphism is also used in **classes** when multiple classes have a method with the **same name**.

For example:
Car, Boat, and Plane all have a `move()` method, but each behaves differently.

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def move(self):
        print("Drive!")

class Boat:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def move(self):
        print("Sail!")

class Plane:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def move(self):
        print("Fly!")

car1 = Car("Ford", "Mustang")
boat1 = Boat("Ibiza", "Touring 20")
plane1 = Plane("Boeing", "747")

for x in (car1, boat1, plane1):
    x.move()
```

### ✔ Output

```
Drive!
Sail!
Fly!
```

**Why is this polymorphism?**
Because `x.move()` calls *different* methods depending on object type — same method name, multiple forms.

---

# 🔥 **11.6 Inheritance-Based Polymorphism (W3 Style Explanation)**

Polymorphism also works with **inheritance**.

A parent class defines a method → child classes can override it.

```python
class Vehicle:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model

    def move(self):
        print("Move!")

class Car(Vehicle):     # inherits and does NOT override move()
    pass

class Boat(Vehicle):    # overrides move()
    def move(self):
        print("Sail!")

class Plane(Vehicle):   # overrides move()
    def move(self):
        print("Fly!")

car1 = Car("Ford", "Mustang")
boat1 = Boat("Ibiza", "Touring 20")
plane1 = Plane("Boeing", "747")

for x in (car1, boat1, plane1):
    print(x.brand)
    print(x.model)
    x.move()
```

### ✔ Output

```
Ford
Mustang
Move!

Ibiza
Touring 20
Sail!

Boeing
747
Fly!
```

### ✔ Key Points

* Child classes inherit parent methods automatically.
* They can **override** the method for different behavior.
* This allows calling the same method (`move()`) on different objects with different outputs.

---

# 🔥 **11.7 Operator Polymorphism (Additional Important Concept)**

Same operator → different behavior depending on datatype.

```python
print(10 + 5)         # 15  (integer addition)
print("A" + "B")      # AB  (string concatenation)
print([1, 2] + [3])   # [1, 2, 3]  (list merging)
```
---

# ✅ **12. Abstraction**

**Definition (interview):**
Abstraction means **hiding internal implementation** and showing only essential details.

Python achieves abstraction using:

* Abstract classes
* Abstract methods (`@abstractmethod`)
* `abc` module

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

---

# ✅ **13. Composition (Has-a Relationship)**

**Definition (interview):**
Composition is when one class **contains another class** — forming a “has-a” relationship.

**Simple meaning:**
A car **has an** engine.

**Example:**

```python
class Engine:
    def start(self):
        print("Engine start")

class Car:
    def __init__(self):
        self.engine = Engine()   # composition

    def start(self):
        self.engine.start()
        print("Car started")
```

---

# 🔥 **13.1 Composition vs Inheritance (Missing earlier — now included)**

### **Inheritance (is-a relationship)**

Dog **is an** Animal
Car **is a** Vehicle

Used when:

* You want to extend or modify parent behavior
* You want a class to be a specialized version of another class

---

### **Composition (has-a relationship)**

Car **has an** Engine
User **has a** Profile

Used when:

* You want to build complex objects from simpler ones
* You want flexibility and loose coupling
* You want to avoid complexities of multiple inheritance

---

### **Interview one-liner:**

Use **inheritance** to model *what something is*.
Use **composition** to model *what something has*.

---

---

# ✅ **18. Inner Classes (Nested Classes)**

An **inner class** is a class defined **inside another class**.

They are used when a class is meant to be used **only inside** another class — helps in grouping related logic and improving code organization.

---

# 🔵 **18.1 Creating an Inner Class**

```python
class Outer:
    def __init__(self):
        self.name = "Outer Class"

    class Inner:
        def __init__(self):
            self.name = "Inner Class"

        def display(self):
            print("This is the inner class")
```

### ✔ Usage

```python
outer = Outer()
print(outer.name)

inner = Outer.Inner()
inner.display()
```

---

# 🔵 **18.2 Accessing Inner Class from Outside**

To access an inner class, you must:

1. Create an object of the outer class
2. Then create an object of the inner class

```python
class Outer:
    def __init__(self):
        self.name = "Outer"

    class Inner:
        def __init__(self):
            self.name = "Inner"

        def display(self):
            print("Hello from inner class")

outer = Outer()
inner = outer.Inner()
inner.display()
```

---

# 🔵 **18.3 Inner Class Accessing Outer Class Data**

Inner classes **do NOT automatically** get access to outer class variables.

You must pass the outer class instance manually:

```python
class Outer:
    def __init__(self):
        self.name = "Emil"

    class Inner:
        def __init__(self, outer):
            self.outer = outer

        def display(self):
            print(f"Outer class name: {self.outer.name}")

outer = Outer()
inner = outer.Inner(outer)
inner.display()
```

---

# 🔵 **18.4 Practical Example — Engine Inside Car**

This is where inner classes are really useful.

```python
class Car:
    def __init__(self, brand, model):
        self.brand = brand
        self.model = model
        self.engine = self.Engine()

    class Engine:
        def __init__(self):
            self.status = "Off"

        def start(self):
            self.status = "Running"
            print("Engine started")

        def stop(self):
            self.status = "Off"
            print("Engine stopped")

    def drive(self):
        if self.engine.status == "Running":
            print(f"Driving the {self.brand} {self.model}")
        else:
            print("Start the engine first!")
```

### ✔ Usage

```python
car = Car("Toyota", "Corolla")
car.drive()              # Start the engine first!
car.engine.start()       # Engine started
car.drive()              # Driving the Toyota Corolla
```

---

# 🔵 **18.5 Multiple Inner Classes**

A class can have multiple nested helper classes.

```python
class Computer:
    def __init__(self):
        self.cpu = self.CPU()
        self.ram = self.RAM()

    class CPU:
        def process(self):
            print("Processing data...")

    class RAM:
        def store(self):
            print("Storing data...")
```

### ✔ Usage

```python
computer = Computer()
computer.cpu.process()
computer.ram.store()
```



---



# ✅ **14. Dunder / Magic Methods**

**Definition (interview):**
Magic (dunder) methods start and end with `__` and let you define how objects behave with operators and built-in functions.

### Common magic methods:

| Method     | Purpose               |
| ---------- | --------------------- |
| `__init__` | Constructor           |
| `__str__`  | User-friendly string  |
| `__repr__` | Developer string      |
| `__len__`  | Length of object      |
| `__add__`  | Overload `+` operator |
| `__eq__`   | Compare objects       |

---

## **Example 1: `__len__`**

```python
class Book:
    def __init__(self, pages):
        self.pages = pages

    def __len__(self):
        return self.pages

b = Book(300)
print(len(b))  # 300
```

---

## **Example 2: Operator Overloading with `__add__` (Missing — added)**

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):   # object1 + object2
        return Point(self.x + other.x, self.y + other.y)

p1 = Point(2, 3)
p2 = Point(4, 5)
p3 = p1 + p2   # calls __add__
print(p3.x, p3.y)  # 6 8
```

---

## **Example 3: Comparing objects using `__eq__` (Added)**

```python
class Student:
    def __init__(self, marks):
        self.marks = marks

    def __eq__(self, other):
        return self.marks == other.marks

s1 = Student(90)
s2 = Student(90)

print(s1 == s2)  # True
```

Here you go — your **clean, simple, interview-ready** explanation of
**`__str__` vs `__repr__`**, exactly as you asked:

---

# ✅ **What is the difference between `__str__` and `__repr__`?**

## **`__str__`**

* **Purpose:** User-friendly / readable string representation
* **Used for:** Showing information to end users
* **Called by:** `print()` or `str(object)`
* **Goal:** Make the output **easy to read and understand**

---

## **`__repr__`**

* **Purpose:** Developer-friendly / unambiguous representation
* **Used for:** Debugging, logging, developers
* **Called by:** `repr(object)` or automatically in the interpreter
* **Goal:** Output should be **valid Python code** or enough to recreate the object

---

# ⭐ **One-Line Difference**

* **`__str__` → Human-readable (for users)**
* **`__repr__` → Machine-readable / unambiguous (for developers)**

---

# ⭐ **Interview Summary Answer**

> **“`__str__` provides a clean, readable output for users, whereas `__repr__` provides a detailed, unambiguous output for developers. If `__str__` is not defined, Python automatically falls back to `__repr__`.”**

---


# 🐍 Python Interview Q&A (Beginner-Friendly + F2F Ready)

---

## 1️⃣ **What is the use of the `self` keyword in Python?**

`self` represents the **current instance(object) of the class**.
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
---

# ✅ **Shallow Copy — 3 Points**

1. **Only outer object is copied; inner objects are NOT copied.**
2. **Inner elements are shared** between original and copied object.
3. Changing inner data in one object **also changes** it in the other.

---

# ✅ **Deep Copy — 3 Points**

1. **Outer and all inner objects are copied separately (full copy).**
2. Original and copied object are **completely independent**.
3. Changing anything (inner or outer) in one **does NOT affect** the other.

---
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
---

# 🔵 **Class Method — 3 Points**

1. Class method takes **`cls` as the first argument**, which represents the **class**, not the object.
2. It can **access and modify class variables** but cannot access instance variables.
3. It is created using the **`@classmethod`** decorator.

---

# 🟢 **Static Method — 3 Points**

1. Static method **does not take `self` or `cls`** — it has no connection to object or class.
2. It is just a **normal function inside a class**, used for utility/helper tasks.
3. It is created using the **`@staticmethod`** decorator.

---
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
---

# ✅ **Interview-Style Answer: map() vs filter()**

### 🔸 **map()**

* **Hinglish:** *Sabko badal do* — map() har element par function apply karke **poori list ko transform** kar deta hai.
* **English:** *Transforms every item* — map() applies a function to **each element** in an iterable and returns the transformed results.

### 🔸 **filter()**

* **Hinglish:** *Jo pasand ho unko rakh lo* — filter() sirf **un items ko select karta hai** jo condition pass karte hain.
* **English:** *Keeps only items that meet a condition* — filter() returns only those elements for which the function evaluates to True.

---

## **22️⃣ How can you handle exceptions in Python?**

# ✅ **Interview-Style Answer**

In Python, we handle exceptions using the **try–except** block.
The code that may cause an error goes inside **try**, and the error-handling code goes inside **except**.

### ⭐ Structured Answer:

* **try block** → code that might raise an exception
* **except block** → handles the exception if it occurs
* **else block** → runs only if no exception occurs
* **finally block** → always runs, used for cleanup (like closing files)

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

---

## **28️⃣ How are arguments passed in Python — by value or by reference?**
---

# ✅ **Interview-Style Answer**

Python uses **“pass-by-object-reference”** or **“pass-by-assignment.”**
This means:

* If you pass a **mutable object** (list, dict, set), changes inside the function **affect the original object**.
* If you pass an **immutable object** (int, float, string, tuple), changes inside the function **do NOT affect** the original object because a new object is created.

### ⭐ Final Interview Line:

**“Python doesn’t use pure pass-by-value or pass-by-reference; it passes the reference to the object, but whether it behaves like value or reference depends on the mutability of the object.”**

---

## **29️⃣ How do you convert a list into a set?**

Use `set()` constructor.

### Example:

```python
my_list = [1,2,3,1]
my_set = set(my_list)
```

---


### ✔ Pickling

Pickling is the process of **converting a Python object into a byte stream** so it can be:

* stored in a file
* sent over a network
* saved for later use

### ✔ Unpickling

Unpickling is the reverse — **converting byte stream back into a Python object**.


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


Python does **not** have strict access specifiers (like private, protected, public), but it follows conventions:

| Specifier | Syntax       | Meaning                                        |
| --------- | ------------ | ---------------------------------------------- |
| Public    | `variable`   | Accessible everywhere                          |
| Protected | `_variable`  | Internal use, not enforced                     |
| Private   | `__variable` | Name mangling applied → `_ClassName__variable` |

Python relies on **developer discipline**, not enforcement.


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


---

## **66️⃣ Difference between `del` and `remove()` in Python lists**

| Operation     | What it does                          |
| ------------- | ------------------------------------- |
| `remove(x)`   | Removes first occurrence of value `x` |
| `del list[i]` | Deletes item at index `i`             |
| `del list`    | Deletes entire list                   |

---


---

## **68️⃣ How does Flask handle database requests?**

Flask itself is lightweight, but database operations are handled using:

* **ORMs like SQLAlchemy**
* **DB connectors** (psycopg2, pymysql)
* **Flask extensions** (Flask-SQLAlchemy)

### Flask request → route → DB operation → response

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
**programs**
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

