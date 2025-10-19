
# 🔄 Python Program: Swapping Two Numbers

This guide explains how to write a Python program to swap the values of two variables (e.g., if `a = 10` and `b = 20`, after the swap `a` will be `20` and `b` will be `10`).

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **The "Pythonic" Swap (Tuple Unpacking)** ✨: The expression `a, b = b, a` is the preferred way to swap in Python. It's clean, readable, and efficient. Behind the scenes, Python creates a temporary tuple `(b, a)` and then unpacks it into the variables `a` and `b`.

  * **The Temporary Variable Algorithm**: The three-step process (`temp = a; a = b; b = temp`) is the classic, fundamental algorithm for swapping that works in nearly every programming language. Understanding this logic is crucial for a solid programming foundation.

  * **The Problem of Overwriting**: The core challenge in swapping is to avoid losing one of the original values. The temporary variable's only job is to hold one value safely while you perform the overwrite.

-----

## 📝 The Step-by-Step Approach (The Traditional Method)

The "Pythonic" swap (`a, b = b, a`) is a brilliant shortcut. To understand the logic of what's happening, let's break down the traditional method using a temporary variable.

Imagine you have two glasses: `a` (filled with juice) and `b` (filled with water). You can't just pour them into each other. You need a third, empty glass (`temp`).

1.  **Get the Numbers:** Let's say we have `a = 10` and `b = 20`.

2.  **Save One Value:** We must save one of the values before it gets overwritten. We copy the value of `a` into a new, temporary variable.

      * `temp = a` (`temp` is now 10).
      * (This is like pouring the juice from glass `a` into the empty `temp` glass).

3.  **Perform the First Assignment:** Now that `a`'s value is safe, we can overwrite `a` with the value from `b`.

      * `a = b` (`a` is now 20, `b` is still 20).
      * (This is like pouring the water from glass `b` into the now-empty glass `a`).

4.  **Complete the Swap:** Finally, we take the value we saved in `temp` and put it in `b`.

      * `b = temp` (`b` is now 10).
      * (This is like pouring the juice from the `temp` glass into the now-empty glass `b`).

The swap is complete\! `a` is 20 and `b` is 10.

-----

## 💻 The Final Code: Two Methods

Here are two methods to write the program in Python.

### **Method 1: Using Pre-defined Numbers**

This version shows both the Pythonic and Traditional methods for a quick test.

```python
# --- Setup ---
a = 10
b = 20
print("--- Before Swap ---")
print(f"a = {a}, b = {b}")

# --- The Pythonic Way (Tuple Unpacking) ---
a, b = b, a
print("\n--- After Pythonic Swap ---")
print(f"a = {a}, b = {b}")

# --- Resetting for the next method ---
a = 10
b = 20

# --- The Traditional Way (Using a Temporary Variable) ---
temp = a
a = b
b = temp
print("\n--- After Traditional Swap ---")
print(f"a = {a}, b = {b}")
```

### **Method 2: Taking Numbers from the User**

This interactive version uses the preferred Pythonic way and handles user input.

```python
try:
    # Get two numbers from the user
    num1 = float(input("Enter the first number (a): "))
    num2 = float(input("Enter the second number (b): "))

    print("\n--- Before Swap ---")
    print(f"a = {num1}, b = {num2}")

    # Perform the swap using the Pythonic way
    num1, num2 = num2, num1

    print("\n--- After Swap ---")
    print(f"a = {num1}, b = {num2}")

except ValueError:
    print("Error: Invalid input. Please enter valid numbers.")
```

  * **Example Run:**
    ```
    Enter the first number (a): 55
    Enter the second number (b): 99

    --- Before Swap ---
    a = 55.0, b = 99.0

    --- After Swap ---
    a = 99.0, b = 55.0
    ```
