

# ✖️ Python Program: Calculating a Factorial (Using Functions)

This guide explains how to write a Python program to calculate the factorial of a non-negative number. The factorial of a number `n`, denoted as `n!`, is the product of all positive integers up to `n` (e.g., $4! = 4 \times 3 \times 2 \times 1 = 24$).

We'll place the core logic inside a reusable **function**.

-----

## **Method 1: Calling the Function with a Pre-defined Number**

This is the most straightforward approach, where we call the function with a number written directly in the code.

### **Code:**

```python
# --- Function Definition ---
# We define a reusable block of code to do the calculation.
def calculate_factorial(n):
    # Handle the edge case where the number is negative
    if n < 0:
        return "Error: Not defined for negative numbers."
    # Handle the edge case where the number is 0
    elif n == 0:
        return 1
    # The main calculation logic
    else:
        factorial_result = 1
        for i in range(1, n + 1):
            factorial_result *= i
        return factorial_result

# --- Main Program ---
# Call the function with a pre-defined number (5)
result = calculate_factorial(5)
print(f"The factorial of 5 is: {result}")

# We can reuse the function easily!
result_2 = calculate_factorial(7)
print(f"The factorial of 7 is: {result_2}")
```

### **Output:**

```
The factorial of 5 is: 120
The factorial of 7 is: 5040
```

-----

## **Method 2: Calling the Function with User Input**

This method is more powerful because it allows the user to enter their own number. It requires a few extra steps to handle the input and the calculation logic correctly.

### **The Core Challenge: A Multi-Step Recipe** 👨‍🍳

Unlike a simple calculation, finding a factorial involves several distinct steps: getting user input, handling special rules (like for `0` or negative numbers), and performing a repetitive multiplication.

### **The Solution: A 5-Step Recipe**

Here's the step-by-step logic for the `calculate_factorial` function and how the main program uses it.

**Step 1: Get the Ingredient (Input)**

  * **Why we do this:** The program needs a number from the user to calculate its factorial. The `input()` function is the standard way to do this.
  * **Code:**
    ```python
    user_num_str = input("Enter a non-negative number: ")
    ```
  * **Example:** If you type `4`, the `user_num_str` variable holds the single text value `"4"`.

**Step 2: Prepare the Ingredient (Conversion)**

  * **Why we do this:** The user's input is always a string, but we need a whole number (an integer) to perform math. The `int()` function converts the string to a number. This is wrapped in a `try-except` block to catch errors if the user enters text.
  * **Code:**
    ```python
    user_num = int(user_num_str)
    ```
  * **Example:** The string `"4"` is converted into the integer `4`.

**Step 3: Handle Special Cases (The Chef's Notes)**

  * **Why we do this:** The factorial has special rules. The calculation for `4!` is different from the rule for `0!` or for negative numbers. The function must check these edge cases first.
  * **Code (inside the function):**
    ```python
    if n < 0:
        return "Error: Not defined for negative numbers."
    elif n == 0:
        return 1
    ```
  * **Example:** If the input number is `0`, the function immediately returns `1` and stops.

**Step 4: Execute the Recipe (The Accumulator Loop)**

  * **Why we do this:** This is the core calculation for positive numbers. To get $4!$ (`1 * 2 * 3 * 4`), we need to perform a repeated multiplication. A `for` loop is perfect for this. We use an "accumulator" variable (`factorial_result`) to keep track of the running product.
  * **Code (inside the function):**
    ```python
    factorial_result = 1
    for i in range(1, n + 1):
        factorial_result *= i # factorial_result = factorial_result * i
    return factorial_result
    ```
  * **Example (if `n` is 4):**
    1.  `factorial_result` starts at `1`.
    2.  The loop starts. First, `i` is `1`. `factorial_result` becomes `1 * 1 = 1`.
    3.  Next, `i` is `2`. `factorial_result` becomes `1 * 2 = 2`.
    4.  Next, `i` is `3`. `factorial_result` becomes `2 * 3 = 6`.
    5.  Finally, `i` is `4`. `factorial_result` becomes `6 * 4 = 24`.
    6.  The loop finishes, and the function returns the final value, `24`.

**Step 5: Serve the Result (Output)**

  * **Why we do this:** The main program, which called the function, receives the returned value. It then uses `print()` to display this final answer to the user.
  * **Code (in the main program):**
    ```python
    final_answer = calculate_factorial(user_num)
    print(f"The factorial of {user_num} is: {final_answer}")
    ```
  * **Example:** The program prints "The factorial of 4 is: 24".

-----

## **Putting It All Together: The Complete Code**

Here is the full program combining the function definition and the user-input logic.

```python
# --- Function Definition ---
# This function contains the complete logic for calculating a factorial.
def calculate_factorial(n):
    if n < 0:
        return "Error: Not defined for negative numbers."
    elif n == 0:
        return 1
    else:
        factorial_result = 1
        for i in range(1, n + 1):
            factorial_result *= i
        return factorial_result

# --- Main Program ---
# This part of the code interacts with the user and calls the function.
try:
    # Step 1 & 2: Get and Prepare the input
    user_num = int(input("Enter a non-negative number: "))

    # Step 4 & 5: Call the function and store/print the result
    final_answer = calculate_factorial(user_num)
    print(f"The factorial of {user_num} is: {final_answer}")

except ValueError:
    print("Error: Invalid input.")
```

### **Example Run:**

```
Enter a non-negative number: 6
The factorial of 6 is: 720
```
