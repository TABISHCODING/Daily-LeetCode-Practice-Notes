

# ✖️ Python Program: Calculating a Factorial (Using Functions)

This guide explains how to structure the factorial calculation program by placing the core logic inside a reusable **function**. The main program will then call this function to get the result.

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **`def` and `return`**: These are the essential keywords. `def` starts a function definition, and `return` sends a value out of it.

  * **Reusability**: This is the biggest advantage of functions. We defined the factorial logic once but could call it multiple times with different numbers (`calculate_factorial(5)`, `calculate_factorial(7)`, etc.).

  * **Organization**: Functions help break your program into logical, named pieces. The main part of the script is now very simple: get a number, call the function, print the result. The complex logic is neatly tucked away.

-----

## 📝 The Step-by-Step Approach

This explains the logic of defining and calling the factorial function.

1.  **Define the Function:** We start with `def calculate_factorial(n):`. This creates a function named `calculate_factorial` that takes one input, which it will call `n` inside the function.

2.  **Place Logic Inside:** The entire logic for handling negative numbers, zero, and the `for` loop calculation is placed inside the indented block of the function.

3.  **Return the Result:** Instead of printing, the function uses the `return` keyword to send the final calculated value back to wherever the function was called.

4.  **Call the Function:** In the main part of the script, the line `final_answer = calculate_factorial(user_num)` **calls** the function. It sends the `user_num` as an argument, the function runs its logic, and the `return` value is then stored in the `final_answer` variable.

-----

## 💻 The Final Code: Two Methods

First, we'll create a function that handles the factorial calculation. Then, our main program will call this function.

### **Method 1: Calling the Function with a Pre-defined Number**

```python
import math

# --- Function Definition ---
# We define a reusable block of code to do the calculation.
# 'n' is a parameter that accepts the number we want to process.
def calculate_factorial(n):
    # Handle edge cases first
    if n < 0:
        return "Error: Not defined for negative numbers."
    elif n == 0:
        return 1
    else:
        # The accumulator and loop logic is now inside the function
        factorial_result = 1
        for i in range(1, n + 1):
            factorial_result *= i
        # The function sends back the final calculated value
        return factorial_result

# --- Main Program ---
# Call the function with a pre-defined number (5)
result = calculate_factorial(5)
print(f"The factorial of 5 is: {result}")

# We can reuse it easily!
result_2 = calculate_factorial(7)
print(f"The factorial of 7 is: {result_2}")
```

### **Method 2: Calling the Function with User Input**

```python
import math

# The function definition is the same as above
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
try:
    user_num = int(input("Enter a non-negative number: "))
    # Call the function with the user's number
    final_answer = calculate_factorial(user_num)
    print(f"The factorial of {user_num} is: {final_answer}")

except ValueError:
    print("Error: Invalid input.")
```
