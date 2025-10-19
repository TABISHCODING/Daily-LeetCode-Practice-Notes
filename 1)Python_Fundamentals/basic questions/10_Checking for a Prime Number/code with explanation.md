

# 🔎 Python Program: Checking for a Prime Number

This guide explains how to write a Python program to determine if a given number is a prime number. A prime is a number **greater than 1** that is only divisible by 1 and itself.

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **The `for...else` Loop** 🧙: This is a unique feature in Python. The `else` block attached to a `for` loop executes **only if the loop completes without being terminated by a `break` statement**. It's perfect for search algorithms: the `if`/`break` handles the "found it" case, and the `else` handles the "searched everything and didn't find it" case.

  * **The `break` Statement**: The `break` statement provides a way to exit a loop immediately. This is essential for efficiency—as soon as you find one factor, you know the number isn't prime, so there's no need to continue checking.

  * **The Square Root Optimization**: Checking for factors only up to the **square root** of a number is a major performance improvement. If a number `n` has a factor larger than its square root, it must also have a corresponding factor smaller than its square root. So, we only need to check the smaller half.

  * **Prime Number Definition**: Remember the rule: A prime is a number **greater than 1** that is only divisible by 1 and itself. Your code must always handle the cases of 0, 1, and negative numbers.

-----

## 📝 The Step-by-Step Approach (Optimized)

This explains the logic of the optimized user-input version.

1.  **Get and Prepare:** The program gets a whole number from the user and converts it to an `int`. It also imports the `math` module to use its square root function.

2.  **Handle Edge Cases:** The first `if num > 1:` check is crucial. By definition, numbers less than or equal to 1 are not prime, so we handle them immediately.

3.  **Search for Factors:** The core idea is to search for any number `i` that divides `num` perfectly.

      * The `for i in range(2, int(math.sqrt(num)) + 1):` loop sets up this search. It efficiently checks only the necessary range of potential factors.
      * Inside the loop, `if (num % i) == 0:` asks, "Does `i` divide `num` with no remainder?"

4.  **Make a Decision (The `for...else` Logic):**

      * **If a factor is found:** The `if` condition is `True`. The program prints that the number is **not prime** and the `break` statement immediately stops the loop. The search is over.
      * **If no factors are found:** The loop will run through all possible values of `i` without the `if` condition ever being true. The `break` is never reached. When the loop finishes naturally, the special `else` block is executed, correctly printing that the number **is prime**.

-----

## 💻 The Final Code: Two Methods

Here are two methods to write the program in Python.

### **Method 1: Using a Pre-defined Number**

This version uses the `for...else` loop, which is a clean way to handle the logic.

```python
# A pre-defined number to check
num = 29

# Prime numbers must be greater than 1
if num > 1:
    # Check for factors from 2 up to the number
    for i in range(2, num):
        # If a factor is found, it's not a prime number
        if (num % i) == 0:
            print(f"{num} is not a prime number.")
            # Break the loop because we've found our answer
            break
    else:
        # This else block runs ONLY IF the for loop completes without a break
        print(f"{num} is a prime number.")
# If the number is 1 or less, it's not prime
else:
    print(f"{num} is not a prime number.")
```

### **Method 2: Taking a Number from the User (Optimized)**

This version is more efficient because it only checks for factors up to the square root of the number. It's the standard way to solve this problem.

```python
# Import the math module for the square root function
import math

try:
    # Get a number from the user
    num = int(input("Enter a whole number to check: "))

    # Prime numbers must be greater than 1
    if num > 1:
        # Loop from 2 up to the square root of the number
        for i in range(2, int(math.sqrt(num)) + 1):
            # If a factor is found, it's not a prime number
            if (num % i) == 0:
                print(f"{num} is not a prime number.")
                break
        else:
            # If the loop finishes without finding a factor, it's prime
            print(f"{num} is a prime number.")
    else:
        print(f"{num} is not a prime number.")

except ValueError:
    print("Error: Invalid input. Please enter a valid whole number.")
```
