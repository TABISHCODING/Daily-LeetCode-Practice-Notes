

# 🔢 Python Program: Checking for Odd or Even

This guide explains how to write a Python program to check if a number is odd or even. The core idea is based on a simple mathematical rule: a number is **even** if it's perfectly divisible by 2 (meaning the remainder is 0), and it's **odd** otherwise. To get the remainder in Python, we use the **modulo operator (`%`)**.

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **The Modulo Operator (`%`)** ➗: This is the most important concept here. The `%` operator doesn't give you the result of a division; it gives you the **remainder**. It's incredibly useful for problems involving divisibility, cycles, and patterns.

  * **The Definition of Even and Odd**: In programming, the mathematical definition is translated directly into code:

      * A number is **Even** if `number % 2 == 0`.
      * A number is **Odd** if `number % 2 != 0` (or if the 'even' check fails).

  * **Choose the Right Type (`int` vs `float`)**: Some problems are specific to certain number types. The odd/even distinction is a property of **integers** (whole numbers), so using `int()` for the conversion is more appropriate and logical here than using `float()`.

  * **`if-else` for Two Outcomes**: The `if-else` structure is perfect for situations where there are exactly two possible outcomes. If the condition is true, do one thing; otherwise, do the other thing.

-----

## 📝 The Step-by-Step Approach

This explains the logic behind the user-input version.

1.  **Get the Ingredient (Input):** The program needs one whole number to check. It uses `input()` to get this value from the user as a string.

2.  **Prepare the Ingredient (Conversion):** The concept of odd/even applies to whole numbers, so the program converts the input string to an **integer** using `int()`. The `try-except` block ensures this is done safely, catching errors if the user types text or a decimal number.

3.  **Perform the Test (Modulo Calculation):** This is the key step. The program calculates `number % 2`. This operation divides the number by 2 and returns only the **remainder**.

      * If `number` is `10`, `10 % 2` is `0`.
      * If `number` is `11`, `11 % 2` is `1`.

4.  **Make a Decision (`if-else`):** The program uses the result of the test to make a decision.

      * The `if number % 2 == 0:` statement asks, "Is the remainder of the division equal to 0?"
      * If **yes**, the code inside the `if` block runs, and the number is declared Even.
      * If **no**, the code inside the `else` block runs, and the number is declared Odd.

5.  **Announce the Result (Output):** Based on the decision, the program prints the correct conclusion to the user.

-----

## 💻 The Final Code: Two Methods

Here are two methods to write the program in Python.

### **Method 1: Using a Pre-defined Number**

This version is simple and useful for a quick test.

```python
# A pre-defined whole number
number = 42

# Check the remainder when divided by 2
# If the remainder is 0, the number is even.
if number % 2 == 0:
    print(f"The number {number} is Even.")
# Otherwise, the number must be odd.
else:
    print(f"The number {number} is Odd.")
```

  * **Output:**
    ```
    The number 42 is Even.
    ```

### **Method 2: Taking a Number from the User**

This interactive version includes error handling to ensure the user enters a whole number.

```python
try:
    # Get a number from the user and convert it to an integer
    number = int(input("Enter a whole number: "))

    # Use the modulo operator to check if the remainder is 0
    if number % 2 == 0:
        print(f"The number {number} is Even.")
    else:
        print(f"The number {number} is Odd.")

except ValueError:
    # This message prints if the input is not a valid whole number
    print("Error: Invalid input. Please enter a whole number.")
```

  * **Example Run:**
    ```
    Enter a whole number: 27
    The number 27 is Odd.
    ```
