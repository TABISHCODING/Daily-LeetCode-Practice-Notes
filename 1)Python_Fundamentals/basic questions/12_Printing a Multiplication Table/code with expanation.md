

# ✖️ Python Program: Printing a Multiplication Table

This guide explains how to write a Python program that generates a multiplication table for a given number. The `for` loop is the perfect tool for this, as we need to repeat the multiplication for a specific sequence of numbers (e.g., 1 through 10).

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **Loops for Automation** ⚙️: This is a classic example of using a loop to automate a repetitive task. Instead of writing 10 separate `print` statements, a simple 3-line loop does all the work.

  * **Formatted Strings (`f-strings`) for Clean Output**: F-strings are incredibly useful for creating well-formatted, dynamic text. The ability to embed variables directly inside the string (`f"{num} x {i} = {product}"`) is perfect for tasks like this.

  * **The Loop Variable is a Tool**: The variable in the loop (`i` in our example) isn't just a counter; it's a value you can actively use in your calculations within each iteration. Here, we use it as the multiplier.

  * **Combining Input and Loops**: A common programming pattern is to get input from a user to set the parameters for a repetitive task. Here, the user's number `num` defines the core of the calculation that happens inside the loop.

-----

## 📝 The Step-by-Step Approach

Let's break down the logic of the user-input version.

1.  **Get the Base Number:** The program first needs to know which table to generate. It asks the user for a number and converts the input string to an integer `num`.

2.  **Set Up the Repetition:** A multiplication table repeats the same action (multiply and print) for a sequence of numbers (1, 2, 3, ...). The `for i in range(1, 11):` line sets up this repetition. It creates a loop that will run 10 times, with the variable `i` taking on the values 1 through 10 in each pass.

3.  **Execute Inside the Loop:** For each value of `i` that the loop provides:

      * **Calculate:** The program performs the multiplication for that line of the table: `product = num * i`.
      * **Print:** It uses a formatted f-string to display the entire equation in a neat, readable line, like `7 x 1 = 7`.

4.  **Repeat Until Done:** The loop automatically moves to the next number in the range and repeats Step 3. This continues until `i` has gone through all the numbers from 1 to 10, at which point the table is complete and the loop terminates.

-----

## 💻 The Final Code: Two Methods

Here are two methods to write the program in Python.

### **Method 1: Using a Pre-defined Number**

This version is simple and useful for a quick test.

```python
# The number for which to generate the table
num = 7

print(f"--- Multiplication Table for {num} ---")

# Loop through numbers 1 to 10 (inclusive)
for i in range(1, 11):
    # For each number 'i', calculate the product and print it
    product = num * i
    print(f"{num} x {i} = {product}")
```

### **Method 2: Taking a Number from the User**

This interactive version allows the user to choose the number for the table.

```python
try:
    # Get a number from the user
    num = int(input("Enter a number to see its multiplication table: "))

    print(f"\n--- Multiplication Table for {num} ---")

    # Loop from 1 to 10
    for i in range(1, 11):
        # Calculate the product in each iteration
        product = num * i
        # Print the result in a clean format
        print(f"{num} x {i} = {product}")

except ValueError:
    print("Error: Invalid input. Please enter a valid whole number.")
```

  * **Example Run:**
    ```
    Enter a number to see its multiplication table: 5

    --- Multiplication Table for 5 ---
    5 x 1 = 5
    5 x 2 = 10
    5 x 3 = 15
    5 x 4 = 20
    5 x 5 = 25
    5 x 6 = 30
    5 x 7 = 35
    5 x 8 = 40
    5 x 9 = 45
    5 x 10 = 50
    ```
