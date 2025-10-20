# 🐍 Python Built-in Functions and Methods - Comprehensive Guide

A complete reference guide for Python's built-in functions and methods for data structures and string operations.

---

## 📋 Table of Contents

1. [String Methods](#-string-methods)
2. [List Methods](#-list-methods)
3. [Dictionary Methods](#-dictionary-methods)
4. [Set Methods](#-set-methods)
5. [Tuple Methods](#-tuple-methods)
6. [Built-in Functions](#-built-in-functions)
7. [Quick Reference](#-quick-reference)

---

## 🔤 String Methods

### **Validation Methods**

#### `str.isalnum()`
**Syntax:** `string.isalnum()`  
**Description:** Returns `True` if all characters are alphanumeric (letters and numbers, no spaces or special characters)  
**Example:**
```python
"Hello123".isalnum()  # True
"Hello 123".isalnum()  # False (contains space)
```
**When to Use:** To validate usernames, identifiers, or check if input contains only letters and numbers  
**Return Type:** `bool`

---

#### `str.isalpha()`
**Syntax:** `string.isalpha()`  
**Description:** Returns `True` if all characters are alphabetic  
**Example:**
```python
"Hello".isalpha()  # True
"Hello123".isalpha()  # False
```
**When to Use:** To validate names or check if string contains only letters  
**Return Type:** `bool`

---

#### `str.isdigit()`
**Syntax:** `string.isdigit()`  
**Description:** Returns `True` if all characters are digits  
**Example:**
```python
"12345".isdigit()  # True
"123.45".isdigit()  # False (contains decimal point)
```
**When to Use:** To validate numeric strings before converting to int  
**Return Type:** `bool`

---

#### `str.islower()`
**Syntax:** `string.islower()`  
**Description:** Returns `True` if all cased characters are lowercase  
**Example:**
```python
"hello".islower()  # True
"Hello".islower()  # False
```
**When to Use:** To check text case formatting in validation  
**Return Type:** `bool`

---

#### `str.isupper()`
**Syntax:** `string.isupper()`  
**Description:** Returns `True` if all cased characters are uppercase  
**Example:**
```python
"HELLO".isupper()  # True
"Hello".isupper()  # False
```
**When to Use:** To verify uppercase formatting requirements  
**Return Type:** `bool`

---

#### `str.isspace()`
**Syntax:** `string.isspace()`  
**Description:** Returns `True` if string contains only whitespace characters  
**Example:**
```python
"   ".isspace()  # True
" a ".isspace()  # False
```
**When to Use:** To detect empty or whitespace-only strings in data cleaning  
**Return Type:** `bool`

---

### **Transformation Methods**

#### `str.replace()`
**Syntax:** `string.replace(old, new, count=-1)`  
**Description:** Replaces occurrences of a substring with another  
**Example:**
```python
"Hello World".replace("World", "Python")  # "Hello Python"
"a-b-c".replace("-", "_", 1)  # "a_b-c" (only first occurrence)
```
**When to Use:** To substitute text, clean data, or modify strings  
**Return Type:** `str`

---

#### `str.split()`
**Syntax:** `string.split(separator=None, maxsplit=-1)`  
**Description:** Splits string into list using separator  
**Example:**
```python
"a,b,c".split(",")  # ["a", "b", "c"]
"one two three".split()  # ["one", "two", "three"] (splits on whitespace)
"a-b-c".split("-", 1)  # ["a", "b-c"] (max 1 split)
```
**When to Use:** To parse CSV data, tokenize text, or break strings into parts  
**Return Type:** `list`

---

#### `str.join()`
**Syntax:** `separator.join(iterable)`  
**Description:** Joins elements of an iterable with separator  
**Example:**
```python
"-".join(["a", "b", "c"])  # "a-b-c"
" ".join(["Hello", "World"])  # "Hello World"
",".join(["1", "2", "3"])  # "1,2,3"
```
**When to Use:** To combine list elements into a single string  
**Return Type:** `str`

---

#### `str.strip()`
**Syntax:** `string.strip(chars=None)`  
**Description:** Removes leading and trailing characters (whitespace by default)  
**Example:**
```python
"  hello  ".strip()  # "hello"
"***hello***".strip("*")  # "hello"
```
**When to Use:** To clean user input or remove whitespace/unwanted characters  
**Return Type:** `str`

---

#### `str.lstrip()`
**Syntax:** `string.lstrip(chars=None)`  
**Description:** Removes leading characters from the left  
**Example:**
```python
"  hello".lstrip()  # "hello"
"000123".lstrip("0")  # "123"
```
**When to Use:** To remove left padding or prefixes  
**Return Type:** `str`

---

#### `str.rstrip()`
**Syntax:** `string.rstrip(chars=None)`  
**Description:** Removes trailing characters from the right  
**Example:**
```python
"hello  ".rstrip()  # "hello"
"file.txt...".rstrip(".")  # "file.txt"
```
**When to Use:** To remove right padding or suffixes  
**Return Type:** `str`

---

### **Case Conversion Methods**

#### `str.lower()`
**Syntax:** `string.lower()`  
**Description:** Converts all characters to lowercase  
**Example:**
```python
"HELLO".lower()  # "hello"
"HeLLo WoRLd".lower()  # "hello world"
```
**When to Use:** For case-insensitive comparisons or text standardization  
**Return Type:** `str`

---

#### `str.upper()`
**Syntax:** `string.upper()`  
**Description:** Converts all characters to uppercase  
**Example:**
```python
"hello".upper()  # "HELLO"
```
**When to Use:** To standardize text to uppercase for display or comparison  
**Return Type:** `str`

---

#### `str.capitalize()`
**Syntax:** `string.capitalize()`  
**Description:** Capitalizes the first character and lowercases the rest  
**Example:**
```python
"hello world".capitalize()  # "Hello world"
"HELLO WORLD".capitalize()  # "Hello world"
```
**When to Use:** To format sentence-style text  
**Return Type:** `str`

---

#### `str.title()`
**Syntax:** `string.title()`  
**Description:** Capitalizes the first letter of each word  
**Example:**
```python
"hello world".title()  # "Hello World"
"the great gatsby".title()  # "The Great Gatsby"
```
**When to Use:** To format titles or proper names  
**Return Type:** `str`

---

### **Search and Check Methods**

#### `str.startswith()`
**Syntax:** `string.startswith(prefix, start=0, end=None)`  
**Description:** Checks if string starts with the specified prefix  
**Example:**
```python
"Hello World".startswith("He")  # True
"Hello World".startswith("World")  # False
```
**When to Use:** To validate prefixes, filter strings, or check file paths  
**Return Type:** `bool`

---

#### `str.endswith()`
**Syntax:** `string.endswith(suffix, start=0, end=None)`  
**Description:** Checks if string ends with the specified suffix  
**Example:**
```python
"hello.txt".endswith(".txt")  # True
"image.png".endswith(".jpg")  # False
```
**When to Use:** To check file extensions or validate suffixes  
**Return Type:** `bool`

---

#### `str.find()`
**Syntax:** `string.find(substring, start=0, end=None)`  
**Description:** Returns the lowest index of substring, or -1 if not found  
**Example:**
```python
"hello".find("l")  # 2
"hello".find("z")  # -1
```
**When to Use:** To locate substring position when you want to handle "not found" gracefully  
**Return Type:** `int`

---

#### `str.index()`
**Syntax:** `string.index(substring, start=0, end=None)`  
**Description:** Returns the lowest index of substring, or raises ValueError  
**Example:**
```python
"hello".index("l")  # 2
# "hello".index("z")  # Raises ValueError
```
**When to Use:** Like `find()` but when you want an exception if substring not found  
**Return Type:** `int`

---

#### `str.count()`
**Syntax:** `string.count(substring, start=0, end=None)`  
**Description:** Counts non-overlapping occurrences of substring  
**Example:**
```python
"hello".count("l")  # 2
"banana".count("a")  # 3
```
**When to Use:** To count character or substring frequency in text analysis  
**Return Type:** `int`

---

### **Formatting Methods**

#### `str.format()`
**Syntax:** `string.format(*args, **kwargs)`  
**Description:** Formats string using placeholders  
**Example:**
```python
"Hello {}".format("World")  # "Hello World"
"{0} {1}".format("Hello", "World")  # "Hello World"
"{name} is {age}".format(name="John", age=30)  # "John is 30"
```
**When to Use:** To create formatted strings with dynamic variables  
**Return Type:** `str`

---

#### `str.zfill()`
**Syntax:** `string.zfill(width)`  
**Description:** Pads string with zeros on the left to reach specified width  
**Example:**
```python
"42".zfill(5)  # "00042"
"-42".zfill(5)  # "-0042"
```
**When to Use:** To create fixed-width numeric strings for IDs or sorting  
**Return Type:** `str`

---

#### `str.center()`
**Syntax:** `string.center(width, fillchar=' ')`  
**Description:** Centers string in field of given width  
**Example:**
```python
"hi".center(10, "-")  # "----hi----"
"test".center(8)  # "  test  "
```
**When to Use:** To center-align text in displays or reports  
**Return Type:** `str`

---

## 📝 List Methods

### **Adding Elements**

#### `list.append()`
**Syntax:** `list.append(element)`  
**Description:** Adds a single element to the end of list  
**Example:**
```python
lst = [1, 2]
lst.append(3)  # lst becomes [1, 2, 3]
```
**When to Use:** To add one item to the end of a list  
**Return Type:** `None` (modifies list in place)

---

#### `list.extend()`
**Syntax:** `list.extend(iterable)`  
**Description:** Extends list by appending all elements from an iterable  
**Example:**
```python
lst = [1, 2]
lst.extend([3, 4])  # lst becomes [1, 2, 3, 4]
lst.extend("ab")  # lst becomes [1, 2, 3, 4, 'a', 'b']
```
**When to Use:** To add multiple items from another list or iterable  
**Return Type:** `None` (modifies list in place)

---

#### `list.insert()`
**Syntax:** `list.insert(index, element)`  
**Description:** Inserts element at specified index position  
**Example:**
```python
lst = [1, 3]
lst.insert(1, 2)  # lst becomes [1, 2, 3]
```
**When to Use:** To add an item at a specific position  
**Return Type:** `None` (modifies list in place)

---

### **Removing Elements**

#### `list.remove()`
**Syntax:** `list.remove(element)`  
**Description:** Removes the first occurrence of specified element  
**Example:**
```python
lst = [1, 2, 3, 2]
lst.remove(2)  # lst becomes [1, 3, 2]
```
**When to Use:** To delete a specific value (raises ValueError if not found)  
**Return Type:** `None` (modifies list in place)

---

#### `list.pop()`
**Syntax:** `list.pop(index=-1)`  
**Description:** Removes and returns element at index (default: last element)  
**Example:**
```python
lst = [1, 2, 3]
x = lst.pop()  # x = 3, lst becomes [1, 2]
y = lst.pop(0)  # y = 1, lst becomes [2]
```
**When to Use:** To remove and retrieve the last or a specific item  
**Return Type:** Element that was removed

---

#### `list.clear()`
**Syntax:** `list.clear()`  
**Description:** Removes all elements from the list  
**Example:**
```python
lst = [1, 2, 3]
lst.clear()  # lst becomes []
```
**When to Use:** To empty a list completely  
**Return Type:** `None` (modifies list in place)

---

### **Searching and Counting**

#### `list.index()`
**Syntax:** `list.index(element, start=0, end=None)`  
**Description:** Returns the index of first occurrence of element  
**Example:**
```python
[1, 2, 3, 2].index(2)  # 1
# [1, 2, 3].index(5)  # Raises ValueError
```
**When to Use:** To find the position of an element  
**Return Type:** `int`

---

#### `list.count()`
**Syntax:** `list.count(element)`  
**Description:** Counts occurrences of element in list  
**Example:**
```python
[1, 2, 2, 3].count(2)  # 2
[1, 2, 3].count(5)  # 0
```
**When to Use:** To count frequency of a value  
**Return Type:** `int`

---

### **Ordering Methods**

#### `list.sort()`
**Syntax:** `list.sort(key=None, reverse=False)`  
**Description:** Sorts list in place in ascending or descending order  
**Example:**
```python
lst = [3, 1, 2]
lst.sort()  # lst becomes [1, 2, 3]
lst.sort(reverse=True)  # lst becomes [3, 2, 1]
```
**When to Use:** To order elements when you want to modify the original list  
**Return Type:** `None` (modifies list in place)

---

#### `list.reverse()`
**Syntax:** `list.reverse()`  
**Description:** Reverses the order of elements in place  
**Example:**
```python
lst = [1, 2, 3]
lst.reverse()  # lst becomes [3, 2, 1]
```
**When to Use:** To reverse the order of elements  
**Return Type:** `None` (modifies list in place)

---

### **Copying**

#### `list.copy()`
**Syntax:** `list.copy()`  
**Description:** Returns a shallow copy of the list  
**Example:**
```python
lst = [1, 2, 3]
new_lst = lst.copy()  # new_lst is [1, 2, 3]
new_lst.append(4)  # lst is still [1, 2, 3]
```
**When to Use:** To create an independent copy of a list  
**Return Type:** `list`

---

## 🗂️ Dictionary Methods

### **Accessing Elements**

#### `dict.get()`
**Syntax:** `dict.get(key, default=None)`  
**Description:** Returns value for key, or default if key doesn't exist  
**Example:**
```python
d = {"a": 1}
d.get("a")  # 1
d.get("b", 0)  # 0 (default value)
```
**When to Use:** To safely access keys without risking KeyError  
**Return Type:** Value or default

---

#### `dict.keys()`
**Syntax:** `dict.keys()`  
**Description:** Returns a view object of all dictionary keys  
**Example:**
```python
d = {"a": 1, "b": 2}
list(d.keys())  # ["a", "b"]
```
**When to Use:** To iterate over or access all keys  
**Return Type:** `dict_keys` view object

---

#### `dict.values()`
**Syntax:** `dict.values()`  
**Description:** Returns a view object of all dictionary values  
**Example:**
```python
d = {"a": 1, "b": 2}
list(d.values())  # [1, 2]
```
**When to Use:** To access all values in the dictionary  
**Return Type:** `dict_values` view object

---

#### `dict.items()`
**Syntax:** `dict.items()`  
**Description:** Returns a view object of key-value pairs as tuples  
**Example:**
```python
d = {"a": 1, "b": 2}
list(d.items())  # [("a", 1), ("b", 2)]
for key, value in d.items():
    print(f"{key}: {value}")
```
**When to Use:** To iterate over both keys and values simultaneously  
**Return Type:** `dict_items` view object

---

### **Modifying Dictionary**

#### `dict.pop()`
**Syntax:** `dict.pop(key, default=None)`  
**Description:** Removes key and returns its value  
**Example:**
```python
d = {"a": 1, "b": 2}
value = d.pop("a")  # value = 1, d becomes {"b": 2}
```
**When to Use:** To remove a key and retrieve its value  
**Return Type:** Value associated with key

---

#### `dict.popitem()`
**Syntax:** `dict.popitem()`  
**Description:** Removes and returns the last inserted key-value pair  
**Example:**
```python
d = {"a": 1, "b": 2}
item = d.popitem()  # item = ("b", 2), d becomes {"a": 1}
```
**When to Use:** To remove the most recently added item (LIFO)  
**Return Type:** `tuple` (key, value)

---

#### `dict.update()`
**Syntax:** `dict.update(other)`  
**Description:** Updates dictionary with key-value pairs from another dict  
**Example:**
```python
d = {"a": 1}
d.update({"b": 2, "c": 3})  # d becomes {"a": 1, "b": 2, "c": 3}
d.update(a=10)  # d becomes {"a": 10, "b": 2, "c": 3}
```
**When to Use:** To merge dictionaries or add multiple items at once  
**Return Type:** `None` (modifies dict in place)

---

#### `dict.clear()`
**Syntax:** `dict.clear()`  
**Description:** Removes all items from the dictionary  
**Example:**
```python
d = {"a": 1, "b": 2}
d.clear()  # d becomes {}
```
**When to Use:** To empty a dictionary completely  
**Return Type:** `None` (modifies dict in place)

---

#### `dict.setdefault()`
**Syntax:** `dict.setdefault(key, default=None)`  
**Description:** Returns value if key exists, else sets and returns default  
**Example:**
```python
d = {}
d.setdefault("a", 1)  # Returns 1, d becomes {"a": 1}
d.setdefault("a", 5)  # Returns 1 (key already exists)
```
**When to Use:** To get a value or initialize a key with a default value  
**Return Type:** Value

---

### **Copying**

#### `dict.copy()`
**Syntax:** `dict.copy()`  
**Description:** Returns a shallow copy of the dictionary  
**Example:**
```python
d = {"a": 1, "b": 2}
new_d = d.copy()  # new_d is {"a": 1, "b": 2}
```
**When to Use:** To create an independent copy of a dictionary  
**Return Type:** `dict`

---

## 🔢 Set Methods

### **Adding Elements**

#### `set.add()`
**Syntax:** `set.add(element)`  
**Description:** Adds a single element to the set  
**Example:**
```python
s = {1, 2}
s.add(3)  # s becomes {1, 2, 3}
s.add(2)  # s remains {1, 2, 3} (duplicates ignored)
```
**When to Use:** To add one element to a set  
**Return Type:** `None` (modifies set in place)

---

#### `set.update()`
**Syntax:** `set.update(iterable)`  
**Description:** Adds multiple elements from an iterable  
**Example:**
```python
s = {1}
s.update([2, 3])  # s becomes {1, 2, 3}
s.update("abc")  # s becomes {1, 2, 3, 'a', 'b', 'c'}
```
**When to Use:** To add multiple elements at once  
**Return Type:** `None` (modifies set in place)

---

### **Removing Elements**

#### `set.remove()`
**Syntax:** `set.remove(element)`  
**Description:** Removes element from set (raises error if not found)  
**Example:**
```python
s = {1, 2, 3}
s.remove(2)  # s becomes {1, 3}
# s.remove(5)  # Raises KeyError
```
**When to Use:** To remove an element when you expect it to exist  
**Return Type:** `None` (modifies set in place)

---

#### `set.discard()`
**Syntax:** `set.discard(element)`  
**Description:** Removes element from set (no error if not found)  
**Example:**
```python
s = {1, 2, 3}
s.discard(2)  # s becomes {1, 3}
s.discard(5)  # No error, s remains {1, 3}
```
**When to Use:** To safely remove an element without exceptions  
**Return Type:** `None` (modifies set in place)

---

#### `set.pop()`
**Syntax:** `set.pop()`  
**Description:** Removes and returns an arbitrary element  
**Example:**
```python
s = {1, 2, 3}
x = s.pop()  # x could be 1, 2, or 3 (arbitrary)
```
**When to Use:** To remove any element (order not guaranteed)  
**Return Type:** Element

---

#### `set.clear()`
**Syntax:** `set.clear()`  
**Description:** Removes all elements from the set  
**Example:**
```python
s = {1, 2, 3}
s.clear()  # s becomes set()
```
**When to Use:** To empty a set completely  
**Return Type:** `None` (modifies set in place)

---

### **Set Operations**

#### `set.union()`
**Syntax:** `set.union(*others)` or `set1 | set2`  
**Description:** Returns a new set with all elements from both sets  
**Example:**
```python
{1, 2}.union({2, 3})  # {1, 2, 3}
{1, 2} | {2, 3}  # {1, 2, 3}
```
**When to Use:** To combine sets (all unique elements)  
**Return Type:** `set`

---

#### `set.intersection()`
**Syntax:** `set.intersection(*others)` or `set1 & set2`  
**Description:** Returns a new set with elements common to all sets  
**Example:**
```python
{1, 2, 3}.intersection({2, 3, 4})  # {2, 3}
{1, 2, 3} & {2, 3, 4}  # {2, 3}
```
**When to Use:** To find shared elements between sets  
**Return Type:** `set`

---

#### `set.difference()`
**Syntax:** `set.difference(*others)` or `set1 - set2`  
**Description:** Returns elements in first set but not in others  
**Example:**
```python
{1, 2, 3}.difference({2, 3, 4})  # {1}
{1, 2, 3} - {2, 3, 4}  # {1}
```
**When to Use:** To find unique elements in the first set  
**Return Type:** `set`

---

#### `set.symmetric_difference()`
**Syntax:** `set.symmetric_difference(other)` or `set1 ^ set2`  
**Description:** Returns elements in either set but not both  
**Example:**
```python
{1, 2, 3}.symmetric_difference({2, 3, 4})  # {1, 4}
{1, 2, 3} ^ {2, 3, 4}  # {1, 4}
```
**When to Use:** To find elements unique to each set  
**Return Type:** `set`

---

### **Set Relationships**

#### `set.issubset()`
**Syntax:** `set.issubset(other)` or `set1 <= set2`  
**Description:** Checks if all elements of set are in other set  
**Example:**
```python
{1, 2}.issubset({1, 2, 3})  # True
{1, 2} <= {1, 2, 3}  # True
```
**When to Use:** To verify subset relationship  
**Return Type:** `bool`

---

#### `set.issuperset()`
**Syntax:** `set.issuperset(other)` or `set1 >= set2`  
**Description:** Checks if set contains all elements of other set  
**Example:**
```python
{1, 2, 3}.issuperset({1, 2})  # True
{1, 2, 3} >= {1, 2}  # True
```
**When to Use:** To verify superset relationship  
**Return Type:** `bool`

---

## 📦 Tuple Methods

Tuples are immutable, so they have only two methods:

#### `tuple.count()`
**Syntax:** `tuple.count(value)`  
**Description:** Counts occurrences of value in tuple  
**Example:**
```python
(1, 2, 2, 3).count(2)  # 2
```
**When to Use:** To count frequency of a value in a tuple  
**Return Type:** `int`

---

#### `tuple.index()`
**Syntax:** `tuple.index(value, start=0, end=None)`  
**Description:** Returns first index of value in tuple  
**Example:**
```python
(1, 2, 3).index(2)  # 1
```
**When to Use:** To find position of an element in a tuple  
**Return Type:** `int`

---

## 🛠️ Built-in Functions

### **Sequence Functions**

#### `len()`
**Syntax:** `len(object)`  
**Description:** Returns the number of items in an object  
**Example:**
```python
len([1, 2, 3])  # 3
len("hello")  # 5
len({"a": 1, "b": 2})  # 2
```
**When to Use:** To get the size/count of elements in any sequence or collection  
**Return Type:** `int`

---

#### `range()`
**Syntax:** `range(start, stop, step)`  
**Description:** Generates a sequence of numbers  
**Example:**
```python
list(range(5))  # [0, 1, 2, 3, 4]
list(range(1, 5))  # [1, 2, 3, 4]
list(range(0, 10, 2))  # [0, 2, 4, 6, 8]
```
**When to Use:** To create numeric sequences for loops or iterations  
**Return Type:** `range` object

---

#### `enumerate()`
**Syntax:** `enumerate(iterable, start=0)`  
**Description:** Returns an enumerate object with (index, value) pairs  
**Example:**
```python
list(enumerate(["a", "b", "c"]))  # [(0, "a"), (1, "b"), (2, "c")]
for i, val in enumerate(["x", "y"], start=1):
    print(f"{i}: {val}")  # 1: x, 2: y
```
**When to Use:** To iterate with both index and value  
**Return Type:** `enumerate` object

---

#### `zip()`
**Syntax:** `zip(*iterables)`  
**Description:** Combines multiple iterables into tuples  
**Example:**
```python
list(zip([1, 2], ["a", "b"]))  # [(1, "a"), (2, "b")]
list(zip([1, 2, 3], ["a", "b"]))  # [(1, "a"), (2, "b")]
```
**When to Use:** To pair elements from multiple sequences  
**Return Type:** `zip` object

---

### **Transformation Functions**

#### `map()`
**Syntax:** `map(function, iterable)`  
**Description:** Applies function to all items in iterable  
**Example:**
```python
list(map(str.upper, ["a", "b"]))  # ["A", "B"]
list(map(lambda x: x**2, [1, 2, 3]))  # [1, 4, 9]
```
**When to Use:** To transform all elements using a function  
**Return Type:** `map` object

---

#### `filter()`
**Syntax:** `filter(function, iterable)`  
**Description:** Filters elements based on function returning True  
**Example:**
```python
list(filter(lambda x: x > 0, [-1, 0, 1, 2]))  # [1, 2]
list(filter(str.isdigit, ["1", "a", "2"]))  # ["1", "2"]
```
**When to Use:** To select elements matching a condition  
**Return Type:** `filter` object

---

#### `sorted()`
**Syntax:** `sorted(iterable, key=None, reverse=False)`  
**Description:** Returns a new sorted list from iterable  
**Example:**
```python
sorted([3, 1, 2])  # [1, 2, 3]
sorted(["banana", "apple"], key=len)  # ["apple", "banana"]
```
**When to Use:** To get a sorted copy without modifying the original  
**Return Type:** `list`

---

#### `reversed()`
**Syntax:** `reversed(sequence)`  
**Description:** Returns a reverse iterator  
**Example:**
```python
list(reversed([1, 2, 3]))  # [3, 2, 1]
list(reversed("hello"))  # ['o', 'l', 'l', 'e', 'h']
```
**When to Use:** To iterate in reverse order  
**Return Type:** Reverse iterator

---

### **Numeric Functions**

#### `sum()`
**Syntax:** `sum(iterable, start=0)`  
**Description:** Sums all numeric elements in iterable  
**Example:**
```python
sum([1, 2, 3])  # 6
sum([1, 2, 3], 10)  # 16 (starts from 10)
```
**When to Use:** To calculate total of numbers  
**Return Type:** Number

---

#### `max()`
**Syntax:** `max(iterable)` or `max(a, b, ...)`  
**Description:** Returns the largest element  
**Example:**
```python
max([1, 5, 3])  # 5
max(1, 5, 3)  # 5
max(["apple", "banana"], key=len)  # "banana"
```
**When to Use:** To find the maximum value  
**Return Type:** Element

---

#### `min()`
**Syntax:** `min(iterable)` or `min(a, b, ...)`  
**Description:** Returns the smallest element  
**Example:**
```python
min([1, 5, 3])  # 1
min(1, 5, 3)  # 1
```
**When to Use:** To find the minimum value  
**Return Type:** Element

---

#### `abs()`
**Syntax:** `abs(number)`  
**Description:** Returns the absolute value (magnitude without sign)  
**Example:**
```python
abs(-5)  # 5
abs(5)  # 5
abs(-3.14)  # 3.14
```
**When to Use:** To get magnitude without sign  
**Return Type:** Number

---

#### `round()`
**Syntax:** `round(number, ndigits=None)`  
**Description:** Rounds number to specified decimal places  
**Example:**
```python
round(3.14159, 2)  # 3.14
round(3.5)  # 4
round(1234, -2)  # 1200
```
**When to Use:** To round floating point numbers  
**Return Type:** Number

---

### **Boolean Functions**

#### `all()`
**Syntax:** `all(iterable)`  
**Description:** Returns True if all elements are truthy (or empty iterable)  
**Example:**
```python
all([True, True, True])  # True
all([True, False, True])  # False
all([1, 2, 3])  # True (all non-zero)
```
**When to Use:** To check if all conditions are met  
**Return Type:** `bool`

---

#### `any()`
**Syntax:** `any(iterable)`  
**Description:** Returns True if any element is truthy  
**Example:**
```python
any([False, False, True])  # True
any([False, False, False])  # False
any([0, 0, 1])  # True
```
**When to Use:** To check if at least one condition is met  
**Return Type:** `bool`

---

### **Type Functions**

#### `type()`
**Syntax:** `type(object)`  
**Description:** Returns the type of the object  
**Example:**
```python
type([1, 2])  # <class 'list'>
type("hello")  # <class 'str'>
type(42)  # <class 'int'>
```
**When to Use:** To check or debug data types  
**Return Type:** `type`

---

#### `isinstance()`
**Syntax:** `isinstance(object, classinfo)`  
**Description:** Checks if object is an instance of class or tuple of classes  
**Example:**
```python
isinstance([1, 2], list)  # True
isinstance("hello", (str, int))  # True
isinstance(42, str)  # False
```
**When to Use:** To validate object types in a safer way than type()  
**Return Type:** `bool`

---

## 🔍 Quick Reference

### String Validation
- `isalnum()` - alphanumeric check
- `isalpha()` - alphabetic check
- `isdigit()` - numeric check
- `islower()` / `isupper()` - case check
- `isspace()` - whitespace check

### String Transformation
- `replace()` - substitute text
- `split()` - break into list
- `join()` - combine list to string
- `strip()` / `lstrip()` / `rstrip()` - remove characters

### String Case
- `lower()` / `upper()` - case conversion
- `capitalize()` - sentence case
- `title()` - title case

### String Search
- `startswith()` / `endswith()` - prefix/suffix check
- `find()` / `index()` - locate substring
- `count()` - count occurrences

### List Operations
- **Add:** `append()`, `extend()`, `insert()`
- **Remove:** `remove()`, `pop()`, `clear()`
- **Search:** `index()`, `count()`
- **Order:** `sort()`, `reverse()`

### Dictionary Operations
- **Access:** `get()`, `keys()`, `values()`, `items()`
- **Modify:** `pop()`, `popitem()`, `update()`, `clear()`
- **Special:** `setdefault()`

### Set Operations
- **Add:** `add()`, `update()`
- **Remove:** `remove()`, `discard()`, `pop()`, `clear()`
- **Operations:** `union()`, `intersection()`, `difference()`, `symmetric_difference()`
- **Checks:** `issubset()`, `issuperset()`

### Essential Built-ins
- **Sequence:** `len()`, `range()`, `enumerate()`, `zip()`
- **Transform:** `map()`, `filter()`, `sorted()`, `reversed()`
- **Math:** `sum()`, `max()`, `min()`, `abs()`, `round()`
- **Logic:** `all()`, `any()`
- **Type:** `type()`, `isinstance()`

---

## 💡 Pro Tips

1. **Immutability Matters:** Strings and tuples are immutable; methods return new objects instead of modifying in place
2. **In-Place vs Return:** List/dict/set methods often modify in place and return `None`
3. **Chaining:** String methods can be chained: `"  HELLO  ".strip().lower()` → `"hello"`
4. **Use `get()` for Dicts:** Safer than `dict[key]` as it won't raise KeyError
5. **Set Operations:** Use sets for fast membership testing and removing duplicates
6. **List Comprehensions:** Often cleaner than `map()` and `filter()` for simple transformations
7. **Check Before Remove:** Use `discard()` for sets or check `if element in list` before `list.remove()`

---

## 📚 Additional Resources

- [Python Official Documentation](https://docs.python.org/3/)
- [Python String Methods](https://docs.python.org/3/library/stdtypes.html#string-methods)
- [Python Built-in Functions](https://docs.python.org/3/library/functions.html)

---

**Created:** 2025  
**Version:** 1.0  
**Total Functions/Methods Documented:** 76

---

*This guide covers the most commonly used built-in functions and methods in Python for data structure operations and string manipulation. For a complete reference, consult the official Python documentation.*
