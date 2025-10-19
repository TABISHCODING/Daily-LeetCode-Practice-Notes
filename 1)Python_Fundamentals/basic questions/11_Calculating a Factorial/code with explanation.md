
# ✖️ Python Program: Calculating a Factorial

This guide explains how to write a Python program to calculate the factorial of a non-negative number. The factorial of a number `n`, denoted as `n!`, is the product of all positive integers up to `n` (e.g., $4! = 4 \times 3 \times 2 \times 1 = 24$).

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **The Accumulator Pattern** 🧺: This is a very common and important pattern in programming. You initialize a variable to a starting value (like `1` for multiplication or `0` for addition) before a loop, and then you update this variable in every iteration to "accumulate" a final result.

  * **Initialize with the Identity Value**: When accumulating a product, you must initialize your variable to **1** (the multiplicative identity). If you start with 0, the result will always be 0. When accumulating a sum, you would start with 0 (the additive identity).

  * **Use Built-in Modules First**: Python's `math` module has a highly optimized `math.factorial()` function. For real-world code, you should always prefer using these well-tested, built-in solutions over writing your own from scratch.

  * **Factorial Edge Cases**: Remember the specific mathematical rules: factorial is **not defined for negative numbers**, and **0\! is 1**. Your code must handle these special cases.

-----

## 📝 The Step-by-Step Approach (for the `for` loop)

Let's trace the logic for calculating the factorial of `4`.

1.  **Get and Prepare:** The program gets the number `4` from the user.

2.  **Handle Edge Cases:** The program first checks if the number is negative or zero. Since `4` is positive, it proceeds to the main calculation.

3.  **Initialize the Accumulator:** A variable, `factorial_loop`, is created and set to `1`. This variable will "accumulate" the product as we loop. It must start at 1, because anything multiplied by 1 is itself.

4.  **Execute the Loop:** The `for i in range(1, 4 + 1):` loop begins. It will run for `i = 1, 2, 3,` and `4`.

      * **Pass 1:** `i` is 1. `factorial_loop` becomes `1 * 1 = 1`.
      * **Pass 2:** `i` is 2. `factorial_loop` becomes `1 * 2 = 2`.
      * **Pass 3:** `i` is 3. `factorial_loop` becomes `2 * 3 = 6`.
      * **Pass 4:** `i` is 4. `factorial_loop` becomes `6 * 4 = 24`.

5.  **Announce the Final Result:** The loop has finished. The final value stored in `factorial_loop` is `24`, which is the correct answer for `4!`. This result is then printed.

-----

## 💻 The Final Code: Two Methods

As with many math problems, Python's `math` module provides a simple shortcut, but it's also great to learn the algorithmic approach using a loop.

### **Method 1: Using a Pre-defined Number**

This version is useful for quick tests without needing to enter a value each time.

```python
# Import the math module for the built-in function
import math

# A pre-defined non-negative number
num = 6
print(f"Calculating the factorial of {num}...")

# --- The Simple Way (using math.factorial) ---
factorial_simple = math.factorial(num)
print(f"\nUsing math.factorial(): {factorial_simple}")

# --- The Algorithmic Way (using a for loop) ---
factorial_loop = 1
# Factorial of 0 is 1
if num == 0:
    factorial_loop = 1
# Factorials are for positive numbers
elif num > 0:
    # Loop from 1 up to the number (inclusive)
    for i in range(1, num + 1):
        factorial_loop = factorial_loop * i
print(f"Using a for loop: {factorial_loop}")
```

### **Method 2: Taking a Number from the User**

This interactive version handles user input and shows the result using both algorithms.

```python
import math

try:
    # Get a whole number from the user
    num = int(input("Enter a non-negative number: "))

    # Check for the edge cases first
    if num < 0:
        print("Error: Factorial is not defined for negative numbers.")
    elif num == 0:
        print("The factorial of 0 is 1.")
    else:
        # --- The Simple Way (using math.factorial) ---
        print(f"\nUsing math.factorial(): {math.factorial(num)}")

        # --- The Algorithmic Way (using a for loop) ---
        factorial_loop = 1
        for i in range(1, num + 1):
            factorial_loop *= i # This is a shortcut for factorial_loop = factorial_loop * i
        print(f"Using a for loop: {factorial_loop}")

except ValueError:
    print("Error: Invalid input. Please enter a valid whole number.")
```
