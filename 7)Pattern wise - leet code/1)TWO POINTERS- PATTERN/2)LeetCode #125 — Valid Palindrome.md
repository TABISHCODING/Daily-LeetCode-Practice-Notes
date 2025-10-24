
---

# 🧩 **LeetCode 125. Valid Palindrome — Complete Structured Notes**

---

## 🧠 1. Problem Understanding (Simplified)

You are given a **string `s`** that may contain:

* Letters (`A–Z`, `a–z`)
* Digits (`0–9`)
* Spaces, punctuation, symbols, etc.

✅ **Goal:**
Check if the string is a **palindrome** —
reads the same forward and backward —
**after removing all non-alphanumeric characters** and **ignoring case**.

---

### ⚙️ Example 1

```python
Input:  s = "A man, a plan, a canal: Panama"
Output: True
```

**Why:**
After cleaning → `"amanaplanacanalpanama"`
Same forward and backward ✅

---

### ⚙️ Example 2

```python
Input:  s = "race a car"
Output: False
```

**Why:**
After cleaning → `"raceacar"`
Forward ≠ Backward ❌

---

### ⚙️ Example 3

```python
Input:  s = " "
Output: True
```

**Why:**
After cleaning → `""` (empty string)
An empty string is considered palindrome ✅

---

## 🧩 2. Approach 1 — Brute Force (Clean + Reverse Compare)

---

### 💡 Idea

1. Build a **cleaned version** of the string keeping only alphanumeric characters.
2. Convert all to lowercase.
3. Compare cleaned string with its reverse:

   * Same → palindrome ✅
   * Different → not palindrome ❌

---

### ⏱️ Time Complexity: O(n)

### 💾 Space Complexity: O(n)

---

### 🧾 Code — Brute Force

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # 1️⃣ Build a cleaned string with only alphanumeric characters (a–z, 0–9)
        clean = ""
        for ch in s:
            if ch.isalnum():          # Keep only letters and digits
                clean += ch.lower()   # Convert to lowercase and add to 'clean'
        
        # 2️⃣ Compare cleaned string with its reverse
        return clean == clean[::-1]
```

---

### 🧮 Dry Run — `"A man, a plan, a canal: Panama"`

| Step | ch  | ch.isalnum()? | Action  | clean                     |
| ---- | --- | ------------- | ------- | ------------------------- |
| 1    | 'A' | ✅             | Add 'a' | `"a"`                     |
| 2    | ' ' | ❌             | Skip    | `"a"`                     |
| 3    | 'm' | ✅             | Add 'm' | `"am"`                    |
| 4    | 'a' | ✅             | Add 'a' | `"ama"`                   |
| ...  | ... | ...           | ...     | ...                       |
| ✅    | —   | —             | —       | `"amanaplanacanalpanama"` |

Now check:

```
clean == clean[::-1] ✅
```

→ **Return True**

---

### ✅ Advantages

* Simple and clear for beginners.

### ⚠️ Limitations

* Uses extra O(n) space to store cleaned string.

---

## 🧩 3. Approach 2 — Two Pointer (Optimal, O(1) Space)

---

### 💡 Idea

Use **two pointers** —
`left` starts at beginning, `right` starts at end.

1. Move both pointers toward the center.
2. Skip all non-alphanumeric characters.
3. Compare lowercase versions of characters.
4. If mismatch → return False.
5. If loop ends → palindrome ✅

---

### ⏱️ Time Complexity: O(n)

### 💾 Space Complexity: O(1)

---

### 🧾 Code — Two Pointer Approach

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        # Initialize pointers
        left, right = 0, len(s) - 1

        # Loop until pointers meet
        while left < right:

            # 1️⃣ Skip non-alphanumeric characters from the left
            while left < right and not s[left].isalnum():
                left += 1  # move left pointer forward until a valid char

            # 2️⃣ Skip non-alphanumeric characters from the right
            while left < right and not s[right].isalnum():
                right -= 1  # move right pointer backward until valid char

            # 3️⃣ Compare lowercase versions of both characters
            if s[left].lower() != s[right].lower():
                return False  # ❌ mismatch found

            # 4️⃣ Move inward if match
            left += 1
            right -= 1

        # ✅ If loop completes, all chars matched
        return True
```

