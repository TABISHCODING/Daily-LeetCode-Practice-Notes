
### 🧠 Problem Understanding

We need to check if we can find all characters of string `s` inside string `t`, **in the correct order**. We are allowed to "skip" characters in `t`, but not in `s`.

  * **Example:** `s = "ace"`, `t = "abcde"`
  * We look for 'a' in "abcde" -\> Found it at index 0.
  * *Now*, we look for 'c' *after* index 0 -\> Found it at index 2.
  * *Now*, we look for 'e' *after* index 2 -\> Found it at index 4.
  * Since we found all characters of `s`, the answer is `True`.

-----

### 🚀 The Two-Pointer Approach

1.  Initialize two pointers:
      * `s_ptr` (or `i`) starts at `0` (pointing to the start of `s`).
      * `t_ptr` (or `j`) starts at `0` (pointing to the start of `t`).
2.  Loop as long as both pointers are inside their strings.
3.  **Inside the loop:**
      * Compare the characters: `s[s_ptr]` and `t[t_ptr]`.
      * **If they match:** We found the character we were looking for. Move **both** pointers forward (`s_ptr += 1`, `t_ptr += 1`).
      * **If they don't match:** The character in `t` is not what we want. We "skip" it by moving only the `t_ptr` forward (`t_ptr += 1`), hoping to find our `s` character later.
4.  **After the loop:** The loop will stop when `s_ptr` or `t_ptr` (or both) go out of bounds.
      * If `s_ptr` reached the end of `s` (i.e., `s_ptr == len(s)`), it means we successfully found every single character from `s`. We return `True`.
      * If `s_ptr` did *not* reach the end, it means we ran out of characters in `t` before we could find all of `s`. We return `False`.

-----

### 🐍 Python Code

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        
        # Pointers for s and t
        s_ptr = 0
        t_ptr = 0
        
        # Loop as long as both pointers are within their string's bounds
        while s_ptr < len(s) and t_ptr < len(t):
            
            # If the characters match,
            # move the s_ptr to look for the *next* char in s
            if s[s_ptr] == t[t_ptr]:
                s_ptr += 1
            
            # ALWAYS move the t_ptr to check the next char in t
            t_ptr += 1
            
        # If s_ptr reached the end of s, it means we found all characters.
        # If s is an empty string, len(s) is 0 and s_ptr is 0, so it's True.
        return s_ptr == len(s)

