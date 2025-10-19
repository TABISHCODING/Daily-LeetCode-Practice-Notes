
# ↔️ Python Program: Checking for a Palindrome Number

A **palindrome** is a number (or word) that reads the same forwards and backward, like `121`, `545`, or `1331`. The easiest way to check this is by converting the number to a string.

-----

## 💡 Core Concepts to Know

Here are the most important concepts to understand for this task.

  * **Solve Problems with the Right Data Type**: This is a fantastic example of a problem that is difficult with math but incredibly simple if you convert the number to a string. Choosing the right data type for the task is a key programming skill.

  * **Returning a Boolean Expression**: The line `return str(n) == str(n)[::-1]` is a concise and "Pythonic" way of writing code. Instead of a longer `if-else` block, we can directly return the result of the comparison itself, as it will always be either `True` or `False`.

  * **Leveraging Previous Concepts**: This solution directly uses the string reversal concept (`[::-1]`) from a previous problem, showing how you can combine tools and techniques to solve new challenges.

-----

## 📝 The Step-by-Step Approach

This explains the logic behind the `is_palindrome` function.

1.  **Define the Function:** `def is_palindrome(n):` creates a function whose job is to answer the question, "Is `n` a palindrome?"

2.  **Convert to String:** The clever trick is to solve this problem with string manipulation. The first step inside the function is to treat the number `n` as a string: `str(n)`.

3.  **Reverse the String:** We use the string slicing trick `[::-1]` that we learned earlier to create a reversed version of the string.

4.  **Compare and Return:** The expression `str(n) == str(n)[::-1]` compares the original string with its reversed version.

      * If they are identical (e.g., `'121' == '121'`), the expression is `True`.
      * If they are different (e.g., `'123' == '321'`), the expression is `False`.

    The function directly returns this `True` or `False` value.

-----

## 💻 The Final Code: Two Methods

### **Method 1: Calling the Function with a Pre-defined Number**

```python
# --- Function Definition ---
# This function returns True if the number is a palindrome, False otherwise.
def is_palindrome(n):
    # Convert number to string and compare it with its reverse
    return str(n) == str(n)[::-1]

# --- Main Program ---
num_to_check = 12321
if is_palindrome(num_to_check):
    print(f"{num_to_check} is a palindrome.")
else:
    print(f"{num_to_check} is not a palindrome.")
```

### **Method 2: Calling the Function with User Input**

```python
# Function definition is the same as above
def is_palindrome(n):
    return str(n) == str(n)[::-1]

# --- Main Program ---
try:
    user_num = int(input("Enter a number to check: "))

    # Call the function in an if statement
    if is_palindrome(user_num):
        print(f"Yes, {user_num} is a palindrome.")
    else:
        print(f"No, {user_num} is not a palindrome.")

except ValueError:
    print("Error: Please enter a valid number.")
```
