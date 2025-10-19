
# 🗓️ Python Program: Checking for a Leap Year

This guide explains how to write a Python program to determine if a given year is a leap year. The logic is a classic programming problem that involves a specific set of rules.

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **Complex Boolean Logic (`and`, `or`)** 🧠: You can combine multiple checks into one powerful condition using logical operators.

      * `and`: Requires **both** conditions to be true.
      * `or`: Requires **at least one** of the conditions to be true.

  * **Parentheses for Order of Operations**: Just like in math, you can use parentheses `()` to group logical checks. This ensures Python evaluates your rules in the correct order and makes the code much easier for humans to read.

  * **The "Not Equal To" Operator (`!=`)**: The `!=` operator is the opposite of `==`. It checks if two values are **not equal**. It's essential for the leap year rule "not divisible by 100."

  * **The Leap Year Algorithm**: The specific set of rules for a leap year is a classic programming problem. Remembering the logic—**(divisible by 4 and not by 100) or (divisible by 400)**—is a key takeaway.

-----

## 📝 The Step-by-Step Approach

This explains how the program evaluates the complex leap year rules.

1.  **Get the Ingredient (Input):** The program needs one piece of information: the **year**. It gets this from the user as a string using `input()`.

2.  **Prepare the Ingredient (Conversion):** A year is a whole number, so the program converts the input string to an **integer** using `int()`. The `try-except` block ensures this is done safely.

3.  **Apply the Rules (Complex Logic):** This is the core of the program. The `if` statement checks a single, complex condition which translates the rules into code:

      * `year % 4 == 0 and year % 100 != 0`: This part checks the first rule. Is the year divisible by 4 **and** at the same time not divisible by 100? This is true for years like 2024, 1996, etc.
      * `year % 400 == 0`: This part checks the second rule. Is the year divisible by 400? This is true for special century years like 1600, 2000, etc.

    The `or` in the middle means the entire condition is **True** if **either** of these two parts is **True**.

4.  **Make a Decision and Announce the Result:**

      * If the complex condition is met, the program executes the `if` block and declares it a Leap Year.
      * If the condition is not met (like for 1900, which is divisible by 100 but not 400), the `else` block runs.

-----

## 💻 The Final Code: Two Methods

Here are two methods to write the program in Python.

### **Method 1: Using a Pre-defined Year**

This version is simple and useful for a quick test.

```python
# A pre-defined year
year = 2000

# Check the leap year conditions using Boolean logic
# (Divisible by 4 AND NOT divisible by 100) OR (Divisible by 400)
if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
    print(f"The year {year} is a Leap Year.")
else:
    print(f"The year {year} is not a Leap Year.")
```

  * **Output:**
    ```
    The year 2000 is a Leap Year.
    ```

### **Method 2: Taking the Year from the User**

This interactive version includes error handling for invalid input.

```python
try:
    # Get the year from the user and convert to an integer
    year = int(input("Enter a year to check: "))

    # Apply the leap year rules in a single if statement
    if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
        print(f"The year {year} is a Leap Year.")
    else:
        print(f"The year {year} is not a Leap Year.")

except ValueError:
    # This message prints if the input is not a valid whole number
    print("Error: Invalid input. Please enter a valid year.")
```

  * **Example Run:**
    ```
    Enter a year to check: 1900
    The year 1900 is not a Leap Year.
    ```
