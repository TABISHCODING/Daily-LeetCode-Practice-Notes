
# 🔎 Python Program: Performing a Linear Search

A **linear search** is the most straightforward way to find an item in a list. It simply starts at the beginning of the list and checks each item, one by one, until it finds what it's looking for or reaches the end.

This guide explains how to implement this search inside a function that will return the **index** of the item if it's found, or **-1** if it's not found.

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **The `enumerate()` Function:** This is a very useful Python function that lets you loop over a sequence while getting both the **index** and the **value** at the same time. It's perfect for algorithms like linear search where you need the position of an item.

  * **Returning `-1` for "Not Found":** It is a standard convention in programming to return `-1` from a search function when the item is not found. This works because `-1` is never a valid index in a list, so it's an unmistakable signal of failure.

  * **Sequential and Simple:** Linear search is easy to understand and implement. Its major drawback is that it can be slow on very large lists because, in the worst-case scenario, it has to look at every single element.

  * **The `break` vs. `return` in a Loop:** In our prime number check, we used `break` to exit the loop. Here, we use `return` because we are inside a function. A `return` statement exits not just the loop, but the **entire function**, sending a value back immediately.

-----

## ✨ A Deep Dive into the `enumerate()` Function

This function is at the heart of our clean solution. Let's break down exactly how it works.

### **1. What `for index, value in enumerate(data_list)` Means**

In short, `enumerate()` takes a list and pairs each item with its index number. The `for index, value in ...` syntax is a special way to "unpack" those pairs as the loop runs.

  * **First, what does `enumerate()` do?**
    It takes a list like `['a', 'b', 'c']` and turns it into a sequence of pairs (specifically, tuples), where each pair contains the index and the value.
    So, `enumerate(['a', 'b', 'c'])` produces:

      * `(0, 'a')`
      * `(1, 'b')`
      * `(2, 'c')`

  * **Second, what does `for index, value in ...` do?**
    This is called **tuple unpacking**. The `for` loop grabs the first pair, `(0, 'a')`, and because you provided two variable names (`index`, `value`), it automatically "unpacks" the pair:

      * `0` gets assigned to `index`.
      * `'a'` gets assigned to `value`.
        This happens for each pair in the sequence, giving you both the position and the item in separate, convenient variables inside the loop.

### **2. What Happens if You Only Write `for value in enumerate(data_list)`?**

If you only provide **one** variable name after `for`, then Python does **not** unpack the pair. Instead, it assigns the **entire tuple** to that single variable.

  * **Example:**
    ```python
    data_list = ['apple', 'banana', 'cherry']

    # Using only one variable, let's call it 'item'
    for item in enumerate(data_list):
        print(item)
    ```
  * **Output:**
    ```
    (0, 'apple')
    (1, 'banana')
    (2, 'cherry')
    ```

As you can see, the `item` variable now holds the complete `(index, value)` pair on each pass of the loop. This is still useful, but if you wanted to access the index or value, you'd have to do it manually like `item[0]` and `item[1]`, which is less convenient than unpacking.

-----

## 📝 The Step-by-Step Approach

Let's break down the logic of the `linear_search` function. Imagine you're looking for the number `45` in the list `[11, 23, 45, 56]`.

1.  **Start at the Beginning:** The search begins at the first item of the list (index 0).

2.  **Check Each Item Sequentially:** The `for` loop goes through the list one item at a time.

      * **Pass 1:** It looks at index 0. The value is `11`. Is `11 == 45`? No. It moves on.
      * **Pass 2:** It looks at index 1. The value is `23`. Is `23 == 45`? No. It moves on.
      * **Pass 3:** It looks at index 2. The value is `45`. Is `45 == 45`? Yes\!

3.  **Handle a "Found" Case:** As soon as the `if value == target:` condition is true, the search is over. The function immediately stops and **returns the current index**, which is `2`.

4.  **Handle a "Not Found" Case:** If the loop were to check every single item in the list and never find a match, it would finish without ever hitting the `return index` line. Only after the loop is completely done, the final line, `return -1`, is executed. This acts as a signal that the target was not in the list.

-----

## 💻 The Final Code: Two Methods

### **Method 1: Using a Pre-defined List**

```python
# --- Function Definition ---
# This function searches for a 'target' in a 'data_list'.
def linear_search(data_list, target):
    # 'enumerate' gives us both the index and the value for each item.
    for index, value in enumerate(data_list):
        # Check if the current value matches the target
        if value == target:
            # If it matches, return the index immediately
            return index
    # If the loop finishes without finding the target, return -1
    return -1

# --- Main Program ---
my_data = [11, 23, 45, 56, 78, 90]
target_to_find = 56

# Call the function to perform the search
found_index = linear_search(my_data, target_to_find)

# Check the result
if found_index != -1:
    print(f"Target {target_to_find} found at index: {found_index}")
else:
    print(f"Target {target_to_find} was not found in the list.")
```

### **Method 2: Taking User Input**

```python
# The function definition is the same as above
def linear_search(data_list, target):
    for index, value in enumerate(data_list):
        if value == target:
            return index
    return -1

# --- Main Program ---
try:
    # Get a list of numbers from the user
    input_str = input("Enter a list of numbers separated by spaces: ")
    data = [int(num) for num in input_str.split()]

    # Get the target number to search for
    target = int(input("Enter the number to search for: "))

    # Call the search function
    result_index = linear_search(data, target)

    # Check the result and inform the user
    if result_index != -1:
        print(f"\nTarget {target} was found at index: {result_index}")
    else:
        print(f"\nTarget {target} was not found in the list.")

except ValueError:
    print("Error: Please enter valid whole numbers.")
```