```

-----

### Here is the logical flow:

1.  **The `while` loop asks:** "Are both pointers still inside their strings?"
2.  **If YES, it enters the loop and asks (Block 1):** "Do the characters match (`s[s_ptr] == t[t_ptr]`)?"
      * **If they MATCH (like in Iteration 1):**
        1.  Run the code *inside* the `if` block: `s_ptr += 1`.
        2.  Now the `if` block is finished.
        3.  Continue to the next line *outside* the `if` block: `t_ptr += 1`.
        4.  (Both pointers moved)
      * **If they DON'T MATCH (like in Iteration 2):**
        1.  **SKIP** the code *inside* the `if` block.
        2.  Continue to the next line *outside* the `if` block: `t_ptr += 1`.
        3.  (Only `t_ptr` moved)

**This is the logic:**

  * We **always** move `t_ptr` because we are scanning through the `t` string to find our character.
  * We **only** move `s_ptr` when we get a "hit" (a match), because that means we can now start looking for the *next* character in `s`.

Of course! This is a great way to understand an algorithm. The key to this code is:
* `t_ptr` (pointer for `t`) moves **every single time** (we're always scanning `t`).
* `s_ptr` (pointer for `s`) **only moves when we find a match** (we're looking for the *next* character in `s`).

Let's do a detailed dry run with two examples.

---

### ⚙️ Dry Run 1: `s = "ace"` and `t = "abcde"` (Should return `True`)

**Constants:**
* `len(s) = 3`
* `len(t) = 5`

**Setup:**
* `s_ptr` is set to `0`.
* `t_ptr` is set to `0`.

**Loop Execution:**

| Iteration | Line Being Run | Code | `s_ptr` | `t_ptr` | `s[s_ptr]` | `t[t_ptr]` | Condition Check | Result & Action |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :--- | :--- |
| 1 | `while ...` | `while 0 < 3 and 0 < 5` | 0 | 0 | - | - | `True and True` | **Enter loop** |
| | `if ...` | `if s[0] == t[0]` | 0 | 0 | 'a' | 'a' | `if 'a' == 'a'` | **True (Match!)** |
| | `s_ptr += 1` | `s_ptr += 1` | **1** | 0 | - | - | | `s_ptr` is now 1 |
| | `t_ptr += 1` | `t_ptr += 1` | 1 | **1** | - | - | | `t_ptr` is now 1 |
| - | - | - | - | - | - | - | - | - |
| 2 | `while ...` | `while 1 < 3 and 1 < 5` | 1 | 1 | - | - | `True and True` | **Enter loop** |
| | `if ...` | `if s[1] == t[1]` | 1 | 1 | 'c' | 'b' | `if 'c' == 'b'` | **False (No match)** |
| | `t_ptr += 1` | `t_ptr += 1` | 1 | **2** | - | - | | `t_ptr` is now 2 |
| - | - | - | - | - | - | - | - | - |
| 3 | `while ...` | `while 1 < 3 and 2 < 5` | 1 | 2 | - | - | `True and True` | **Enter loop** |
| | `if ...` | `if s[1] == t[2]` | 1 | 2 | 'c' | 'c' | `if 'c' == 'c'` | **True (Match!)** |
| | `s_ptr += 1` | `s_ptr += 1` | **2** | 2 | - | - | | `s_ptr` is now 2 |
| | `t_ptr += 1` | `t_ptr += 1` | 2 | **3** | - | - | | `t_ptr` is now 3 |
| - | - | - | - | - | - | - | - | - |
| 4 | `while ...` | `while 2 < 3 and 3 < 5` | 2 | 3 | - | - | `True and True` | **Enter loop** |
| | `if ...` | `if s[2] == t[3]` | 2 | 3 | 'e' | 'd' | `if 'e' == 'd'` | **False (No match)** |
| | `t_ptr += 1` | `t_ptr += 1` | 2 | **4** | - | - | | `t_ptr` is now 4 |
| - | - | - | - | - | - | - | - | - |
| 5 | `while ...` | `while 2 < 3 and 4 < 5` | 2 | 4 | - | - | `True and True` | **Enter loop** |
| | `if ...` | `if s[2] == t[4]` | 2 | 4 | 'e' | 'e' | `if 'e' == 'e'` | **True (Match!)** |
| | `s_ptr += 1` | `s_ptr += 1` | **3** | 4 | - | - | | `s_ptr` is now 3 |
| | `t_ptr += 1` | `t_ptr += 1` | 3 | **5** | - | - | | `t_ptr` is now 5 |
| - | - | - | - | - | - | - | - | - |
| 6 | `while ...` | `while 3 < 3 and 5 < 5` | 3 | 5 | - | - | `False and False` | **Exit loop** |

**Final Step:**
* **Code:** `return s_ptr == len(s)`
* **Check:** `return 3 == 3`
* **Result:** `True`

---

### ⚙️ Dry Run 2: `s = "axc"` and `t = "abcde"` (Should return `False`)

**Constants:**
* `len(s) = 3`
* `len(t) = 5`

**Setup:**
* `s_ptr` is set to `0`.
* `t_ptr` is set to `0`.

**Loop Execution:**

| Iteration | Line Being Run | Code | `s_ptr` | `t_ptr` | `s[s_ptr]` | `t[t_ptr]` | Condition Check | Result & Action |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :--- | :--- |
| 1 | `while ...` | `while 0 < 3 and 0 < 5` | 0 | 0 | - | - | `True and True` | **Enter loop** |
| | `if ...` | `if s[0] == t[0]` | 0 | 0 | 'a' | 'a' | `if 'a' == 'a'` | **True (Match!)** |
| | `s_ptr += 1` | `s_ptr += 1` | **1** | 0 | - | - | | `s_ptr` is now 1 |
| | `t_ptr += 1` | `t_ptr += 1` | 1 | **1** | - | - | | `t_ptr` is now 1 |
| - | - | - | - | - | - | - | - | - |
| 2 | `while ...` | `while 1 < 3 and 1 < 5` | 1 | 1 | - | - | `True and True` | **Enter loop** |
| | `if ...` | `if s[1] == t[1]` | 1 | 1 | 'x' | 'b' | `if 'x' == 'b'` | **False (No match)** |
| | `t_ptr += 1` | `t_ptr += 1` | 1 | **2** | - | - | | `t_ptr` is now 2 |
| - | - | - | - | - | - | - | - | - |
| 3 | `while ...` | `while 1 < 3 and 2 < 5` | 1 | 2 | - | - | `True and True` | **Enter loop** |
| | `if ...` | `if s[1] == t[2]` | 1 | 2 | 'x' | 'c' | `if 'x' == 'c'` | **False (No match)** |
| | `t_ptr += 1` | `t_ptr += 1` | 1 | **3** | - | - | | `t_ptr` is now 3 |
| - | - | - | - | - | - | - | - | - |
| 4 | `while ...` | `while 1 < 3 and 3 < 5` | 1 | 3 | - | - | `True and True` | **Enter loop** |
| | `if ...` | `if s[1] == t[3]` | 1 | 3 | 'x' | 'd' | `if 'x' == 'd'` | **False (No match)** |
| | `t_ptr += 1` | `t_ptr += 1` | 1 | **4** | - | - | | `t_ptr` is now 4 |
| - | - | - | - | - | - | - | - | - |
| 5 | `while ...` | `while 1 < 3 and 4 < 5` | 1 | 4 | - | - | `True and True` | **Enter loop** |
| | `if ...` | `if s[1] == t[4]` | 1 | 4 | 'x' | 'e' | `if 'x' == 'e'` | **False (No match)** |
| | `t_ptr += 1` | `t_ptr += 1` | 1 | **5** | - | - | | `t_ptr` is now 5 |
| - | - | - | - | - | - | - | - | - |
| 6 | `while ...` | `while 1 < 3 and 5 < 5` | 1 | 5 | - | - | `True and False` | **Exit loop** |

**Final Step:**
* **Code:** `return s_ptr == len(s)`
* **Check:** `return 1 == 3`
* **Result:** `False`

### 📊 Complexity Analysis

  * **Time Complexity:** $O(N)$, where $N$ is the length of the string `t`. In the worst case, we have to scan the entire string `t` exactly once.
  * **Space Complexity:** $O(1)$. We only use two integer variables (`s_ptr` and `t_ptr`), so the space is constant.
