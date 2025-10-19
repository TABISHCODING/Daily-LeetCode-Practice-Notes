

# 🔄 Python Program: Reversing a Number

This guide explains how to write a Python program to reverse the digits of a whole number (e.g., `12345` becomes `54321`). We will explore a clever "Pythonic" trick, a classic mathematical algorithm, and an approach using a built-in function.

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **String Slicing (`[::-1]`)** ✂️: This is Python's powerful shortcut for reversing any sequence (like strings or lists). The code `str(num)[::-1]` converts the number to a string, reverses it, and then `int()` converts it back. It's the simplest and often the best way.

  * **The Modulo and Integer Division Trick**: The core of the mathematical method relies on two operators for manipulating digits:

      * `number % 10` always gets the **last digit**.
      * `number // 10` always **removes the last digit**.

  * **Algorithmic vs. Pythonic Solutions**: It's valuable to know both approaches. The string slicing method is a clean, readable, "Pythonic" solution. The `while` loop method is a language-agnostic algorithm that demonstrates a deeper understanding of number manipulation and is a common type of problem in technical interviews.

  * **Building a Number**: The pattern `new_number = (new_number * 10) + digit` is a standard technique for constructing an integer from its digits, one by one.

-----

## 📝 The Step-by-Step Approach (for the `while` loop)

The string slicing method is a simple one-line trick. The mathematical `while` loop method is more interesting and follows a clever algorithm. Let's break it down with the number `123`.

1.  **Get and Prepare:** The program gets the number `123`. It initializes two variables:

      * `reversed_num_math = 0` (to build our result)
      * `temp_num = 123` (a copy to tear apart, preserving the original)

2.  **Start the Loop:** The `while temp_num > 0:` loop begins because `123` is greater than 0.

3.  **First Pass of the Loop:** (`temp_num` is 123)

      * **Extract Last Digit:** `digit = 123 % 10` which gives `3`.
      * **Append to Result:** `reversed_num_math = (0 * 10) + 3` which makes `reversed_num_math` equal to `3`.
      * **Remove Last Digit:** `temp_num = 123 // 10` which gives `12`.

4.  **Second Pass of the Loop:** (`temp_num` is 12)

      * The loop continues because `12` is greater than 0.
      * **Extract Last Digit:** `digit = 12 % 10` which gives `2`.
      * **Append to Result:** `reversed_num_math = (3 * 10) + 2` which makes `reversed_num_math` equal to `32`.
      * **Remove Last Digit:** `temp_num = 12 // 10` which gives `1`.

5.  **Third Pass of the Loop:** (`temp_num` is 1)

      * The loop continues because `1` is greater than 0.
      * **Extract Last Digit:** `digit = 1 % 10` which gives `1`.
      * **Append to Result:** `reversed_num_math = (32 * 10) + 1` which makes `reversed_num_math` equal to `321`.
      * **Remove Last Digit:** `temp_num = 1 // 10` which gives `0`.

6.  **End the Loop:** The condition `temp_num > 0` is now false (`0` is not greater than `0`), so the loop terminates. The final `reversed_num_math` is `321`.

-----

## 💻 The Final Code: Three Approaches

Here are two methods for implementing the program, each showing the different approaches.

### **Method 1: Using a Pre-defined Number**

This version is useful for quick tests without needing to enter a value each time.

```python
# A pre-defined whole number to reverse
num = 12345
print(f"The original number is: {num}")

# --- 1. The Pythonic Way (String Slicing) ---
reversed_num_str = int(str(num)[::-1])
print(f"\nReversed using String Slicing: {reversed_num_str}")

# --- 2. The Built-in Function Way (reversed()) ---
# The reversed() function returns an iterator, so we must join the characters back together
reversed_num_func = int("".join(reversed(str(num))))
print(f"Reversed using reversed() function: {reversed_num_func}")

# --- 3. The Algorithmic Way (Math) ---
reversed_num_math = 0
# We need a copy of the number to work with
temp_num = num
while temp_num > 0:
    digit = temp_num % 10
    reversed_num_math = (reversed_num_math * 10) + digit
    temp_num = temp_num // 10
print(f"Reversed using a While Loop: {reversed_num_math}")
```

### **Method 2: Taking a Number from the User**

This interactive version handles user input and shows the result using all three algorithms.

```python
try:
    # Get a number from the user
    num = int(input("Enter a whole number to reverse: "))

    # --- Method 1: The Pythonic Way (String Slicing) ---
    print("\n--- Using String Slicing ---")
    reversed_num_str = int(str(num)[::-1])
    print(f"The reversed number is: {reversed_num_str}")

    # --- Method 2: The Built-in Function Way (reversed()) ---
    print("\n--- Using reversed() function ---")
    reversed_num_func = int("".join(reversed(str(num))))
    print(f"The reversed number is: {reversed_num_func}")

    # --- Method 3: The Algorithmic Way (Math) ---
    print("\n--- Using a While Loop ---")
    reversed_num_math = 0
    temp_num = num # Use a copy to preserve the original number
    while temp_num > 0:
        digit = temp_num % 10
        reversed_num_math = (reversed_num_math * 10) + digit
        temp_num = temp_num // 10
    print(f"The reversed number is: {reversed_num_math}")

except ValueError:
    print("Error: Invalid input. Please enter a whole number.")
```
