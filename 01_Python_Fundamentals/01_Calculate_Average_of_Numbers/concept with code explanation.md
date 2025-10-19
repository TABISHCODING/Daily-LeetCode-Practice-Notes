
-----

# Python Program to Calculate Average

## Goal: Calculate the Average of a List of Numbers

Our main objective is to write a Python program that can calculate the average of a set of numbers. The mathematical formula for an average is simple:

Average=Count of Numbers/Sum of Numbers
​
We'll explore two ways to do this in Python.

-----

## Method 1: Using a Pre-defined List (The Simple Way)

This is the most straightforward approach, where we define the list of numbers directly in the code.

### Code:

```python
# A list of numbers
numbers = [10, 20, 30, 45, 55]
# Calculate the sum of the numbers in the list
total_sum = sum(numbers)
# Count how many numbers are in the list
count = len(numbers)
# Calculate the average by dividing the sum by the count
average = total_sum / count
# Print the final result
print(f"The list of numbers is: {numbers}")
print(f"The average is: {average}")
```

### Output:

```
The list of numbers is: [10, 20, 30, 45, 55]
The average is: 32.0
```

-----

## Method 2: Taking Input from the User (The Flexible Way)

This method is more powerful because it allows the user to enter their own numbers each time the program runs. However, handling user input requires a few extra steps because of how Python treats it.

### The Core Challenge: Computers are Literal 🤖

Before we write the code, we must understand some fundamental rules:

  * **`input()` Always Returns a String:** No matter what the user types—numbers, letters, or symbols—the `input()` function captures it all as a single piece of text (a **string**).
  * **You Can't Do Math on Strings:** Trying to perform mathematical operations on a string like `"10"` will cause an error. The computer sees text, not a number.
  * **Conversion Functions (`int()`, `float()`) are Specialists:** These functions are designed to convert **one** clean string that looks like a number (e.g., `"123"`) into an actual number. They will fail if the string has spaces or multiple numbers (e.g., `int("10 20 30")` causes a `ValueError`).

Because of these rules, we need a special "assembly line" workflow to process a user's input of multiple numbers.

### The Solution: A 5-Step Data Assembly Line

Here's the step-by-step logic to correctly gather, clean, convert, and calculate the average from user input.

**Step 1: Get Raw Input as a Single String**

  * **Why we do this:** The program's first job is to get the information from the user. The `input()` function is the standard way to do this.
  * **Code:**
    ```python
    input_string = input("Enter a list of numbers separated by space: ")
    ```
  * **Example:** If you type `10 20 30`, the `input_string` variable holds the single text value `"10 20 30"`. The computer does not yet see these as separate numbers.

**Step 2: Split the String into a List of Smaller Strings**

  * **Why we do this:** We need to work with each number individually, but right now they are all stuck together. The `.split()` method acts like scissors, cutting the string at each space to create a list of smaller strings.
  * **Code:**
    ```python
    numbers_str_list = input_string.split()
    ```
  * **Example:** The string `"10 20 30"` is split into the list `['10', '20', '30']`. Notice these are **still strings** (text), not yet numbers.

**Step 3: Convert Each String into an Actual Number**

  * **Why we do this:** This is the most critical transformation. We cannot perform math on text. We use a `for` loop to go through our list of strings, convert each one into an actual number (`int`), and add it to a new, clean list.
  * **Code:**
    ```python
    numbers = []  # Create a new, empty list to hold the numbers
    for num_str in numbers_str_list:
        numbers.append(int(num_str))
    ```
  * **Example:** The loop processes `['10', '20', '30']` one item at a time. `'10'` becomes `10`, `'20'` becomes `20`, etc. After the loop, the `numbers` list contains `[10, 20, 30]`. This list is now ready for calculation.

**Step 4: Calculate the Average**

  * **Why we do this:** Now that we have a clean list of actual numbers, we can finally compute the average using the same logic from Method 1.
  * **Code:**
    ```python
    total_sum = sum(numbers)
    count = len(numbers)
    average = total_sum / count
    ```
  * **Example:** For the list `[10, 20, 30]`:
      * `sum(numbers)` adds them all up (`10 + 20 + 30 = 60`).
      * `len(numbers)` counts how many there are (3).
      * The division `60 / 3` gives us the final average of `20`.

**Step 5: Display the Final Result**

  * **Why we do this:** The program has the answer, but it needs to communicate it back to the user. The `print()` function displays the result on the screen.
  * **Code:**
    ```python
    print(f"The average of your numbers is: {average}")
    ```

-----

## Putting It All Together: The Complete Code

Here is the full program combining all the steps.

```python
# Step 1: Ask the user to enter numbers, separated by spaces
input_string = input("Enter a list of numbers separated by space: ")
# Step 2: Split the user's input string into a list of strings
numbers_str_list = input_string.split()
# Step 3: Convert the list of strings into a list of numbers (integers)
# We use a loop to go through each item and convert it.
numbers = []
for num_str in numbers_str_list:
    numbers.append(int(num_str))
# Step 4: Calculate the sum and count
total_sum = sum(numbers)
count = len(numbers)
# Calculate the average
average = total_sum / count
# Step 5: Print the result
print(f"The average of your numbers is: {average}")
```

### Example Run:

```
Enter a list of numbers separated by space: 5 10 15 20
The average of your numbers is: 12.5
```

-----

## Summary: Python Concepts Used (Cheat Sheet)

Here are the key Python tools we used in this guide.

| Concept      | What It Does                                      | Example Syntax                                |
| :----------- | :------------------------------------------------ | :-------------------------------------------- |
| **Variables**| Stores a piece of data with a name.               | `my_name = "Gemini"`                          |
| **Lists** | Holds an ordered collection of items.             | `scores = [95, 88, 100]`                      |
| `len()`      | Counts the number of items in a list.             | `count = len(scores)`                         |
| `sum()`      | Adds up all the numbers in a list.                | `total = sum(scores)`                         |
| `input()`    | Gets text input from the user.                    | `user_text = input("Enter your name: ")`      |
| `.split()`   | Splits a string into a list of smaller strings.   | `words = "one two three".split()`             |
| `for` Loop   | Repeats a block of code for each item in a list.  | `for score in scores: print(score)`           |
| `int()`      | Converts a string into a whole number (integer).  | `number = int("123")`                         |
| `.append()`  | Adds a single item to the end of a list.          | `scores.append(75)`                           |
| **f-string** | Displays output with variables inside the string. | `print(f"Your score is: {score}")`            |
