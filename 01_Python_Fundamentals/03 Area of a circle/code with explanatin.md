
# ⭕ Python Program to Calculate the Area of a Circle

This guide explains how to write a Python program to calculate the area of a circle using the formula: $Area = \pi \times r^2$.

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **Import Modules for More Power** 🛠️: Python has built-in "modules" like `math` that give you extra features. You must `import` a module at the top of your file to use its functions and constants.

  * **Use Constants for Accuracy**: For universal constants like Pi, always use the version from the `math` module (`math.pi`) instead of typing `3.14`. It's more accurate and makes your code more professional.

  * **The Power Operator (`**`)**: The double-asterisk `**` is Python's operator for exponentiation (raising a number to a power). It's a direct and readable way to write formulas involving squares (`r²` becomes `radius ** 2`), cubes, and more.

  * **Format Your Output**: For numbers with many decimal places, you can format them inside an f-string to make them easier to read. The format `{variable:.2f}` rounds the number to 2 floating-point decimal places.

-----

## 📝 The Step-by-Step Approach

This explains the logic behind the user-input version.

1.  **Import the Tools:** The first step is `import math`. Think of this as getting a special toolkit. We need this toolkit because it contains a very accurate value for `math.pi`.

2.  **Define the Goal:** The program's purpose is to calculate a circle's area using the formula $Area = \pi \times r^2$.

3.  **Get the Ingredient (Input):** The formula requires one piece of information: the **radius**. The program uses `input()` to get this value from the user as a raw string.

4.  **Prepare the Ingredient (Conversion):** The raw string is converted to a `float` so we can use it in our math formula. The `try-except` block acts as a safety check to ensure the input is a valid number.

5.  **Execute the Formula (Calculation):** The program uses the prepared `radius` and the `math.pi` constant to perform the calculation: `area = math.pi * (radius ** 2)`.

6.  **Present the Result (Output):** Finally, the program uses `print()` and an f-string to display the final answer, formatted nicely to two decimal places.

-----

## 💻 The Final Code: Two Methods

Here are two methods to write the program in Python.

### **Method 1: Using a Pre-defined Radius**

This version is great for a quick test where the radius is already known.

```python
# Import the math module to use its constants, like pi
import math

# A pre-defined value for the circle's radius
radius = 10

# Calculate the area using the formula: π * r²
# The ** 2 means "to the power of 2" (squared)
area = math.pi * (radius ** 2)

# Print the result. We format it to 2 decimal places for a cleaner look.
print(f"The area of a circle with a radius of {radius} is {area:.2f}.")
```

  * **Output:**
    ```
    The area of a circle with a radius of 10 is 314.16.
    ```

### **Method 2: Taking the Radius from the User**

This interactive version handles user input and potential errors.

```python
# Import the math module
import math

# Use a try-except block to handle invalid input
try:
    # Ask the user for the radius and convert it to a float
    radius = float(input("Enter the radius of the circle: "))

    # Calculate the area
    area = math.pi * (radius ** 2)

    # Print the final, formatted result
    print(f"The area of a circle with a radius of {radius} is {area:.2f}.")

except ValueError:
    # This message prints if the user enters text that is not a number
    print("Error: Invalid input. Please enter a valid number for the radius.")
```

  * **Example Run:**
    ```
    Enter the radius of the circle: 4.5
    The area of a circle with a radius of 4.5 is 63.62.
    ```