---

## 🔍 Deep Dive — How the “Skip” Works

These two lines:

```python
while left < right and not s[left].isalnum():
    left += 1

while left < right and not s[right].isalnum():
    right -= 1
```

mean:

> “Keep moving pointers inward until you find a letter or digit.”

This helps **ignore spaces, commas, punctuation, etc.**

---

Here is the final updated explanation, incorporating your clarification.

-----

✅ **Palindrome Check Machine Analogy**
Imagine we have two machines:

  * One on the left side
  * One on the right side

They are checking a sentence to see if it reads the same from both ends.

🏭 **The Machines Work Like This**
Each machine picks the next item from its side.

1.  **If the item is impurity** (like space, comma, punctuation):
      * → ⚠️ **Skip** and throw to trash. The machine moves to the next item immediately.
2.  **If it is pure** (letter or number):
      * → ✅ **Keep it** and wait for the other machine to also find a pure item.

Once *both* machines have found pure items, they ✅ **compare** them (ignoring case).

  * **If both are the same:**
      * 🟢 **Matching pure items** → They both throw their items away and move to the *next* one to start the process over.
  * **If different:**
      * 🔴 **Not the same** → The machines stop. It's **Not a palindrome**.
  * **If they cross each other:**
      * ✅ **Palindrome fully matched**. The job is done.

-----

✅ **Example Machine Run**
**Input:** `"@#A m,a@"`
**Characters:**
`@  #  A  _  m  ,  a  @`
`L                       R` (L=Left, R=Right)

| Step | Left Machine (L) | Right Machine (R) | Compare? | Action |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Sees `@` → impurity | Sees `@` → impurity | ❌ | Both skip. L moves right, R moves left. |
| 2 | Sees `#` → impurity | Sees `a` → pure | ❌ | L skips. R waits. L moves right. |
| 3 | Sees `A` → pure | Sees `a` → pure | ✅ | **Compare `A` and `a`**. They match (ignore case). |
| 4 | - | - | - | 🟢 **Match\!** Both machines move inward. |
| 5 | Sees `     ` → impurity | Sees `,` → impurity | ❌ | Both skip. L moves right, R moves left. |
| 6 | Sees `m` → pure | Sees `m` → pure | ✅ | **Compare `m` and `m`**. They match. |
| 7 | - | - | - | 🟢 **Match\!** Both machines move inward. |
| 8 | L and R have now crossed. | - | - | ✅ **Job done\!** |

→ Machines finish successfully ✅
→ **So, the string is a palindrome** ✅

-----

✅ **Key Takeaway: The Two Jobs of `left += 1` and `right -= 1`**

You are exactly right\! These lines are used in two different places for two different jobs: one *before* the comparison (to skip) and one *after* (to move on).

### 1\. The "Skip" Job (Inside the `while` loops)

This is your machine's **"⚠️ Skip"** action. It happens **before** the comparison. Its only goal is to find the next pure item.

```python
# JOB 1: Keep skipping until you find a pure item
while left < right and not s[left].isalnum():
    left += 1  
```

  * **What `left += 1` does here:** "The item at `s[left]` is an impurity (space, comma, etc.). **Skip it.** Move the left pointer one step to the right and check the *next* item."

<!-- end list -->

```python
# JOB 1: Keep skipping until you find a pure item
while left < right and not s[right].isalnum():
    right -= 1 
```

  * **What `right -= 1` does here:** "The item at `s[right]` is an impurity. **Skip it.** Move the right pointer one step to the left and check the *next* item."

### 2\. The "Move Inward" Job (After a successful match)

This is your machine's **"🟢 Matching pure items"** action. It happens **after** the two pure items have been successfully compared.

```python
            # 3️⃣ Compare the two pure items
            if s[left].lower() != s[right].lower():
                return False  # ❌ mismatch found

            # 4️⃣ Move inward if match
            left += 1   # <-- JOB 2: Move past the character we just matched
            right -= 1  # <-- JOB 2: Move past the character we just matched
```

  * **What `left += 1` and `right -= 1` do here:** "Great\! The items matched. We are **done with these two characters**. Now, move *both* pointers inward to find the *next* pair to compare."
