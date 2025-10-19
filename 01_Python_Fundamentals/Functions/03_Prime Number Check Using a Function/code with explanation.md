
# 🔎 Python Program: Prime Number Check Using a Function

For checking a prime, a great practice is to have the function return a simple **`True`** or **`False`** (a Boolean value). This makes the function reusable and the main program's logic clean and readable.

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **Functions Should Do One Thing Well:** The `is_prime` function has one job: checking for primality. It doesn't get input or print results. This makes it more reusable and your code cleaner. This is called the **Single Responsibility Principle**.

  * **Returning Booleans (`True` / `False`)**: This is the standard way for a function to answer a yes/no question. It makes the calling code simple and readable (`if is_prime(num):`).

  * **Separation of Concerns**: Notice the clean separation. The main program handles **user interaction** (input and output), while the function handles the **core logic** (the algorithm).

-----

## 📝 The Step-by-Step Approach

This explains the logic of defining and using the boolean-based `is_prime` function.

1.  **Define the Function:** We define `def is_prime(n):`. Its job is to determine if `n` is prime.

2.  **Return Boolean Values:** Instead of printing, the function returns `True` or `False`. This is very powerful because the result can be used in other logic, like an `if` statement.

3.  **Return Early:** As soon as the function knows the answer, it returns. If `n <= 1`, it immediately `return False`. If it finds a factor in the loop, it immediately `return False`.

4.  **The "Success" Case:** If the loop finishes completely without finding any factors, it means the number is prime, and the function returns `True` at the very end.

5.  **Use the Return Value:** The main program calls the function inside an `if` statement: `if is_prime(user_num):`. This works because `is_prime(user_num)` will evaluate to either `True` or `False`, directly controlling the `if-else` block.

-----

## 💻 The Final Code: Two Methods

### **Method 1: Calling the Function with a Pre-defined Number**

```python
import math

# --- Function Definition ---
# This function will answer a yes/no question: is the number prime?
def is_prime(n):
    # Handle edge cases
    if n <= 1:
        return False  # Not prime

    # Loop to check for factors
    for i in range(2, int(math.sqrt(n)) + 1):
        if (n % i) == 0:
            return False  # Factor found, so not prime

    # If the loop finishes without finding a factor, it is prime
    return True

# --- Main Program ---
num_to_check = 29
# Use the function directly in an if statement
if is_prime(num_to_check):
    print(f"{num_to_check} is a prime number.")
else:
    print(f"{num_to_check} is not a prime number.")
```

### **Method 2: Calling the Function with User Input**

```python
import math

# The function definition is the same as above
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(math.sqrt(n)) + 1):
        if (n % i) == 0:
            return False
    return True

# --- Main Program ---
try:
    user_num = int(input("Enter a whole number to check: "))

    # Call the function and check its True/False return value
    if is_prime(user_num):
        print(f"{user_num} is a prime number.")
    else:
        print(f"{user_num} is not a prime number.")

except ValueError:
    print("Error: Invalid input.")
```
